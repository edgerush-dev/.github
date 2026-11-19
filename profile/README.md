## EdgeRush

A Kubernetes-native API gateway written in Rust: an operator, control planes and data
planes in one binary; Ingress and Gateway API served from the same data plane; rate
limiting per pod or cluster-wide with no external store to run.

**Status: it runs in a cluster, set up by its operator, and passes Gateway API's core
conformance tests.** No images are published yet, so it is built from source. Not for
production. A hobby project with no timelines.

### What it is for

- **One data plane for Ingress and Gateway API**, side by side, from ordinary Kubernetes
  objects. Ingress stays a first-class API.
- **Operator-driven.** `ControlPlane` and `DataPlane` resources become Deployments and
  Services; one control plane can drive many data planes, each its own failure domain.
- **Rate limiting per pod or across the cluster, with no external store to run.** One mode
  for each data plane: each pod limiting on what it sees, or counts kept in memory in
  EdgeRush's own rate-limiting service, packaged with it. Limits keep working when the
  control plane is down.
- **Low added latency, measured.** Thread-per-core on Tokio, our own HTTP/1 server and
  client, compiled filter chains, benchmarked beside NGINX, HAProxy, Envoy and Kong doing
  the same work on the same machine.

### What works today

- **Protocols:** HTTP/1.1, HTTP/2 and HTTP/3; gRPC; WebSocket; TCP, TLS passthrough and UDP
- **TLS** on BoringSSL, with mTLS to clients and to backends
- **Routing:** Gateway API's matching, redirects, rewrites and mirrors
- **Backends:** load balancing, health checks, timeouts and retries
- **Rate limiting:** token bucket, fixed or rolling window; per pod, or shared between
  pods through EdgeRush's own service
- **Kubernetes:** Ingress and Gateway API from one data plane, set up by the operator
- **Conformance:** passes Gateway API's core tests for HTTP, gRPC, TLS and TCP routes

### Get involved

- [**edgerush**](https://github.com/edgerush-dev/edgerush): the code, and a README that
  shows how to try it
- [Contributing](https://github.com/edgerush-dev/edgerush/blob/main/CONTRIBUTING.md):
  contributions of any size are welcome, AI-assisted ones included
- [Security](https://github.com/edgerush-dev/edgerush/blob/main/SECURITY.md): report
  problems privately
- Anything else: hello@edgerush.dev

EdgeRush is open source under the Apache-2.0 licence.
