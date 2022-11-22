# F5-XC-VIRTUAL-SITE
This repository consists of Terraform templates to bring up a F5XC Virtual Site.

## Usage

- Clone this repo with: `git clone --recurse-submodules https://github.com/cklewar/f5-xc-virtual-site`
- Enter repository directory with: `cd f5-xc-virtual-site`
- Obtain F5XC API certificate file from Console and save it to `cert` directory
- Pick and choose from below examples and add mandatory input data and copy data into file `main.tf.example`.
- Rename file __main.tf.example__ to __main.tf__ with: `rename main.tf.example main.tf`
- Initialize with: `terraform init`
- Apply with: `terraform apply -auto-approve` or destroy with: `terraform destroy -auto-approve`

## Virtual site module usage example

````hcl
variable "project_prefix" {
  type        = string
  description = "prefix string put in front of string"
  default     = "f5xc"
}

variable "project_suffix" {
  type        = string
  description = "prefix string put at the end of string"
  default     = "01"
}

variable "f5xc_api_p12_file" {
  type = string
}

variable "f5xc_api_url" {
  type = string
}

variable "f5xc_tenant" {
  type = string
}

module "f5xc_virtual_site" {
  source                 = "./modules/f5xc/site/virtual"
  f5xc_namespace         = "system"
  f5xc_tenant            = var.f5xc_tenant
  f5xc_virtual_site_name = format("%s-virtual-site-%s", var.project_prefix, var.project_suffix)
  f5xc_virtual_site_type = "CUSTOMER_EDGE"
}
````