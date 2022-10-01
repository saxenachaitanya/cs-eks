# tEKS

<p align="center">
  <img src="images/logo.png">
</p>

[![teks](https://github.com/particuleio/teks/actions/workflows/terraform.yml/badge.svg)](https://github.com/particuleio/teks/actions/workflows/terraform.yml)
[![teks:mkdocs](https://github.com/particuleio/teks/actions/workflows/mkdocs.yml/badge.svg)](https://github.com/particuleio/teks/actions/workflows/mkdocs.yml)
[![semantic-release](https://img.shields.io/badge/%20%20%F0%9F%93%A6%F0%9F%9A%80-semantic--release-e10079.svg)](https://github.com/semantic-release/semantic-release)
[![FOSSA Status](https://app.fossa.com/api/projects/git%2Bgithub.com%2Fparticuleio%2Fteks.svg?type=shield)](https://app.fossa.com/projects/git%2Bgithub.com%2Fparticuleio%2Fteks?ref=badge_shield)

<!-- vim-markdown-toc GFM -->

* [Terraform/Terragrunt](#terraformterragrunt)
* [Requirements](#requirements)
  * [Terragrunt](#terragrunt)
* [Main purposes](#main-purposes)
* [What you get](#what-you-get)
* [Curated Features](#curated-features)
  * [Enforced security](#enforced-security)
  * [Out of the box monitoring](#out-of-the-box-monitoring)
  * [Helm v3 provider](#helm-v3-provider)
  * [Other and not limited to](#other-and-not-limited-to)
* [Requirements](#requirements-1)
* [Examples](#examples)
* [Additional infrastructure blocks](#additional-infrastructure-blocks)
* [Branches](#branches)
* [License](#license)

<!-- vim-markdown-toc -->

tEKS is a set of Terraform / Terragrunt modules designed to get you everything
you need to run a production EKS cluster on AWS. It ships with sensible
defaults, and add a lot of common addons with their configurations that work out
of the box.

:warning: the v5 and further version of this project have been completely revamp
and now offer a skeleton to use as a base for your infrastructure projects
around EKS. All the modules have been moved outside this repository and get
their own versioning. The [old README is accessible
here](https://github.com/particuleio/teks/tree/release-4.X)

:warning: Terraform implementation will not be maintained anymore because of
time, and mostly because it has become quite difficult to get feature parity
with Terragrunt. [Archive branch is available here](https://github.com/particuleio/teks/tree/archive/terraform)

## Terraform/Terragrunt

* Terragrunt implementation is available in the [`terragrunt`](./terragrunt) folder.

## Requirements

### Terragrunt

* [Terraform](https://www.terraform.io/downloads.html)
* [Terragrunt](https://github.com/gruntwork-io/terragrunt/releases)

## Main purposes

The main goal of this project is to glue together commonly used tooling with Kubernetes/EKS and to get from an AWS Account to a production cluster with everything you need without any manual configuration.

## What you get

A production cluster all defined in IaaC with Terraform/Terragrunt:

* AWS VPC if needed based on [`terraform-aws-vpc`](https://github.com/terraform-aws-modules/terraform-aws-vpc)
* EKS cluster base on [`terraform-aws-eks`](https://github.com/terraform-aws-modules/terraform-aws-eks)
* Kubernetes addons based on [`terraform-kubernetes-addons`](https://github.com/particuleio/terraform-kubernetes-addons): provides various addons that are often used on Kubernetes and specifically on EKS.

Everything is tied together with Terragrunt and allows you to deploy a multi
cluster architecture in a matter of minutes (ok maybe an hour) and different AWS
accounts for different environments.

## Curated Features

The main additionals features are the curated addons list, see
[here](https://github.com/particuleio/terraform-kubernetes-addons) and in the
customization of the cluster policy

### Enforced security

* No IAM credentials on instances, everything is enforced with [IRSA](https://aws.amazon.com/blogs/opensource/introducing-fine-grained-iam-roles-service-accounts/)
* Each addons is deployed in it's own namespace with sensible default network policies.
* Calico Tigera Operator for network policy

### Out of the box monitoring

* Prometheus Operator with defaults dashboards
* Addons that support metrics are enable along with their `serviceMonitor`
* Custom grafana dashboard are available by default.

### Helm v3 provider

* All addons support Helm v3 configuration
* All charts are easily customizable

### Other and not limited to

* priorityClasses for addons
* use of [`kubectl-provider`], no more local exec and custom manifest are properly handled
* lot of manual stuff have been automated under the hood

## Requirements

Terragrunt is not a hard requirement but all the modules are tested with Terragrunt.

* [Terraform](https://www.terraform.io/intro/getting-started/install.html)
* [Terragrunt](https://github.com/gruntwork-io/terragrunt#install-terragrunt)
* [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/)
* [helm](https://helm.sh/)

## Examples

[`terragrunt/live`](terragrunt/live) folder provides an opinionated directory structure for a production environment with an example using

## Additional infrastructure blocks

If you wish to extend your infrastructure you can pick up additional modules on the [particuleio github page](https://github.com/particuleio).
Some modules can also be found on the [clusterfrak-dynamics github page](https://github.com/clusterfrak-dynamics).

## Branches

* [`main`](https://github.com/particuleio/teks/tree/main): Backward incompatible with v1.X but compatible with v2.X, releases bumped to v3.X because a lot has changed.
* [`release-1.X`](https://github.com/particuleio/teks/tree/release-1.X): Compatible with Terraform < 0.12 and Terragrunt < 0.19. Be sure to target the same modules version.
* [`release-2.X`](https://github.com/particuleio/teks/tree/release-2.X): Compatible with Terraform >= 0.12 and Terragrunt >= 0.19. Be sure to target the same modules version.

## License

[![FOSSA Status](https://app.fossa.io/api/projects/git%2Bgithub.com%2Fparticuleio%2Fteks.svg?type=large)](https://app.fossa.io/projects/git%2Bgithub.com%2Fparticuleio%2Fteks?ref=badge_large)
