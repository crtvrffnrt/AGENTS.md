# BloodHound Helper Profile

## Scope

This repository is for interacting with the BloodHound Enterprise API or Bloodhound CE.

## Source of Truth

- Read `creds.txt` first. It contains the target hostname and the credentials needed to interact with the BloodHound instance.
- Prefer the live API over memory. Confirm behavior against `/api/v2/spec` before assuming endpoint shape, request bodies, or identifiers.

## BloodHound API Notes

- Use the BloodHound API for BloodHound Enterprise and Community Edition tasks.
- Prefer the API spec and reference pages over assumptions.
- When possible, confirm the API version and available endpoints before making broader requests.
- The instance usually exposes the spec at `/api/v2/spec` without authentication.
- The UI is under `/ui`, but the API routes are under `/api/v2`.
- Useful starting endpoints:
  - `/api/v2/login`
  - `/api/v2/self`
  - `/api/v2/available-domains`
  - `/api/v2/search`
  - `/api/v2/graphs/cypher`
  - `/api/v2/pathfinding`
  - `/api/v2/attack-paths/details`
- For entity drill-down, common routes include:
  - `/api/v2/users/{object_id}`
  - `/api/v2/groups/{object_id}`
  - `/api/v2/computers/{object_id}`
  - `/api/v2/domains/{object_id}`
- For graph queries, the cypher API returns a unified graph payload with `nodes`, `edges`, and `literals`. Use the actual `objectid`/SID values from node properties when possible.
- The `pathfinding` endpoint expects raw node identifiers in `start_node` and `end_node`. Do not assume the `node_...` prefix form works for the API.
- If you need attack-path or finding data, check `/api/v2/attack-paths/details` first. It often exposes the actual source/target nodes and accepted state directly.

## Authentication

BloodHound supports two authentication styles:

- `JWT bearer token` for temporary, short-lived access.
- `Signed requests` for long-lived integrations. This is the preferred method.

### JWT bearer token

- Send the token as `Authorization: Bearer $JWT_TOKEN`.
- Use this only when you need a quick, temporary session.
- The login request uses JSON with `login_method: "secret"`, `username`, and `secret`.
- The login response includes `data.session_token`.

### Signed requests

- Use signed requests for durable automation.
- Required headers:
  - `Authorization: bhesignature $TOKEN_ID`
  - `RequestDate: $RFC3339_DATETIME`
  - `Signature: $BASE64ENCODED_HMAC_SIGNATURE`
- The token ID is public-ish and identifies the client.
- The token key is secret and must be protected like a password.
- The signature is based on the request method, request URI, request timestamp, and body.

## Practical Workflow

1. Read `creds.txt` and identify the hostname and auth material.
2. Determine whether the task is a one-off lookup or a longer-lived integration.
3. Use JWT only for quick temporary calls.
4. Use signed requests for repeated or persistent access.
5. Prefer the smallest request that answers the question.
6. Verify responses against the API reference if endpoint behavior is unclear.
7. For challenge or flag-style questions, inspect the relevant finding or path record before guessing the final identifier.
8. When a user says a UPN is excluded, check the underlying SID/object ID and the graph node id separately. BloodHound may surface different identifiers in the UI, API, and export views.

## Working Rules

- Do not assume endpoint shapes or auth details that are not supported by the reference.
- Use direct, concrete requests and verify the result before moving on.
- If a graph query or path search returns unexpected data, verify whether the API wants raw IDs, not UI-rendered `node_...` or `edge_...` tokens.
- If `creds.txt`, an API spec, or required auth material is unavailable, state the gap and use only safe local context until the missing input is provided.
- Do not store credentials, tokens, hostnames, or customer graph details as memory. Stable API quirks and generic query patterns may be memory candidates if the runtime supports memory.
