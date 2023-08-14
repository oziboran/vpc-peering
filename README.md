# AWS VPC, Subnets, NAT Gateways, and VPC Peering Setup

This repository provides CloudFormation templates and instructions to create an AWS Virtual Private Cloud (VPC) with public and private subnets, NAT Gateways, and establish VPC peering connections. The templates are designed to help you quickly set up a networking environment within the AWS cloud.

## Prerequisites

Before you begin, make sure you have the following:

- An AWS account
- AWS Command Line Interface (CLI) or AWS Management Console access
- Familiarity with basic AWS concepts, including VPC, subnets, and CloudFormation

## How to Use

Follow these steps to create and set up your networking environment:

1. **Clone the Repository:**
   Clone or download this repository to your local machine.

2. **Deploy the VPC Stack:**
   - Access the AWS Management Console.
   - Navigate to the CloudFormation service.
   - Click on "Create stack" and select "With new resources (standard)".
   - Upload the `vpc-with-subnets.yaml` template from the repository.
   - Provide the required parameters, such as VPC CIDR block and subnet configurations.
   - Continue through the wizard, reviewing and confirming the settings.
   - Once the stack creation is complete, you'll find the VPC ID, public subnet IDs, and private subnet IDs in the stack outputs.

3. **Deploy the VPC Peering Stack:**
   - Access the AWS Management Console.
   - Navigate to the CloudFormation service.
   - Click on "Create stack" and select "With new resources (standard)".
   - Upload the `vpc-peering.yaml` template from the repository.
   - Provide the following parameters:
     - `VpcId1`: ID of the first VPC created in the previous step.
     - `VpcId2`: ID of the second VPC to establish peering with.
     - `SubnetId1`: ID of a subnet in the first VPC.
     - `SubnetId2`: ID of a subnet in the second VPC.
   - Continue through the wizard, reviewing and confirming the settings.
   - Once the stack creation is complete, you'll find the VPC Peering Connection ID in the stack outputs.

4. **Testing the Peering Connection:**
   - Test communication between instances in the peered VPCs. Resources in each VPC can communicate using private IP addresses as if they were part of the same network.

## Cleanup

After testing, remember to delete the CloudFormation stacks to avoid incurring unnecessary charges:

1. Delete the VPC Peering Stack:
   ```bash
   aws cloudformation delete-stack --stack-name MyVpcPeeringStack
