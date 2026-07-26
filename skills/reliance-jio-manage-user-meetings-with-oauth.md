---
name: Manage a JioMeet user's meetings with OAuth
description: >-
  Run the JioMeet OAuth 2.0 authorization-code flow, then create, fetch, list, update and
  cancel scheduled meetings on behalf of the signed-in user.
api: openapi/reliance-jio-jiomeet-oauth-openapi.yml
server: https://jiomeetpro.jio.com
operations:
  - accessTokenEndpointFetchAccessAndRefreshToken  # POST /api/oauth2/v2/token
  - userInfoFetchUserProfileInfo                   # GET  /api/my_profile
  - scheduledMeetingCreateAScheduledMeeting        # POST /api/meeting
  - scheduledMeetingListAllMeetingsOfUser          # GET  /api/meeting/{userId}
  - scheduledMeetingFetchAScheduledMeeting         # GET  /api/meeting/meetingDetails/{meetingId}
  - scheduledMeetingUpdateAScheduledMeeting        # PUT  /api/meeting/meetingDetails/{meetingId}
  - scheduledMeetingDeleteAScheduledMeeting        # POST /api/meeting/cancel/{meetingId}
generated: '2026-07-25'
method: generated
source: >-
  Grounded in the operations harvested from Jio's own API reference at dev.jiomeet.com
  plus the OAuth guide at /docs/quick-start/integrate_using_oauth_client. operationIds
  are assigned by overlays/reliance-jio-jiomeet-oauth-overlay.yaml - Jio's spec declares
  none - so always resolve them to the method + path in the comment.
---

# Manage a JioMeet user's meetings with OAuth

User-authorized flow on the **JioMeet Platform OAuth API**, against
`https://jiomeetpro.jio.com`. Use this — not the app-credential JWT surface — whenever
you act *as a person* rather than as the application.

## Authorize

1. Register an OAuth application in the JioMeet console and record `clientId`,
   `clientSecret` and your redirect URI. Jio enforces the redirect URI hard: HTTPS only,
   no raw IPs, no wildcards or fragments, and it must not carry the query parameters
   `sessionId`, `token`, `success`, `redirect_uri` or `clientId`.
2. Send the user to
   `https://jiomeetpro.jio.com/oauth2/authorize?clientId=…&redirect_uri=…&response_type=code&state=…`.
   Always send `state` (a base64-encoded CSRF token).
3. Exchange the code — `accessTokenEndpointFetchAccessAndRefreshToken`
   (`POST /api/oauth2/v2/token`). Authenticate the *client* with **HTTP Basic**
   (`clientId:clientSecret`), send `Content-Type: application/json`, and post
   `{"grant_type": "authorization_code", "code": "<code>"}`.
   The 200 returns `access_token`, `refresh_token`, `token_type` (Bearer), `expires_in`
   and the granted `scope`.
4. Call everything else with `Authorization: Bearer <access_token>`.

**Lifetimes:** authorization code 5 minutes, access token 1 day, refresh token 60 days.
Refresh with the same endpoint and `{"grant_type": "refresh_token", "refresh_token": "…"}`.

**Scopes** (request only what you use): `user:read`, `meeting:create`, `meeting:read`,
`meeting:update`, `meeting:delete`, `meeting:join`. Full reference:
`scopes/reliance-jio-scopes.yml`.

## Steps

1. **Identify the user** — `userInfoFetchUserProfileInfo` (`GET /api/my_profile`),
   scope `user:read`. Take the user id from here; you need it for the list call.
2. **Create a scheduled meeting** — `scheduledMeetingCreateAScheduledMeeting`
   (`POST /api/meeting`), scope `meeting:create`. `startTime` / `endTime` are ISO 8601.
3. **List the user's meetings** — `scheduledMeetingListAllMeetingsOfUser`
   (`GET /api/meeting/{userId}`), scope `meeting:read`.
4. **Fetch one** — `scheduledMeetingFetchAScheduledMeeting`
   (`GET /api/meeting/meetingDetails/{meetingId}`), scope `meeting:read`.
5. **Update** — `scheduledMeetingUpdateAScheduledMeeting`
   (`PUT /api/meeting/meetingDetails/{meetingId}`), scope `meeting:update`.
6. **Cancel** — `scheduledMeetingDeleteAScheduledMeeting`
   (`POST /api/meeting/cancel/{meetingId}`), scope `meeting:delete`. Note it is a
   **POST to /cancel/**, not an HTTP DELETE.

## Rules an agent must respect

- **Cancelling is a POST.** Do not assume REST verb symmetry on this API.
- **No idempotency key exists.** A retried `POST /api/meeting` schedules a duplicate
  meeting. Reconcile with the list operation before retrying.
- **No pagination** on `GET /api/meeting/{userId}`.
- **412** is the validation failure status (`{customCode, message, errorsArray}`); 401
  means the bearer token is missing, expired or out of scope. See
  `errors/reliance-jio-problem-types.yml`.
- **Cancelling a meeting is destructive and unrecoverable** — confirm with the user
  before calling it. The agentic-access profile classifies it as an acting operation.
- **No webhooks**: if you need to know a meeting changed, poll.
