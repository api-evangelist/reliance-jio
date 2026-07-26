---
name: Create and record a JioMeet meeting
description: >-
  Provision a dynamic JioMeet meeting with a server-side app credential, hand the join
  links to participants, start and stop recording, and pull the recording back.
api: openapi/reliance-jio-jiomeet-platform-openapi.yml
server: https://jiomeetpro.jio.com
operations:
  - createADynamicMeeting        # POST /api/platform/v1/room
  - startRecording               # POST /api/platform/v1/recordings/start
  - checkRecordingStatus         # POST /api/platform/v1/recordings/isrecording
  - stopRecording                # POST /api/platform/v1/recordings/stop
  - listRecordings               # POST /api/platform/v1/recordings/list
generated: '2026-07-25'
method: generated
source: >-
  Grounded in the operations harvested from Jio's own API reference at dev.jiomeet.com.
  operationIds are assigned by overlays/reliance-jio-jiomeet-platform-overlay.yaml -
  Jio's spec declares none - so always resolve them to the method + path in the comment.
---

# Create and record a JioMeet meeting

Server-to-server flow on the **JioMeet Platform Server API**. Everything happens against
`https://jiomeetpro.jio.com`.

## Before you start

1. Create an app in the JioMeet console at <https://platform.jiomeet.com> and copy the
   **app id** and **secret**. The secret is shown once.
2. Mint a JWT yourself for every call — there is no token endpoint on this API. Sign it
   with the secret using **HS256** (one-step) or with your private key using **RS256**
   (two-step). The payload must carry an issuer and an `app` claim holding the app id.
   Keep the expiry short.
3. Send it as `Authorization: <jwt>` plus `Content-Type: application/json`. The spec
   models this as a required *header parameter*, not a security scheme — do not expect
   tooling to add it for you.

## Steps

1. **Create the meeting** — `createADynamicMeeting` (`POST /api/platform/v1/room`).
   Body: `name`, `title`, `description`, `hostToken` (boolean), `isAutoRecordingEnabled`
   (boolean). Set `hostToken: true` if you need a host join link.
   The 200 response returns `jiomeetId` (10 digits), `roomPIN`, `subdomain`,
   `joinEndpoint`, `hostToken`, `guestMeetingLink` and `meetingLink`.
   **A dynamic meeting is valid for 24 hours from creation.** Give guests
   `guestMeetingLink`; append the `hostToken` as a query parameter to grant host rights.
2. **Start recording** — `startRecording` (`POST /api/platform/v1/recordings/start`).
   Body: `jiomeetId` and `roomPIN`. The meeting must already be **started** or the call
   has no effect. Keep the returned `historyId` — it is how you fetch the recording later.
   Skip this step entirely if you set `isAutoRecordingEnabled: true` at creation, in
   which case recording begins once more than one participant is in the call.
3. **Poll status** — `checkRecordingStatus` (`POST /api/platform/v1/recordings/isrecording`)
   before you act on a recording; there is no callback and no webhook to tell you.
4. **Stop recording** — `stopRecording` (`POST /api/platform/v1/recordings/stop`).
5. **Fetch recordings** — `listRecordings` (`POST /api/platform/v1/recordings/list`).
6. **Report on the meeting** — `getMeetingReport`
   (`GET /api/platform/v1/analytics/report`) and `listChatThread`
   (`GET /api/platform/v1/chat/thread`) for attendance and chat history.

## Rules an agent must respect

- **There is no idempotency contract.** No `Idempotency-Key` header exists. Re-issuing
  `POST /api/platform/v1/room` creates a *second* meeting. Never blind-retry a create;
  on a timeout, treat the outcome as unknown and reconcile before retrying.
- **There is no pagination.** `listRecordings` and the report operations return whatever
  they return; there is no `limit`, `offset` or cursor.
- **There is no rate-limit contract** and no `429` declared. Back off conservatively.
- **There are no webhooks.** Every state change must be polled.
- **Errors** are not RFC 9457. Expect `application/json` with
  `{customCode, message, errors}` on 400/401 and `{customCode, message, errorsArray}` on
  **412**, which is Jio's validation status (not 422). See
  `errors/reliance-jio-problem-types.yml`.
- **Treat `hostToken`, `roomPIN` and the JWT as secrets** — the host token in a URL grants
  host control of the meeting to anyone holding the link.
