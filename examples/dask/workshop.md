# Dask on AWS ECS Workshop
## Introduction
This workshop will step you through the key aspects of building a containerised dask environment on AWS. 

The solution you will deploy is based on the [Amazon Elastic Container Service](https://aws.amazon.com/ecs/) (ECS), a fully managed container orchestration service that helps you easily deploy, manage and scale containerized applications.

During the workshop you will:
1. Set up your cloud development environment using the [AWS Cloud9](https://aws.amazon.com/cloud9/) IDE
1. Create your customised dask container image using Docker, and publish it to the [Amazon Elastic Container Registry](https://aws.amazon.com/ecr/) (ECR) service
1. Deploy the dask environment using the provided [AWS CloudFormation](https://aws.amazon.com/cloudformation/) "infrastructure-as-code" template.  This template sets up the following services:
    * An [Amazon Virtual Private Cloud](https://aws.amazon.com/vpc/) network, with two subnets for the dask scheduler and dask worker tasks, as well as an Internet Gateway, NAT Gateway and S3 endpoint to facilitate connectivity with external resources
    * The Amazon ECS cluster with task definitions to run the dask scheduler and worker containers
    * A managed Jupyter Notebook instance created via the [Amazon SageMaker](https://aws.amazon.com/sagemaker) service
1. Step through a Jupyter Notebook that performs large scale data processing on the [ERA5](https://registry.opendata.aws/ecmwf-era5/) climate reanalysis data set, hosted in [Amazon S3](https://aws.amazon.com/s3/) on the [AWS Open Data Registry](https://registry.opendata.aws)

## Prerequisites
* Access to an AWS account, preferably with admin level privileges
* Familiarity with Linux, containers and Python

## Architecture
The workshop is based on the dask ECS environment as shown in the diagram below.
![architecture](cloudformation/dask-architecture.png)

For the purposes of the workshop some of the steps will be performed manually, to help you understand some of the moving parts in more detail.

## Workshop labs

[Lab 1 - Setup your cloud development environment](workshop-01.md)

[Lab 2 - Build your customised dask container image](workshop-02.md)

[Lab 3 - Create the dask ECS environment](workshop-03.md)

[Lab 4 - Process data using the SageMaker Notebook](workshop-04.md)