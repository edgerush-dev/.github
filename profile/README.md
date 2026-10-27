## EdgeRush

A Kubernetes-native API gateway written in Rust: an operator, control planes and data
planes in one binary; Ingress and Gateway API served from the same data plane; rate
limiting per pod or cluster-wide with no external store to run.

**Status: the data plane runs; Kubernetes is arriving.** The proxy serves traffic from a
YAML file, and in a cluster follows Services' endpoints itself; rate limiting runs, each
pod on its own or through EdgeRush's rate-limiting service; the control plane translates
Ingresses but does not yet hand its config to data planes, and the operator is still to be
built. Not for production. A hobby project with no timelines.

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

HTTP/1.1, HTTP/2 and HTTP/3 (QUIC) from clients; gRPC; WebSocket; TLS on BoringSSL, with
certificates chosen by SNI and mTLS both ways; Gateway API's matching and precedence;
redirects, rewrites and mirrors; load balancing, health checks, timeouts and retries; TCP
and TLS passthrough; PROXY protocol; Prometheus metrics; rate limiting, per pod or decided
by EdgeRush's rate-limiting service. Begun: `edgerush controller`, translating Ingresses as
the cluster changes, and the data plane following EndpointSlices itself.

### Get involved

- [**edgerush**](https://github.com/edgerush-dev/edgerush): the code, and a README that
  shows how to try it
- [Contributing](https://github.com/edgerush-dev/edgerush/blob/main/CONTRIBUTING.md):
  contributions of any size are welcome, AI-assisted ones included
- [Security](https://github.com/edgerush-dev/edgerush/blob/main/SECURITY.md): report
  problems privately
- Anything else: hello@edgerush.dev

EdgeRush is open source under the Apache-2.0 licence.
