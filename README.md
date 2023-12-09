# Terraform module template

[![](https://img.shields.io/badge/github-ggrptr/terraform--module--template-%233DA639.svg)](https://github.com/ggrptr/terraform-module-template "github.com/ggrptr/terraform-module-template")
[![License](https://img.shields.io/badge/license-MIT-%233DA639.svg)](https://opensource.org/licenses/MIT)

A template project for kickstarting a [Terraform](https://www.terraform.io/) module, with testing, validation and security checks.

All the tools used in this template run in [Docker](https://www.docker.com/) containers, to avoid having to install or configure them locally. 

### _Documentation coming soon_

Example module documentation:

<!-- BEGIN_TF_DOCS -->
## Requirements

| Name | Version |
|------|---------|
| <a name="requirement_terraform"></a> [terraform](#requirement\_terraform) | >= 0.16.0 |
| <a name="requirement_aws"></a> [aws](#requirement\_aws) | 5.26.0 |

## Providers

| Name | Version |
|------|---------|
| <a name="provider_aws"></a> [aws](#provider\_aws) | 5.26.0 |

## Modules

| Name | Source | Version |
|------|--------|---------|
| <a name="module_label_aws_s3_bucket_example"></a> [label\_aws\_s3\_bucket\_example](#module\_label\_aws\_s3\_bucket\_example) | git::https://github.com/cloudposse/terraform-null-label | 488ab91e34a24a86957e397d9f7262ec5925586a |

## Resources

| Name | Type |
|------|------|
| [aws_s3_bucket.example](https://registry.terraform.io/providers/hashicorp/aws/5.26.0/docs/resources/s3_bucket) | resource |

## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|:--------:|
| <a name="input_context"></a> [context](#input\_context) | Object wrapper for the context map of the null label module. See the null label module for more information. | <pre>object({<br>    enabled             = optional(bool, true)<br>    namespace           = optional(string, null)<br>    tenant              = optional(string, null)<br>    environment         = optional(string, null)<br>    stage               = optional(string, null)<br>    name                = optional(string, null)<br>    delimiter           = optional(string, null)<br>    attributes          = optional(list(string), [])<br>    tags                = optional(map(string), {})<br>    additional_tag_map  = optional(map(string), {})<br>    regex_replace_chars = optional(string, null)<br>    label_order         = optional(list(string), [])<br>    id_length_limit     = optional(number, null)<br>    label_key_case      = optional(string, null)<br>    label_value_case    = optional(string, null)<br>    descriptor_formats  = optional(map(string), {})<br>    labels_as_tags      = optional(list(string), ["unset"])<br>  })</pre> | n/a | yes |

## Outputs

No outputs.
<!-- END_TF_DOCS -->