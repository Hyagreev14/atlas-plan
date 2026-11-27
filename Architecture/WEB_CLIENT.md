# ATLAS Web client architecture

**Status:** Proposed. The web client is intended to be hosted by an ATLAS Server deployment; it is not an existing shipped application.

## Purpose

A self-hosted ATLAS instance should provide a browser-accessible interface in addition to accepting connections from ATLAS desktop clients. The browser client allows an authorized user to access server-backed workspace information from devices where the desktop application is not installed.

The web client should share ATLAS product language, design system, domain models and user-facing workflows where practical. It must not pretend that browser security boundaries are equivalent to native desktop capabilities.

## Hosting and request flow

The planned container deployment serves the compiled web application and the server API from one origin where practical:

1. Browser requests the ATLAS Web application from the configured server URL.
2. User authenticates with that instance.
3. Browser receives a secure session using the selected authentication design.
4. Web UI calls versioned server APIs.
5. Server independently authenticates and authorizes every request.
6. UI renders only data and actions the account is permitted to access.

Serving UI and API from one origin can simplify deployment and reduce cross-origin complexity, but the final routing and session design must be reviewed for CSRF, XSS, cookie and origin risks.

## Shared experience

The web client can expose server-backed features such as:
- Dashboard and workspace overview.
- Account profile and session/device management.
- Projects metadata and synchronized workspace organization.
- Recent activity that is explicitly synchronized and permitted.
- Server-backed AI conversations or settings only where the AI execution and provider-secret model is deliberately designed.
- Instance-specific pages for administrators, subject to role checks.

The exact screen inventory and feature parity with desktop remain product decisions. Do not claim that every desktop screen or capability will be available in a browser.

## Desktop versus browser capability boundary

| Capability | Desktop client | Browser client |
|---|---|---|
| View authorized synchronized data | Yes | Yes |
| Account and device management | Yes | Yes |
| Server-backed project metadata | Yes | Yes |
| Open arbitrary local project folders | With user permission | No general access |
| Launch installed desktop applications | Yes, through trusted local services | No |
| Execute local terminal commands | Through permission-controlled local services | No |
| Discover local developer tools | Through platform adapters | No |
| Access server-hosted data | Through authenticated API | Through authenticated API |
| Remote execution on another device | Not implicit | Not implicit |

A future desktop companion or remote agent could expose narrowly scoped capabilities, but it would be a separate security-sensitive design. It must require explicit pairing, device-level authorization, clear user presence/consent and the same ATLAS permission enforcement. The web server must never gain arbitrary command execution on a connected desktop merely because the user signed in.

## Responsive design

The web client should be usable on laptop, tablet and mobile-sized browser viewports. Responsive layout does not automatically make the browser a full mobile-native application. Touch interaction, narrow layouts, accessible navigation and session handling require their own design and tests.

## Security requirements

- Treat all browser input and stored browser state as untrusted.
- Enforce authorization on the server for every API request and object.
- Use secure session handling appropriate to the deployment and threat model.
- Protect state-changing requests against CSRF where cookie-based authentication is used.
- Apply a restrictive Content Security Policy and safe output encoding.
- Avoid storing long-lived bearer credentials in localStorage.
- Do not expose server secrets, AI provider keys or other users' data to the browser.
- Validate uploads and downloads, enforce size/type limits and prevent path traversal.
- Validate redirect targets and external links.
- Rate-limit authentication and sensitive endpoints.
- Keep audit records for security-relevant actions without recording secret values.

## API and compatibility

- Use an explicit API versioning policy.
- Generate or maintain typed client contracts from reviewed schemas where practical.
- Keep web and desktop clients compatible with a documented range of server versions.
- Return structured errors and capability information.
- Do not silently break older clients during server upgrades.
- Document which features are unavailable when the client/server version combination is unsupported.

## Acceptance criteria

- A user can open the configured server URL and reach the hosted ATLAS Web interface.
- The web client authenticates against that server and uses the same account and authorization boundaries as desktop clients.
- User A cannot access User B's data by changing IDs or API requests.
- Browser UI does not claim access to local filesystem, terminal or application-launch capabilities it does not possess.
- The interface remains usable at desktop and narrow viewport sizes.
- Security tests cover session handling, CSRF/XSS protections as applicable, authorization and sensitive data exposure.
