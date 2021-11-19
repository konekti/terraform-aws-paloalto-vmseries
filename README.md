<<<<<<< HEAD
<!-- BEGIN_TF_DOCS -->
# Creating modules for AWS I&A Organization

This repo template is used to seed Terraform Module templates for the [AWS I&A GitHub organization](https://github.com/aws-ia). Usage of this template is allowed per included license. PRs to this template will be considered but are not guaranteed to be included. Consider creating an issue to discuss a feature you want to include before taking the time to create a PR.
### TL;DR

1. [install pre-commit](https://pre-commit.com/)
2. configure pre-commit: `pre-commit install`
3. install required tools
    - [tflint](https://github.com/terraform-linters/tflint)
    - [tfsec](https://aquasecurity.github.io/tfsec/v1.0.11/)
    - [terraform-docs](https://github.com/terraform-docs/terraform-docs)
    - [golang](https://go.dev/doc/install) (for macos you can use `brew`)
    - [coreutils](https://www.gnu.org/software/coreutils/)

Write code according to [I&A module standards](https://aws-ia.github.io/standards-terraform/)

## Module Documentation

**Do not manually update README.md**. `terraform-docs` is used to generate README files. For any instructions an content, please update [.header.md](./.header.md) then simply run `terraform-docs ./` or allow the `pre-commit` to do so.

## Terratest

Please include tests to validate your examples/<> root modules, at a minimum. This can be accomplished with usually only slight modifications to the [boilerplate test provided in this template](./test/examples\_basic\_test.go)

### Configure and run Terratest

1. Install

    [golang](https://go.dev/doc/install) (for macos you can use `brew`)
2. Change directory into the test folder.
    
    `cd test`
3. Initialize your test
    
    go mod init github.com/[github org]/[repository]

    `go mod init github.com/aws-ia/terraform-aws-vpc`
4. Run tidy

    `git mod tidy`
5. Install Terratest

    `go get github.com/gruntwork-io/terratest/modules/terraform`
6. Run test (You can have multiple test files).
    - Run all tests

        `go test`
    - Run a specific test with a timeout

        `go test -run examples_basic_test.go -timeout 45m`
## Module Standards

For best practices and information on developing with Terraform, see the [I&A Module Standards](https://aws-ia.github.io/standards-terraform/)

## Continuous Integration

The I&A team uses AWS CodeBuild to perform continuous integration (CI) within the organization. Our CI uses the a repo's `.pre-commit-config.yaml` file as well as some other checks. All PRs with other CI will be rejected. See our [FAQ](https://aws-ia.github.io/standards-terraform/faq/#are-modules-protected-by-ci-automation) for more details.

=======
# Palo Alto Networks VM-Series Module for AWS

A Terraform module for deploying a VM-Series firewall in AWS cloud.

## Usage

```hcl
module "vpc" {
  source           = "../../modules/vpc"
  
  global_tags      = var.global_tags
  prefix_name_tag  = var.prefix_name_tag
  vpc              = var.vpcs
  vpc_route_tables = var.route_tables
  subnets          = var.vpc_subnets
  security_groups  = var.security_groups
}

module "vmseries" {
  source              = "../../modules/vmseries/"

  region              = var.region
  prefix_name_tag     = var.prefix_name_tag
  ssh_key_name        = var.ssh_key_name
  fw_license_type     = var.fw_license_type
  fw_version          = var.fw_version
  fw_instance_type    = var.fw_instance_type
  tags                = var.global_tags
  firewalls           = var.firewalls
  interfaces          = var.interfaces
  subnets_map         = module.vpc.subnet_ids
  security_groups_map = module.vpc.security_group_ids
}
```

<!-- BEGINNING OF PRE-COMMIT-TERRAFORM DOCS HOOK -->
>>>>>>> 3e2c781 (docs: enhance modules documentation (#94))
## Requirements

| Name | Version |
|------|---------|
<<<<<<< HEAD
| <a name="requirement_terraform"></a> [terraform](#requirement\_terraform) | >= 0.14.0 |
| <a name="requirement_aws"></a> [aws](#requirement\_aws) | >= 3.72.0 |
| <a name="requirement_awscc"></a> [awscc](#requirement\_awscc) | >= 0.11.0 |

## Providers

No providers.
=======
| <a name="requirement_terraform"></a> [terraform](#requirement\_terraform) | >=0.12.29, <0.14 |
| <a name="requirement_aws"></a> [aws](#requirement\_aws) | ~> 3.10 |

## Providers

| Name | Version |
|------|---------|
| <a name="provider_aws"></a> [aws](#provider\_aws) | ~> 3.10 |
>>>>>>> 3e2c781 (docs: enhance modules documentation (#94))

## Modules

No modules.

## Resources

<<<<<<< HEAD
No resources.

## Inputs

No inputs.

## Outputs

No outputs.
<!-- END_TF_DOCS -->
=======
| Name | Type |
|------|------|
| [aws_eip.this](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/eip) | resource |
| [aws_eip_association.this](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/eip_association) | resource |
| [aws_instance.pa_vm_series](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/instance) | resource |
| [aws_network_interface.this](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/network_interface) | resource |
| [aws_network_interface_attachment.this](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/network_interface_attachment) | resource |
| [aws_route.to_eni](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/route) | resource |
| [aws_ami.pa_vm](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/data-sources/ami) | data source |

## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|:--------:|
| <a name="input_addtional_interfaces"></a> [addtional\_interfaces](#input\_addtional\_interfaces) | Map additional interfaces after initial EC2 deployment. | `map(any)` | `{}` | no |
| <a name="input_buckets_map"></a> [buckets\_map](#input\_buckets\_map) | Map of S3 Bucket name to ID, can be passed from remote state output or data source.<br><br>Example:<pre>buckets_map = {<br>  "bootstrap_bucket1 = {<br>     arn = "arn:aws-us-gov:s3:::bootstrap_bucket1<br>     name = "bootstrap_bucket1"<br>  }<br>  "bootstrap_bucket2 = {<br>     arn = "arn:aws-us-gov:s3:::bootstrap_bucket2<br>     name = "bootstrap_bucket2"<br>  }<br>}</pre> | `map(any)` | `{}` | no |
| <a name="input_firewalls"></a> [firewalls](#input\_firewalls) | Map of VM-Series Firewalls to create with interface mappings.<br><br>Required: `name`, `interfaces` (a map of names and indexes).<br><br>Example:<pre>firewalls = [{<br>  name = "ingress-fw1"<br>  bootstrap_options = {<br>    mgmt-interface-swap = "disable" # Change to "enable" for interface swap<br>  }<br>  interfaces = [{<br>    name  = "ingress-fw1-mgmt"<br>    index = "0"<br>    },<br>    {<br>      name  = "ingress-fw1-untrust"<br>      index = "1"<br>    },<br>    {<br>      name  = "ingress-fw1-trust"<br>      index = "2"<br>  }]<br>}]</pre> | `any` | n/a | yes |
| <a name="input_fw_instance_type"></a> [fw\_instance\_type](#input\_fw\_instance\_type) | EC2 Instance Type. | `string` | `"m5.xlarge"` | no |
| <a name="input_fw_license_type"></a> [fw\_license\_type](#input\_fw\_license\_type) | Select the VM-Series Firewall license type - available options: `byol`, `payg1`, `payg2`. | `string` | `"byol"` | no |
| <a name="input_fw_license_type_map"></a> [fw\_license\_type\_map](#input\_fw\_license\_type\_map) | Map of the VM-Series Firewall licence types and corresponding VM-Series Firewall Amazon Machine Image (AMI) ID.<br>The key is the licence type, and the value is the VM-Series Firewall AMI ID." | `map(string)` | <pre>{<br>  "byol": "6njl1pau431dv1qxipg63mvah",<br>  "payg1": "6kxdw3bbmdeda3o6i1ggqt4km",<br>  "payg2": "806j2of0qy5osgjjixq9gqc6g"<br>}</pre> | no |
| <a name="input_fw_version"></a> [fw\_version](#input\_fw\_version) | Select which VM-Series Firewall version to deploy.<br><br>Example:<pre>#default = "9.1.0"<br>#default = "8.1.9"<br>#default = "8.1.0"</pre> | `string` | `"9.0.6"` | no |
| <a name="input_interfaces"></a> [interfaces](#input\_interfaces) | Map of interfaces to create with optional parameters.<br><br>Required: name, subnet\_name, security\_group<br>Optional: `eip_name`, `source_dest_check`.<br><br>Example:<pre>interfaces = [<br>  {<br>    name              = "ingress-fw1-mgmt"<br>    eip_name          = "ingress-fw1-mgmt-eip"<br>    source_dest_check = true<br>    subnet_name       = "ingress-mgmt-subnet-az1"<br>    security_group    = "sg-123456789"<br>  },<br>  {<br>    name              = "ingress-fw1-trust"<br>    source_dest_check = false<br>    subnet_name       = "ingress-trust-subnet-az1"<br>    security_group    = "sg-123456789"<br>}]</pre> | `any` | n/a | yes |
| <a name="input_prefix_name_tag"></a> [prefix\_name\_tag](#input\_prefix\_name\_tag) | Prefix used to build name tags for resources. | `string` | `""` | no |
| <a name="input_region"></a> [region](#input\_region) | AWS Region | `any` | n/a | yes |
| <a name="input_route_tables_map"></a> [route\_tables\_map](#input\_route\_tables\_map) | Map of Route Tables Name to ID, can be passed from remote state output or data source. | `map(any)` | `{}` | no |
| <a name="input_rts_to_fw_eni"></a> [rts\_to\_fw\_eni](#input\_rts\_to\_fw\_eni) | Map of RTs from base\_infra output and the FW ENI to map default route to. | `map(any)` | `{}` | no |
| <a name="input_security_groups_map"></a> [security\_groups\_map](#input\_security\_groups\_map) | Map of security group name to ID, can be passed from remote state output or data source.<br><br>Example:<pre>security_groups_map = {<br>  "panorama-mgmt-inbound-sg" = "sg-0e1234567890"<br>  "panorama-mgmt-outbound-sg" = "sg-0e1234567890"<br>}</pre> | `map(any)` | `{}` | no |
| <a name="input_ssh_key_name"></a> [ssh\_key\_name](#input\_ssh\_key\_name) | Name of AWS keypair to associate with instances. | `string` | `""` | no |
| <a name="input_subnets_map"></a> [subnets\_map](#input\_subnets\_map) | Map of subnet name to ID, can be passed from remote state output or data source.<br><br>Example:<pre>subnets_map = {<br>  "panorama-mgmt-1a" = "subnet-0e1234567890"<br>  "panorama-mgmt-1b" = "subnet-0e1234567890"<br>}</pre> | `map(any)` | `{}` | no |
| <a name="input_tags"></a> [tags](#input\_tags) | Map of additional tags to apply to all resources. | `map(any)` | `{}` | no |

## Outputs

| Name | Description |
|------|-------------|
| <a name="output_firewalls"></a> [firewalls](#output\_firewalls) | n/a |
<!-- END OF PRE-COMMIT-TERRAFORM DOCS HOOK -->
>>>>>>> 3e2c781 (docs: enhance modules documentation (#94))
