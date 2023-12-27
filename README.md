# Terraform module template

[![](https://img.shields.io/badge/github-ggrptr/terraform--module--template-%233DA639.svg)](https://github.com/ggrptr/terraform-module-template "github.com/ggrptr/terraform-module-template")
[![License](https://img.shields.io/badge/license-MIT-%233DA639.svg)](https://opensource.org/licenses/MIT)

A template project for kickstarting a [Terraform](https://www.terraform.io/) module, with testing, validation and security checks.

All the tools used in this template run in [Docker](https://www.docker.com/) containers, to avoid having to install or configure them locally. 

The tools used are:
- [Terraform](https://www.terraform.io)
- [TFLint](https://github.com/terraform-linters/tflint)
- [Terraform-docs](https://terraform-docs.io)
- [Checkov](https://www.checkov.io)

All the tools have a Makefile target to run them in a Docker container, and also configured as 
pre-commit hooks, so the checks will run automatically when you commit your changes.

## Usage

### Manual execution
You can clone this repository and use it as a starting point for your module, and use make targets for your 
terraform development workflow:

```bash
make terraform init
make terraform plan
make terraform apply
...
```

If you want to run command in a subdirectory (examples, tests, etc), you have to cd into the directory and give the
location of the Makefile:
```bash
make -f ../Makefile terraform init
```

#### AWS credentials
The Makefile targets will use the AWS credentials from the host environment, so you have to set them before running 
the commands that require AWS access. These variables are used:
- AWS_ACCESS_KEY_ID
- AWS_SECRET_ACCESS_KEY
- AWS_SESSION_TOKEN
- AWS_REGION

### Pre-commit hooks

The project contains a pre-commit configuration file (.pre-commit-config.yaml), 
that will run the checks automatically when you commit your changes.

### Installation of pre-commit hooks
For this to work, you have to install the pre-commit tool on your host (it isn't containerised yet),
and the pre-commit hooks in the repository.

Installing pre-commit on Ubuntu:
```bash
sudo apt install pre-commit
```

Installing pre-commit hooks (in your project folder, you have to do in after every git clone):
```bash
pre-commit install --hook-type pre-commit --hook-type commit-msg --overwrite --install-hooks
```
The above is not so intuitive, because the default pre-commit install command only installs the pre-commit hook,
which isn't enough for the commit-msg hook to work.

### Configured hooks
It the pre-commit configuration is correct, the following hooks will run automatically when you commit your changes.
If any of the checks fail, the commit will be aborted.
If the hooks change any files, the commit will be aborted, and you have to stage modified files, and commit again.

#### Conventional pre commit
Checks if your commit message follows the [conventional commit](https://www.conventionalcommits.org/en/v1.0.0/) format.

#### Terraform init
Initialises the terraform project, installs the required providers and modules.

#### Terraform validate
Validates the terraform code, checks for syntax errors.

#### Tflint
Checks for errors in the terraform code with the [TFLint](https://github.com/terraform-linters/tflint) tool.

#### Checkov
Checks for security issues in the terraform code with the [Checkov](https://www.checkov.io) tool.

#### Terraform docs
Generates documentation for the terraform module with the [terraform-docs](https://terraform-docs.io) tool.
It writes the documentation to the README.md file, between the BEGIN_TF_DOCS and END_TF_DOCS comments, like below:

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

**[MIT License](https://opensource.org/licenses/MIT)**

Copyright (c) 2023 [ggrptr](https://github.com/ggrptr)