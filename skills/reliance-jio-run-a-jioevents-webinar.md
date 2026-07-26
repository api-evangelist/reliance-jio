---
name: Run a JioEvents webinar end to end
description: >-
  Schedule a JioEvents webinar, add sessions to it, issue and manage meeting invites, and
  download the attendance and registration report.
api: openapi/reliance-jio-jioevents-platform-openapi.yml
server: https://jioevents.com
operations:
  - scheduledWebinarCreateAScheduledWebinar    # POST   /api/platform/v1/schedule/webinar
  - scheduledWebinarFetchAScheduledWebinar     # GET    /api/platform/v1/schedule/webinar
  - scheduledWebinarUpdateAScheduledWebinar    # PUT    /api/platform/v1/schedule/webinar
  - scheduledWebinarDeleteAScheduledWebinar    # DELETE /api/platform/v1/schedule/webinar
  - sessionsCreateASession                     # POST   /api/platform/v1/sessions/{meetingId}
  - sessionsGetSessions                        # GET    /api/platform/v1/sessions/{meetingId}
  - sessionsDeleteASession                     # DELETE /api/platform/v1/sessions/{meetingId}/{sessionId}
  - meetingInviteCreateAMeetingInvite          # POST   /api/platform/v1/meetingInvite
  - meetingInviteGetMeetingInvites             # GET    /api/platform/v1/meetingInvite/{meetingId}
  - meetingInviteDeleteMeetingInvites          # DELETE /api/platform/v1/meetingInvite/{meetingId}
  - webinarDownloadAttendanceRegistrationReport # GET   /api/platform/v1/webinar/{meetingId}/download
generated: '2026-07-25'
method: generated
source: >-
  Grounded in the operations harvested from Jio's own API reference at dev.jiomeet.com.
  operationIds are assigned by overlays/reliance-jio-jioevents-platform-overlay.yaml -
  Jio's spec declares none - so always resolve them to the method + path in the comment.
---

# Run a JioEvents webinar end to end

Server-to-server flow on the **JioEvents Platform Server API**. Note the host: this API
runs on `https://jioevents.com`, **not** on `jiomeetpro.jio.com` like the JioMeet APIs.
Neither host is written down in Jio's prose documentation.

## Before you start

Authenticate exactly as for the JioMeet Platform Server API: a self-signed JWT (HS256 or
RS256) built from JioMeet app credentials, sent as the `Authorization` header alongside
`Content-Type: application/json`. See `authentication/reliance-jio-authentication.yml`.

## Steps

1. **Schedule the webinar** — `scheduledWebinarCreateAScheduledWebinar`
   (`POST /api/platform/v1/schedule/webinar`). Keep the returned meeting id; every other
   operation in this flow is keyed on it as `{meetingId}`.
2. **Verify it** — `scheduledWebinarFetchAScheduledWebinar`
   (`GET /api/platform/v1/schedule/webinar`).
3. **Add sessions** — `sessionsCreateASession`
   (`POST /api/platform/v1/sessions/{meetingId}`), one call per session. Read them back
   with `sessionsGetSessions` (`GET /api/platform/v1/sessions/{meetingId}`) and remove one
   with `sessionsDeleteASession`
   (`DELETE /api/platform/v1/sessions/{meetingId}/{sessionId}`).
4. **Invite people** — `meetingInviteCreateAMeetingInvite`
   (`POST /api/platform/v1/meetingInvite`). List with
   `meetingInviteGetMeetingInvites` (`GET /api/platform/v1/meetingInvite/{meetingId}`).
5. **Amend the agenda** — `scheduledWebinarUpdateAScheduledWebinar`
   (`PUT /api/platform/v1/schedule/webinar`).
6. **Report** — `webinarDownloadAttendanceRegistrationReport`
   (`GET /api/platform/v1/webinar/{meetingId}/download`) returns the attendance and
   registration report after the event.
7. **Tear down** — `scheduledWebinarDeleteAScheduledWebinar`
   (`DELETE /api/platform/v1/schedule/webinar`) and, if needed,
   `meetingInviteDeleteMeetingInvites`
   (`DELETE /api/platform/v1/meetingInvite/{meetingId}`).

## Rules an agent must respect

- **Deletes here are bulk and unqualified.** `DELETE /api/platform/v1/meetingInvite/{meetingId}`
  deletes *meeting invites* (plural) for that webinar, and
  `DELETE /api/platform/v1/schedule/webinar` takes the webinar itself. Confirm with a
  human before either — the agentic-access profile raises the webinar delete to the
  highest consequence class in this provider.
- **No idempotency, no pagination, no rate-limit contract, no webhooks.** Re-issuing a
  create makes a duplicate; list operations return everything; nothing is pushed to you.
- **Errors**: `{customCode, message, errors}` on 400/401, `{customCode, message,
  errorsArray}` on **412** (Jio's validation status). See
  `errors/reliance-jio-problem-types.yml`.
- **Do not cross the hosts.** A JioEvents meeting id is not addressable on the JioMeet
  platform API and vice versa, even though both use `/api/platform/v1/` path prefixes.
