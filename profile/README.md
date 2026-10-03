## EdgeRush

A Kubernetes-native API gateway written in Rust: an operator, control planes and data
planes in one binary; Ingress and Gateway API served from the same data plane; cluster-wide
rate limiting with no external store.

**Status: the data plane runs; Kubernetes does not yet.** The proxy serves traffic from a
YAML file; the control plane, the operator and the rate limiter are still to be built. Not
for production. A hobby project with no timelines.

### What it is for

- **One data plane for Ingress and Gateway API**, side by side, from ordinary Kubernetes
  objects. Ingress stays a first-class API.
- **Operator-driven.** `ControlPlane` and `DataPlane` resources become Deployments and
  Services; one control plane can drive many data planes, each its own failure domain.
- **Cluster-wide rate limiting with no external store.** Counters live in the data plane's
  memory and are shared between its pods peer to peer, off the request path, and limits
  keep working when the control plane is down.
- **Low added latency, measured.** Thread-per-core on Tokio, our own HTTP/1 server and
  client, compiled filter chains, benchmarked beside NGINX, HAProxy, Envoy and Kong doing
  the same work on the same machine.

### What works today

HTTP/1.1, HTTP/2 and HTTP/3 (QUIC) from clients; gRPC; WebSocket; TLS on BoringSSL, with
certificates chosen by SNI and mTLS both ways; Gateway API's matching and precedence;
redirects, rewrites and mirrors; load balancing, health checks, timeouts and retries; TCP
and TLS passthrough; PROXY protocol; Prometheus metrics.

### Get involved

- [**edgerush**](https://github.com/edgerush-dev/edgerush): the code, and a README that
  shows how to try it
- [Contributing](https://github.com/edgerush-dev/edgerush/blob/main/CONTRIBUTING.md):
  contributions of any size are welcome, AI-assisted ones included
- [Security](https://github.com/edgerush-dev/edgerush/blob/main/SECURITY.md): report
  problems privately
- Anything else: hello@edgerush.dev

EdgeRush is open source under the Apache-2.0 licence.
