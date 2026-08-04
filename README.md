# Reliance Jio (reliance-jio)

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

Reliance Jio Infocomm, the telecom arm of Jio Platforms Limited and Reliance Industries, is India's largest mobile network operator, serving roughly half a billion subscribers on an all-IP 4G/5G network from its home market of India, alongside JioFiber broadband, JioAirFiber fixed wireless, IoT connectivity, and an enterprise CPaaS business branded JioCX. Jio sits at the network-operator layer of the telecom value chain and its API posture is split in two — standards-forward on the inside, intermediated on the outside, and genuinely self-serve only for its SaaS products.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/reliance-jio/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/reliance-jio/refs/heads/main/apis.yml)

## Tags

- Telecommunications
- India
- Mobile Network Operator
- Network APIs
- CAMARA
- Open Gateway
- SIM Swap
- Identity Verification
- CPaaS
- Messaging
- Voice
- IoT
- Broadband
- 5G
- BSS
- OSS
- Standards
- Video Conferencing

## Timestamps

- **Created:** 2026-07-25
- **Modified:** 2026-07-25

## APIs

### JioMeet Platform Server API

Server-to-server REST API for the JioMeet video meeting platform, documented publicly at dev.jiomeet.com. Covers creating dynamic meetings, creating, fetching, updating and deleting scheduled meetings, starting, stopping and listing recordings, checking recording status, listing chat threads, and pulling meeting reports. Authentication is an HS256-signed JWT built from an app id and secret generated in the JioMeet platform console.

- **Human URL:** [https://dev.jiomeet.com/docs/JioMeet%20Platform%20Server%20APIs/jiomeet-platform-apis](https://dev.jiomeet.com/docs/JioMeet%20Platform%20Server%20APIs/jiomeet-platform-apis)

#### Tags

- Video
- Meetings
- Recording
- Collaboration

#### Properties

- [Documentation](https://dev.jiomeet.com/docs/quick-start/integrate-with-ser)
- [API Reference](https://dev.jiomeet.com/docs/JioMeet%20Platform%20Server%20APIs/jiomeet-platform-apis)
- [Authentication](https://dev.jiomeet.com/docs/quick-start/authentication)

### JioMeet Platform OAuth API

User-authorized REST API for JioMeet, using OAuth 2.0. An access and refresh token are obtained from the `/api/oauth2/v2/token` endpoint using HTTP Basic authentication with an OAuth client id and secret, and subsequent calls use HTTP Bearer authentication. Documented operations cover creating, fetching, listing, updating and deleting a user's scheduled meetings and fetching user profile info.

- **Human URL:** [https://dev.jiomeet.com/docs/JioMeet%20Platform%20OAuth%20APIs/jiomeet-user-oauth-apis](https://dev.jiomeet.com/docs/JioMeet%20Platform%20OAuth%20APIs/jiomeet-user-oauth-apis)

#### Tags

- Video
- Meetings
- OAuth
- Identity

#### Properties

- [Documentation](https://dev.jiomeet.com/docs/quick-start/integrate_using_oauth_client)
- [API Reference](https://dev.jiomeet.com/docs/JioMeet%20Platform%20OAuth%20APIs/jiomeet-user-oauth-apis)
- [Authentication](https://dev.jiomeet.com/docs/JioMeet%20Platform%20OAuth%20APIs/access-token-endpoint-fetch-access-and-refresh-token)

### JioEvents Platform Server API

Server-side REST API for JioEvents, Jio's webinar and virtual event platform, documented alongside JioMeet at dev.jiomeet.com. Covers creating, fetching, updating and deleting scheduled webinars, creating, listing and deleting sessions, creating, listing and deleting meeting invites, and downloading attendance and registration reports.

- **Human URL:** [https://dev.jiomeet.com/docs/JioEvents%20Platform%20Server%20APIs/jioevents-platform-apis](https://dev.jiomeet.com/docs/JioEvents%20Platform%20Server%20APIs/jioevents-platform-apis)

#### Tags

- Events
- Webinars
- Video

#### Properties

- [Documentation](https://dev.jiomeet.com/docs/JioEvents%20Platform%20Server%20APIs/jioevents-platform-apis)
- [API Reference](https://dev.jiomeet.com/docs/JioEvents%20Platform%20Server%20APIs/scheduled-webinar-create-a-scheduled-webinar)

### JioPayments Set-Top-Box API

In-app purchase and digital content payment API for applications published on the Jio set-top box, distributed by Jio Platforms as a downloadable PDF API specification (v1.1) from the JioDevelopers set-top-box developer page. The specification PDF is publicly retrievable without login; the developer console that issues credentials is behind a sign-up wall.

- **Human URL:** [https://developer.jio.com/set-top-box.html](https://developer.jio.com/set-top-box.html)

#### Tags

- Payments
- Set-Top Box
- Media

#### Properties

- [Documentation](https://developer.jio.com/set-top-box.html)
- [API Reference](https://jiomedia.akamaized.net//JioStore/Downloads/DeveloperToolKit/STB/JioPayments-STB-APISpecs-v1.1.pdf)

## Reviewer Notes

- **Real self-serve portal:** [https://dev.jiomeet.com/](https://dev.jiomeet.com/) (HTTP 200) — public docs, quick starts, per-operation API reference, SDK guides, and a sign-up path to [platform.jiomeet.com](https://platform.jiomeet.com/). This is the only surface where a developer can go from reading to calling on their own.
- **First-party portal at the primary domain:** [https://developer.jio.com/](https://developer.jio.com/) (HTTP 200) — a set-top-box app developer programme, console behind a login, footer still dated 2022.
- **No OpenAPI anywhere.** `/openapi.json`, `/openapi.yaml`, `/swagger.json`, `/api-docs`, `/spec` and `/redoc` all return 404 on dev.jiomeet.com. The reference pages are generated by the docusaurus-openapi-docs plugin, so a source spec exists internally — it is simply never served. The only downloadable specification of any kind is a PDF (JioPayments STB API Specs v1.1). Nothing was harvested; there is no `openapi/` directory.
- **CAMARA posture:** Jio has **launched** the CAMARA **SIM Swap** API alongside Bharti Airtel and Vodafone Idea under GSMA Open Gateway (GSMA press release, 9 October 2025). A CAMARA **Number Verification** API was announced for end-2025 but no Jio-hosted documentation, endpoint or spec for it was found — on the evidence available that one is still an announcement, not an implementation. Jio publishes **zero** CAMARA artifacts of its own.
- **No Open Gateway portal.** `opengateway.jio.com` and `developers.opengateway.jio.com` do not resolve; `jio.com/opengateway` redirects to the 404 page. The Telefónica-style pattern is absent.
- **Channel to developers is Aduna.** Reliance Jio is one of the twelve carrier equity owners of Aduna, the Ericsson-led network-API joint venture. Jio's network APIs reach developers through Aduna, the GSMA federated hub, and CPaaS partners — never directly from Jio. That intermediation is the defining fact about this provider.
- **TM Forum:** Jio was the **first** communications service provider to achieve TM Forum **Open API Platinum** conformance — 23 certifications across more than 20 Open APIs, with a public conformance report for TMF653. Those are BSS/OSS supplier-integration interfaces: certified, real, and entirely non-public.
- **Auth:** HS256 JWT (JioMeet server APIs) and OAuth 2.0 Basic-then-Bearer (JioMeet OAuth APIs). **CIBA does not appear anywhere.** No Jio OIDC discovery document is served — `.well-known/openid-configuration` returns the SPA shell on www.jio.com, 404 on the JioMeet hosts, and 403 on api.jio.com.
- **3GPP:** no NEF, SCEF, network-slicing or edge/MEC API documentation was found.
- **Webhooks / AsyncAPI:** none. The nearest event surface is browser `postMessage` events for the JioMeet web iframe embed.
- **SDKs:** 34 public repositories at [github.com/JioMeet](https://github.com/JioMeet) — iOS, Android, Web, Flutter, React Native, plus Video KYC, Translate and Localization SDKs. The `RelianceJio` and `JioPlatforms` GitHub organizations exist but publish nothing.
- **JioCX (Jio's own CPaaS):** SMS, Voice, WhatsApp, RCS, Email, Alerts and branded caller ID are marketed under `jio.com/business/services/cpaas` with no API reference, no sandbox and no keys; `jiocx.com` and `developer.jiocx.com` both return 403. Jio competes with the CPaaS aggregators while publishing like a carrier.

## Links

- [Website](https://www.jio.com/)
- [JioMeet Developer Documentation](https://dev.jiomeet.com/)
- [JioDevelopers Platform](https://developer.jio.com/)
- [JioMeet Platform Console](https://platform.jiomeet.com/)
- [GitHub Organization](https://github.com/JioMeet)
- [LinkedIn](https://www.linkedin.com/company/jio/)
- [JioGames Developer Program](https://developer.jiogames.com/)
- [JioGames Publishing Documentation](https://publish.jiogames.com/documents/)
- [JioCX CPaaS](https://www.jio.com/business/services/jiocx/)
- [Jio Business IoT](https://www.jio.com/business/services/iot/)
- [GSMA Open Gateway press release — Indian operators, 9 Oct 2025](https://www.gsma.com/newsroom/press-release/indian-mobile-operators-help-online-businesses-combat-scams-and-identity-theft-through-new-federated-network-services-supported-by-gsma-open-gateway/)
- [TM Forum Open API conformance report — TMF653](https://s3.us-east-1.amazonaws.com/tmf-sfdc-public/Conformance/CON-01539/JIO-Certification%20Report-TMF653%20API-Aug2022.pdf)
- [Aduna](https://adunaglobal.com/)
