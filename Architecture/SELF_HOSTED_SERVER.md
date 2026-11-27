# ATLAS self-hosted server architecture

**Status:** Proposed architecture. No server implementation, Docker image, API contract or deployment port is implied to exist yet.

## Purpose

ATLAS Server is an optional, user-operated service that adds server-managed identity, multi-user administration, cross-device synchronization and browser access. It can be deployed on a home server, NAS, VPS or another supported host.

The server must not turn ATLAS into a mandatory cloud product. Standalone desktop mode remains independently useful.

## Logical responsibilities

### 1. HTTP entry point

- Serve the ATLAS Web application assets.
- Expose a versioned API for authentication, account operations, device registration, synchronization and server administration.
- Terminate or sit behind HTTPS in production deployments.
- Apply request size limits, rate limits and safe error handling.
- Validate origin, host and forwarded-header handling; do not trust arbitrary proxy headers.

### 2. Identity and session service

- Create and authenticate server-local user accounts.
- Support administrator-managed invitations or account creation policy.
- Issue revocable sessions or tokens with bounded lifetime and scope.
- Track linked devices and active sessions.
- Support logout, session revocation, password reset/recovery policy and administrator recovery procedures.
- Avoid exposing whether an account exists through distinguishable unauthenticated errors where practical.

Authentication method selection (password, passkey, OIDC or other options) remains an implementation decision requiring threat modelling. Do not imply that any particular method is already selected.

### 3. Authorization and tenant isolation

- Treat each account as a distinct security boundary.
- Enforce authorization on the server for every object and operation; hiding UI controls is not authorization.
- Scope user-owned records by immutable internal user identifiers, not display names or client-supplied ownership claims.
- Define explicit roles for instance administration and ordinary users.
- Prevent one user from enumerating, reading, modifying or deleting another user's data.
- Audit security-sensitive administrative actions without recording secret values.

### 4. Synchronization service

- Exchange only data categories explicitly designated as synchronizable.
- Authenticate and authorize every sync request.
- Use versioned records or change cursors so clients can resume after interruption.
- Make retries idempotent and protect against duplicate writes.
- Return structured conflict information instead of silently overwriting concurrent edits.
- Support tombstones or equivalent deletion propagation, with documented retention and restore behaviour.
- Never treat a client-provided user ID as proof of identity.

### 5. Persistence layer

The implementation must choose and document its database and migration strategy. Persistent data must live outside the disposable container filesystem, in a named volume or explicitly mounted host path.

The server needs documented:
- Schema migrations and supported upgrade paths.
- Backup and restore procedures.
- Data export and deletion behaviour.
- Storage permissions and encryption-at-rest assumptions.
- Recovery behaviour after interrupted writes or disk-full conditions.

Do not hard-code a database choice in this planning document before evaluating operational needs.

## Container deployment model

The intended user experience is a Docker-based installation. A future image may bundle the server API and the static web client in one container initially, provided internal boundaries remain clear enough to split services later if scaling or maintenance requires it.

Illustrative port mapping:

```bash
docker run -d \
  --name atlas-server \
  -p 8080:8080 \
  -v atlas-data:/app/data \
  --restart unless-stopped \
  <future-atlas-server-image>
```

This is conceptual only. The image name, internal port, volume path, environment variables, health check and supported architectures are not yet defined. Do not publish this as a working install command until an image and deployment contract exist.

### Container requirements

- Run as a non-root user where feasible.
- Keep persistent state in explicit volumes.
- Provide a health endpoint and container health check.
- Handle SIGTERM and graceful shutdown.
- Support configuration through documented environment variables or a mounted config file; never bake secrets into the image.
- Pin and publish image versions; document upgrade and rollback constraints.
- Minimize image contents and scan dependencies.
- Avoid privileged mode and unnecessary host mounts.
- Do not mount the Docker socket into the application container.
- Make logs useful but redact credentials, tokens and private project content.

### Networking and exposure

- Binding a host port with Docker's `-p` publishes a container port on the host; it does not by itself make the service safely or universally reachable from the public internet.
- Local-only deployments should be able to bind to loopback.
- Remote access requires a deliberate network design such as a trusted private network or reverse proxy with HTTPS.
- Never recommend exposing an unauthenticated instance directly to the internet.
- Document firewall, TLS, proxy, DNS and update responsibilities for self-hosters.
- Avoid assuming that port 8080 is final; it is only an example in planning.

## Web application hosting

The server deployment should serve the ATLAS Web frontend and route API requests to the backend. The browser UI and API should share the same server identity and permission model.

The web client is not equivalent to the desktop app: a browser cannot freely launch local executables, inspect arbitrary local directories or access privileged desktop integrations. Those capabilities remain desktop-local unless a separately designed and explicitly authorized companion/remote-execution system is introduced.

## Operations and administration

A self-hosted release needs a first-run setup flow that:
- Creates or securely bootstraps the initial instance administrator.
- Requires changing/removing any one-time bootstrap credential.
- Makes account creation policy explicit (admin invite, open registration or disabled).
- Displays server version, health and storage status.
- Provides documented backup, restore, upgrade and recovery paths.
- Shows connected devices and allows revocation.
- Makes security and network exposure state understandable to the operator.

## Non-goals for the initial server design

- No ATLAS-operated mandatory cloud.
- No automatic remote control of client machines.
- No implicit synchronization of entire project directories.
- No server-side storage of plaintext local credentials by default.
- No promise of high availability, clustering or horizontal scaling in the first release.
- No claim that a Docker image or web app is implemented.

## Required design work before implementation

1. Threat model for internet-facing and LAN-only deployment.
2. Authentication, session and recovery design.
3. Tenant and object-level authorization model.
4. Sync protocol, versioning and conflict semantics.
5. Database selection, migrations, backup and restore.
6. Container configuration, health checks, update and rollback contract.
7. HTTPS/reverse-proxy and network exposure guide.
8. Operational tests for account isolation, backup recovery and upgrade safety.
