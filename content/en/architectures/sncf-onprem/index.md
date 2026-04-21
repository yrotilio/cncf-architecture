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
- sovereignty
reference_architectures:
- platform
---

## Relevant projects

{{< cardpane >}}
  {{< card header="ArgoCD" >}}
  [![argo logo](https://github.com/cncf/artwork/raw/main/projects/argo/horizontal/color/argo-horizontal-color.svg)](https://www.cncf.io/projects/argo/)
  - **Using since:** 2024
  - **Current version:** v3.3.6

  ArgoCD serves as our main infrastructure engine. We've configured it so it can manage day 1 and day 2 operations seamlessly : Cluster APIs primitives on the management cluster to ensure CP operations, and kubernetes deployment to ensure tooling and user clusters configuration.
  {{< /card >}}

  {{< card header="Cluster API" >}}
  [![ClusterAPI logo](https://raw.githubusercontent.com/kubernetes-sigs/cluster-api/main/logos/kubernetes-cluster-logos_final-02.svg)](https://github.com/kubernetes-sigs/cluster-api/)
  - **Using since:** 2024
  - **Current version:** v1.18.5

  Cluster API manages K8s control planes & machines at scale leaning on the adhoc infrastucture providers (CAPO for Openstack and CACPPT for Talos), and serves as autoscaling & autohealing provider.
  {{< /card >}}

  {{< card header="External-dns" >}}
  [![External-secrets logo](https://raw.githubusercontent.com/kubernetes-sigs/external-dns/refs/heads/master/docs/img/external-dns.png)](https://github.com/kubernetes-sigs/external-dns/)
  - **Using since:** 2021
  - **Current version:** v

  External-dns automates Designate records management for users Clusters.
  {{< /card >}}

  {{< card header="External Secrets Operator" >}}
  [![External-secrets logo](https://github.com/cncf/artwork/raw/main/projects/external-secrets-operator/horizontal/color/eso-horizontal-color.svg)](https://www.cncf.io/projects/external-secrets/)
  - **Using since:** 2022
  - **Current version:** v1.3.2

  External Secrets Operator is the glue between Hashicorp Vault and Users clusters, managing pull secrets and so on
  {{< /card >}}

  {{< card header="Harbor" >}}
  [![harbor logo](https://github.com/cncf/artwork/raw/main/projects/harbor/horizontal/color/harbor-horizontal-color.svg)](https://www.cncf.io/projects/harbor/)
  - **Using since:** 2021
  - **Current version:** v

  Harbor is the central registry storing and distributings all the images used on container based infrastructures @ SNCF.
  {{< /card >}}

  {{< card header="Kubernetes" >}}
  [![kubernetes logo](https://raw.githubusercontent.com/cncf/artwork/main/projects/kubernetes/icon/color/kubernetes-icon-color.svg)](https://www.cncf.io/projects/kubernetes/)
  - **Using since:** 2018
  - **Current version:** 1.35.x

  Kubernetes is the sole container orchestrator deployed in all SNCF's hosting zones.
  {{< /card >}}

  {{< card header="OpenStack" >}}
  [![openstack logo](https://raw.githubusercontent.com/openstack/openstackdocstheme/refs/heads/master/openstackdocstheme/theme/openstackdocs/static/images/openstack-logo-full.svg)](https://opendev.org/openstack/openstack/)
  - **Using since:** 2024
  - **Current version:** ???

  OpenStack provides Machines, DNS, storage and network to the platform, it is automated by CAPO.
  {{< /card >}}

  {{< card header="ORAS" >}}
  [![oras logo](https://github.com/cncf/artwork/raw/main/projects/oras/horizontal/color/oras-horizontal-color.svg)](https://www.cncf.io/projects/oras/)
  - **Using since:** 2024
  - **Current version:** ???

  ORAS is used to manage CAPI providers as OCI artifacts, enabling argocd to manage the lifecycle of said providers.
  {{< /card >}}

  {{< card header="Renovate" >}}
  [![renovate logo](https://github.com/renovatebot/renovate/blob/main/docs/usage/assets/images/logo.png)](https://github.com/renovatebot/renovate/)
  - **Using since:** 2024
  - **Current version:** ???

  Renovate automates OS patch management.
  {{< /card >}}

  {{< card header="Talos Linux" >}}
  [![talos logo](https://raw.githubusercontent.com/siderolabs/docs/refs/heads/main/public/talos/v1.13/images/logo.svg)](https://github.com/siderolabs/talos/)
  - **Using since:** 2024
  - **Current version:** ???

  Talos Linux provides an immutable OS and K8s control plane provider combo.
  {{< /card >}}
{{< /cardpane >}}

## TLDR; Synopsis

This reference architecture describes SNCF's second internal On Premise Kubernetes Platform, built upon a bare metal open source OpenStack Infrastructure to provide at scale Container orchestration and scheduling. 
It has revolutionized hosting options for the organization's applications, successfully providing a public cloud managed kubernetes service equivalent to internal teams. This platform allows them to build a sovereign strategy in coherence to the applications' requirements.

In particular, this architecture targets:
* A layer by layer explanation on how the platform was designed for end-to-end automation for all its components

## Organization

SNCF is the publicly owned french rail operator, in charge of every layer of the rail transportation idiom except actually building trains. It encompasses thousands of differents trades, resulting in needing thousands of different software applications operated mostly by one IT departement.

The company decided in the late 2010s to move massively to the public cloud, giving birth to a containers platform team leaning on public cloud managed kubernetes services to create a hosting solution for container compatible applications.
In 2023, that massive public cloud move was mainly wrapped up, the Kubernetes platform entering a growth sustainability phase, with at scale management problematics enforcing GitOps adoption. These stabilization efforts soon highlighted the need to offer the same level of service for container compatible applications not elligible for public cloud migrations, in order to prevent the organization to vendor lock itself with a lopsided two-tier system.

This was addressed by a joined initiative between a private cloud provider built on premises and an end-to-end automated kubernetes platform build on top of it.

## Teams

* Private Cloud Infrastructure - 
* Cloud Native Integration - 

## Architecture

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
