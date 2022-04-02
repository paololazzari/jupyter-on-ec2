# jupyter-on-ec2

This repository contains a simple CloudFormation template that sets up a Jupyter Notebook environment on an EC2 Amazon Linux 2 instance, which you can access over the public internet.

# Requirements

You need to have the following configured in your AWS account:

- The subnet in which you deploy must auto-assign public IPv4 addresses
- The route associated to the subnet must have a route to an internet gateway

# Usage

## Deployment

You can launch the template directly with the following button:

[![alt text](https://s3.amazonaws.com/cloudformation-examples/cloudformation-launch-stack.png "Launch template on AWS")](https://us-east-1.console.aws.amazon.com/cloudformation/home?region=us-east-1#/stacks/create/review?templateURL=https://jupyter-on-ec2.s3.amazonaws.com/jupyter-notebook-on-ec2.yml)

<details><summary>... or use the CLI</summary>
<p>

```bash
$ export IP_ADDRESS=...
$ export JUPYTER_PASSWORD...
$ export VPC=...
$ export SUBNET=...
$ export SSHKEYNAME=...
$ aws cloudformation create-stack --stack-name jupyter-on-ec2 --template-url=https://jupyter-on-ec2.s3.amazonaws.com/jupyter-notebook-on-ec2.yml --parameters ParameterKey=MyIPAddress,ParameterValue=$IP_ADDRESS ParameterKey=JupyterPassword,ParameterValue=$JUPYTER_PASSWORD ParameterKey=VPC,ParameterValue=$VPC ParameterKey=Subnet,ParameterValue=$SUBNET ParameterKey=SSHKeyName,ParameterValue=$SSHKEYNAME --region us-east-1
```
</p>
</details>


## Accessing Jupyter Notebook

As soon as the CloudFormation template has finished deployment you can access Jupyter Notebook. To do so, follow these steps:


<details>
<summary>1. Retrieve the public dns of the instance from the outputs section</summary>

![output](https://user-images.githubusercontent.com/6552810/162047704-318f94bb-938a-451a-a542-dc95d57867e5.png)

</details>

<details>
<summary>2. Accept the self signed certificate warning</summary>

![self-signed-cert-warning](https://user-images.githubusercontent.com/6552810/162047731-9e8dd4ec-cb8d-4958-9ffe-5ab0393c5812.png)

</details>

<details>
<summary>3. Enter your password at the Jupyter Notebook login page</summary>

![jupyter-login](https://user-images.githubusercontent.com/6552810/162047761-8b4bd85e-565e-49cf-b39b-2d4012528aec.png)

</details>

<details>
<summary>4. Use Jupyter Notebook</summary>

![jupyter-notebook](https://user-images.githubusercontent.com/6552810/162047775-ff044393-859c-4679-8f32-e2d29c66daec.png)

</details>



# How it works

The CloudFormation template creates an EC2 instance that runs nginx in reverse-proxy mode, as well as jupyter notebook.
