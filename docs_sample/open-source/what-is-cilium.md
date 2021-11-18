## Cilium | eBPF-based Networking, Observability, and Security
Cilium is an open source project to provide eBPF-based networking, security, and observability for cloud native environments such as Kubernetes clusters and other container orchestration platforms.


# The Cilium in use by Accuknox contains several upgrades including 

Accuknox has been contributing  to Cilium and maintains a fork of the same (which is being upstreamed back to the primary distribution) with improvements in the following areas
 - Extensible Identity solution based on SPIFFE standards
 - Improving policy audit handling
 - Improving policy telemetry and statistics collection to fit realistic scenarios
 - Policy discovery tools.

 # Where can I get the upgrades to Cilium
 Find upgrades to our Cilium policies by visiting our open source github repos at https://github.com/kubearmor/cilium


# Do we intend to maintain a separate version of Cilium?

No. A fork exists to allow our community of users to directly access the feature upgrades that Accuknox is building. However all changes are being upstreamed to the community hosted at https://github.com/cilium

