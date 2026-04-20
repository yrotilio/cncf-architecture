---
title: An anywhere «Kubernetes Service» compatible with both Private and Public Clouds.
date: 2026-04-28

org_name: SNCF
org_team: Tech Team Containerization
org_url: https://www.groupe-sncf.com
org_logo_filename: images/sncf.png
contact: Comtet Thomas, Blampey Florian, Guyaud Julien, Rotilio Yann
email: thomas.comtet@sncf.fr, florian.blampey@sncf.fr, julien.guyaud@sncf.fr, y.rotilio@sncf.fr
org_description: French Railway Operator.
org_size: "284,000+" # size of entire org
user_size: "150,000+"  # size of target userbase - could be internal team etc

industries:
- Transport
- Rail
- Software
- Cloud
tags: 
- cloud_native
- private_cloud
- kubernetes
- france
reference_architectures:
- Platform Engineering
---

## Relevant CNCF projects

{{< cardpane >}}
  {{< card header="ArgoCD" >}}
  [![argo logo](https://github.com/cncf/artwork/raw/main/projects/argo/horizontal/color/argo-horizontal-color.svg)](https://www.cncf.io/projects/argo/)
  - **Using since:** 2024
  - **Current version:** v3.3.6

  ArgoCD serves as our main infrastructure engine. We've configured it so it can manage day 1 and day 2 operations seamlessly : Cluster APIs primitives on the management cluster to ensure CP operations, and kubernetes deployment to ensure tooling and user clusters configuration.
  {{< /card >}}

  {{< card header="Cilium" >}}
  [![cilium logo](https://github.com/cncf/artwork/raw/main/projects/cilium/horizontal/color/cilium-horizontal-color.svg)](https://www.cncf.io/projects/cilium/)
  - **Using since:** 2024
  - **Current version:** v1.18.5

  Cilium is our CNI provider.
  {{< /card >}}

  {{< card header="Cluster API" >}}
  [![ClusterAPI logo](https://raw.githubusercontent.com/kubernetes-sigs/cluster-api/main/logos/kubernetes-cluster-logos_final-02.svg)](https://github.com/kubernetes-sigs/cluster-api/)
  - **Using since:** 2024
  - **Current version:** v1.18.5

  TODO: Cluster API's function.
  {{< /card >}}

  {{< card header="Envoy" >}}
  [![envoy logo](https://github.com/cncf/artwork/raw/main/projects/envoy/horizontal/color/envoy-horizontal-color.svg)](https://www.cncf.io/projects/envoy/)
  - **Using since:** 2024
  - **Current version:** v1.7.1

  Envoy is used as our Gateway API provider.
  {{< /card >}}

  {{< card header="External-dns" >}}
  [![External-secrets logo](https://raw.githubusercontent.com/kubernetes-sigs/external-dns/refs/heads/master/docs/img/external-dns.png)](https://github.com/kubernetes-sigs/external-dns/)
  - **Using since:** 2021
  - **Current version:** v

  TODO:External-dns 
  {{< /card >}}

  {{< card header="External Secrets Operator" >}}
  [![External-secrets logo](https://github.com/cncf/artwork/raw/main/projects/external-secrets-operator/horizontal/color/eso-horizontal-color.svg)](https://www.cncf.io/projects/external-secrets/)
  - **Using since:** 2022
  - **Current version:** v1.3.2

  TODO: External Secrets Operator 
  {{< /card >}}

  {{< card header="Harbor" >}}
  [![harbor logo](https://github.com/cncf/artwork/raw/main/projects/harbor/horizontal/color/harbor-horizontal-color.svg)](https://www.cncf.io/projects/harbor/)
  - **Using since:** 2021
  - **Current version:** v

  TODO: Harbor is our global registry.
  {{< /card >}}

  {{< card header="Kubernetes" >}}
  [![kubernetes logo](https://raw.githubusercontent.com/cncf/artwork/main/projects/kubernetes/icon/color/kubernetes-icon-color.svg)](https://www.cncf.io/projects/kubernetes/)
  - **Using since:** 2018
  - **Current version:** 1.35

  TODO: Kubernetes' function
  {{< /card >}}

  {{< card header="Kyverno" >}}
  [![kyverno logo](https://github.com/cncf/artwork/raw/main/projects/kyverno/horizontal/color/kyverno-horizontal-color.svg)](https://www.cncf.io/projects/kyverno/)
  - **Using since:** 2024
  - **Current version:** v1.13.4 (CNIP)

  TODO: Kyverno good.
  {{< /card >}}

  {{< card header="ORAS" >}}
  [![oras logo](https://github.com/cncf/artwork/raw/main/projects/oras/horizontal/color/oras-horizontal-color.svg)](https://www.cncf.io/projects/oras/)
  - **Using since:** 2024
  - **Current version:** v1.13.4 (CNIP)

   TODO: ORAS good.
  {{< /card >}}
{{< /cardpane >}}

## Describe your organisation

TODO

## Describe your entity and/or team

TODO

## Brief overview of your architecture and any potential goals you are trying to achieve with it?

The architecture explained below, is our OnPremise implementation of our Kubernetes deployment strategy.

### Goals

- Implement an easy and uniform way to consume and maintain Kubernetes across all our landing zones (private and public clouds).
- Have a centralized way to manage the lifecycle of our clusters and their components.
- Apply security and compliance policies across all clusters we are managing.
- Be able to scale manage lot of clusters with a small team.
- Be able to deploy clusters in a few minutes.
- Improve maintainability of our clusters.
- We wanted cloud native tools on premise.

## Can you expand on why you are using those projects/services?

CNCF projects and OpenSource are at the heart of our architecture:
- **Kubernetes (Talos)** *(Kubenetes : using since 2018, Talos : using since 2025)* : We use Kubernetes because it's awesome! Talos is an immutable OS to deploy Kubernetes.
- **Openstack to provide the infrastructure** *(using since 2025)* : OpenStack allow us to consume the infrastructure in a cloud native way.
- **ClusterAPI to rule them all** *(using since 2025)* : We use ClusterAPI to manage the lifecycle of our clusters. It also provides node autoscaling and node autoremediation in case of failure. It is compatible with Talos and Openstack.
- **ArgoCD to deploy clusters & components** *(using since 2023)* : We are using ArgoCD on all our clusters on private and public clouds. It allows us to manage the lifecycle of clusters infrastructure components.
- **Kyverno to enforce policies and mutate resources** *(using since 2022)* : Kyverno allow us to enforce policies like force the use of our private registry, force the usage of requests and limits, etc. It also allows us to mutate resources like auto add pod disruption budget or topology spread constraints, etc.
- **Cilium as CNI**  *(using since 2023)* :
- **Harbor as a private registry** *(using since 2020)* : Harbor is our private registry used to store OCI artifacts (like images, charts, etc.).

## What has worked well?

TODO

## What has not worked well?

TODO

## What sort of “glue” have you had to develop to enable usage of your architecture ?

TODO

## Has your architecture evolved? What lessons have you learned from previous iterations?

TODO

## What’s next for your architecture? What are you looking to do next?

TODO

## Discussion

End user members may participate in the [discussion thread](https://github.com/cncf/enduser-private/discussions/87) for this architecture.
