# Deployment of a single FortiGate-VM on the Oracle Cloud Infrastructure (OCI)
## Introduction
A Terraform script to deploy a FortiGate-VM HA Cluster on OCI with 3 ports setup

## Requirements
* [Terraform](https://learn.hashicorp.com/terraform/getting-started/install.html) >= 1.0.9
* Terraform Provider OCI >= 4.50
* Terraform Provider Template >= 2.2.0
* A [OCI API key](https://docs.cloud.oracle.com/en-us/iaas/Content/API/Concepts/apisigningkey.htm)

## Deployment overview
Terraform deploys the following components:
   - A Virtual Cloud Network (VPC) with two public subnets
   - A VCN with one private subnets
   - Two FortiGate-VM instances with 3 NICs.  hamgmt/sync, untrust, and trust 
   - Four firewall rules: one for external, one for internal, one for sync/HA management.

## Deployment
To deploy the FortiGate-VMs to OCI:
1. Clone the repository.
2. Move the OCI API key and FortiGate-VM license file to the same folder
3. Customize variables in the `terraform.tfvars.example` and `variables.tf` file as needed.  And rename `terraform.tfvars.example` to `terraform.tfvars`.
4. Initialize the providers and modules:
   ```sh
   $ cd XXXXX
   $ terraform init
    ```
5. Submit the Terraform plan:
   ```sh
   $ terraform plan
   ```
6. Verify output.
7. Confirm and apply the plan:
   ```sh
   $ terraform apply
   ```
8. If output is satisfactory, type `yes`.

Output will include the information necessary to log in to the FortiGate-VM instances:
```sh
ClusterPublicIP = <FGT Public IP>
Default_Password = [
  "<FGT Password>",
]
Default_Username = admin
FGTActiveMGMTPublicIP = [
  "<FGT Active Public IP>",
]
FGTPassiveMGMTPublicIP = [
  "<FGT Passive Public IP>",
]
```
*After deployment, FortiGate-VM instances may not get the proper configurations during the initial bootstrap configuration. 
User may need to do a manual factoryreset on the units in order to get proper configurations.  To do a factoryreset, user can
login to the units via Console, and do `exec factoryreset` on each of the units*

## Destroy the instance
To destroy the instance, use the command:
```sh
$ terraform destroy
```

# Support
Fortinet-provided scripts in this and other GitHub projects do not fall under the regular Fortinet technical support scope and are not supported by FortiCare Support Services.
For direct issues, please refer to the [Issues](https://github.com/fortinet/fortigate-terraform-deploy/issues) tab of this GitHub project.
For other questions related to this project, contact [github@fortinet.com](mailto:github@fortinet.com).

## License
[License](https://github.com/fortinet/fortigate-terraform-deploy/blob/master/LICENSE) © Fortinet Technologies. All rights reserved.

Marketplace Catalog for mp_listing_id in variables.tf
BYOL 7.2.3: ocid1.image.oc1..aaaaaaaatgr6fgvzztpmmb2tuka55uasrviedqfnksbbwscj3nvhhcxiglba

Marketplace Image for mp_listing_resource_id in variables.tf
PAGY 7.2.3 2ocpu: ocid1.image.oc1..aaaaaaaa2ufmdc65fcfgwa7totfdb3ary4xwrwyoprodb5bqz2fxmqpxozda
PAYG 7.2.3 4ocup: ocid1.image.oc1..aaaaaaaa4d4x7cmgq4yimk6eg3kydwelpuctbxracvqcqktgza7zpmujan2a
PAYG 7.2.3 8ocup: ocid1.image.oc1..aaaaaaaar3qypkpwertilhsqwdm3pqywd5va66pxncexmpkkvdoq256h7z6q
PAYG 7.2.3 24ocup: ocid1.image.oc1..aaaaaaaaksmo2becayfqiutbkjqmquxcdg2rvrqcmise2ow4qmqylzcfjwta
