# Dask on AWS ECS Workshop
This workshop will step you through the key aspects of building a containerised [Dask distributed](https://distributed.dask.org/en/latest/) environment on AWS and performing some data analysis tasks that would be difficult to perform on a single machine (at least, they would take a long time unless you have a very big machine!).

The solution you will deploy is based on [Amazon Elastic Container Service](https://aws.amazon.com/ecs/) (ECS), a fully managed container orchestration service that helps you easily deploy, manage and scale containerized applications.  The underlying compute will be provided through the [AWS Fargate](https://aws.amazon.com/fargate/) service, a serverless compute engine for containers that removes the need to provision and manage servers.

Once the environment is running, you will step through some large-scale data processing tasks on the [ERA5](https://registry.opendata.aws/ecmwf-era5/) climate reanalysis data set, hosted in [Amazon S3](https://aws.amazon.com/s3/) on the [AWS Open Data Registry](https://registry.opendata.aws), including:
 * Loading a ~200GB subset of the dataset into cluster memory 
 * Performing temperature conversion
 * Calculation and plotting of mean and standard deviation temperature for every point
 * Extraction of time-series temperature data for specific locations into a dataframe table

During the workshop you will:
1. Set up your cloud development environment using the [AWS Cloud9](https://aws.amazon.com/cloud9/) browser based development environment (IDE)
1. Create your customised Dask container image using [Docker](https://www.docker.com), and publish it to the [Amazon Elastic Container Registry](https://aws.amazon.com/ecr/) (ECR) service
1. Deploy the Dask environment using the provided [AWS CloudFormation](https://aws.amazon.com/cloudformation/) "infrastructure-as-code" template.  This template sets up the following services:
    * An [Amazon Virtual Private Cloud](https://aws.amazon.com/vpc/) network, with two subnets for the Dask scheduler and Dask worker tasks, as well as an Internet Gateway, NAT Gateway and S3 endpoint to facilitate connectivity with external resources
    * The Amazon ECS cluster with task definitions to run the Dask scheduler and worker containers
    * A managed Jupyter Notebook instance created via the [Amazon SageMaker](https://aws.amazon.com/sagemaker) service
1. Step through a [Jupyter Notebook](https://jupyter.org) that performs large scale data processing on the [ERA5](https://registry.opendata.aws/ecmwf-era5/) climate reanalysis data set, hosted in [Amazon S3](https://aws.amazon.com/s3/) on the [AWS Open Data Registry](https://registry.opendata.aws)

## Prerequisites
* Access to an AWS account, preferably with admin level privileges
* Familiarity with Linux, Docker containers and Python

## Workshop Labs Part 1 - Build a custom container image
The following labs are optional.  They will guide you through using Cloud9 and Docker to create a customised Dask container image, which will be uploaded to the Amazon Elastic Container Registry ready for deployment.  A public image is provided if you'd prefer to skip these steps and proceed straight to [Lab 3 - Create the Dask ECS environment](workshop-03.md).

### [Lab 1 - Setup your cloud development environment](workshop-01.md)

### [Lab 2 - Build your customised Dask container image](workshop-02.md)


## Workshop Labs Part 2 - Deploy Dask and perform analysis
This is where the fun starts - deploy the Dask into an AWS VPC running on the Amazon Elastic Container Service and Fargate, then use an Amazon SageMaker Notebook to submit data analysis jobs to your cluster.
### [Lab 3 - Create the Dask ECS environment](workshop-03.md)

### [Lab 4 - Process data using the SageMaker Notebook](workshop-04.md)

## Workshop Cleanup
### [Clean up - Delete all resources](workshop-05.md)

## Architecture
The workshop is based on the Dask ECS environment as shown in the diagram below.
![architecture](cloudformation/dask-architecture.png)

For the purposes of the workshop some of the steps will be performed manually, to help you understand some of the moving parts in more detail.
