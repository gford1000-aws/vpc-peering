# VPC Peering

AWS CloudFormation scripts that show different VPC Peering approaches

## 1. [Simple VPC Peering](https://github.com/gford1000-aws/vpc-peering/blob/master/vpc-peering-example.cform)

In this example, two VPCs containing private subnets are peered together.  The VPCs are assumed to be created using the script in [VPC](https://github.com/gford1000-aws/vpc), taking the default values in that script.

The script creates the following:

![alt text](https://github.com/gford1000-aws/vpc-peering/blob/master/Simple%20peering%20between%20VPCs.png "Script per designer")

Notes:

* The two VPCs must have different CIDR blocks


## Arguments

| Argument           | Description                                               |
| ------------------ |:---------------------------------------------------------:|
| CidrAddressVPC1    | The initial X.Y of the CIDR X.Y.0.0/16 for the first VPC  |
| CidrAddressVPC2    | The initial X.Y of the CIDR X.Y.0.0/16 for the second VPC |
| VPCPeeringRole     | The value for the Role tag in the VPC Peering             |
| VPCTemplateURL     | The S3 url to the VPC Cloudformation script               |


## Outputs

| Output           | Description                        |
| ---------------- |:----------------------------------:|
| VPC1             | The resource id of the first VPC   |
| VPC2             | The resource id of the second VPC  |

## Licence

This project is released under the MIT license. See [LICENSE](LICENSE) for details.
