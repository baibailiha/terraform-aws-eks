# Change Log

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](http://keepachangelog.com/) and this
project adheres to [Semantic Versioning](http://semver.org/).

## [[v1.1.0](https://github.com/terraform-aws-modules/terraform-aws-eks/compare/v1.0.0...v1.1.0)] - 2018-06-25]

### Added

- new variable `worker_sg_ingress_from_port` allows to change the minimum port number from which pods will accept communication (Thanks, @ilyasotkov 👏).
- expanded on worker example to show how multiple worker autoscaling groups can be created.
- IPv4 is used explicitly to resolve testing from IPv6 networks (thanks, @tsub 🙏).
- Configurable public IP attachment and ssh keys for worker groups. Defaults defined in `worker_group_defaults`. Nice, @hatemosphere 🌂
- `worker_iam_role_name` now an output. Sweet, @artursmet 🕶️

### Changed

- IAM test role repaired by @lcharkiewicz 💅
- `kube-proxy` restart no longer needed in userdata. Good catch, @hatemosphere 🔥
- worker ASG reattachment wasn't possible when using `name`. Moved to `name_prefix` to allow recreation of resources. Kudos again, @hatemosphere 🐧

## [[v1.0.0](https://github.com/terraform-aws-modules/terraform-aws-eks/compare/v0.2.0...v1.0.0)] - 2018-06-11]

### Added

- security group id can be provided for either/both of the cluster and the workers. If not provided, security groups will be created with sufficient rules to allow cluster-worker communication. - kudos to @tanmng on the idea ⭐
- outputs of security group ids and worker ASG arns added for working with these resources outside the module.

### Changed

- Worker build out refactored to allow multiple autoscaling groups each having differing specs. If none are given, a single ASG is created with a set of sane defaults - big thanks to @kppullin 🥨

## [[v0.2.0](https://github.com/terraform-aws-modules/terraform-aws-eks/compare/v0.1.1...v0.2.0)] - 2018-06-08]

### Added

- ability to specify extra userdata code to execute following kubelet services start.
- EBS optimization used whenever possible for the given instance type.
- When `configure_kubectl_session` is set to true the current shell will be configured to talk to the kubernetes cluster using config files output from the module.

### Changed

- files rendered from dedicated templates to separate out raw code and config from `hcl`
- `workers_ami_id` is now made optional. If not specified, the module will source the latest AWS supported EKS AMI instead.

## [[v0.1.1](https://github.com/terraform-aws-modules/terraform-aws-eks/compare/v0.1.0...v0.1.1)] - 2018-06-07]

### Changed

- Pre-commit hooks fixed and working.
- Made progress on CI, advancing the build to the final `kitchen test` stage before failing.

## [v0.1.0] - 2018-06-07

### Added

- Everything! Initial release of the module.
- added a local variable to do a lookup against for a dynamic value in userdata which was previously static. Kudos to @tanmng for finding and fixing bug #1!
