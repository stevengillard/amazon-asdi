# Lab 3: Build the dask infrastructure
In this lab, we will spin up the infrastructure resources necessary to run our dask container in distributed mode.  This includes:
 * A [Virtual Private Cloud](https://aws.amazon.com/vpc/) (VPC) with a single public and private subnet
 * [Internet Gateway](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Internet_Gateway.html), [NAT Gateway](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-nat-gateway.html) and [S3 gateway endpoint](https://docs.aws.amazon.com/vpc/latest/privatelink/vpce-gateway.html) resources to facilitate connectivity in and out of the VPC
 * [Security Groups](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_SecurityGroups.html) (a virtual firewall) with ingress rules to control traffic
 * An [Elastic Container Service](https://aws.amazon.com/ecs/) cluster
 * [Task definitions](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/task_definitions.html) for the dask scheduler and dask workers
 * A [SageMaker Notebook instance](https://docs.aws.amazon.com/sagemaker/latest/dg/nbi.html), connected to the VPC

We'll use a CloudFormation template to deploy these resources, as setting everything up through the AWS console will be time consuming and error-prone - using an infrastructure as code tool is a much better approach!

The CloudFormation template can be found [here](cloudformation/dask-environment.yaml) if you wish to review the contents.

## Deploy the CloudFormation template
We'll use the AWS console to deploy the template, but it can be done via the CLI if you prefer.

1. Navigate to the AWS CloudFormation page in the AWS console (or click [here](https://console.aws.amazon.com/cloudformation/home))

    ![CloudFormation](workshop/0301-CloudFormation.png)

1. Click **Create Stack** and select **with new resources**

    ![CreateStack](workshop/0302-CloudFormationCreate.png)

1. Select **Template is ready** and **Upload a template file**

1. Navigate to the location of the [dask-environment.yaml](cloudformation/dask-environment.yaml) file and select it (you may need to download the file to your computer first - either from github or if you are in Cloud9 simply right click and select **Download**).  The file will be uploaded to S3 automatically, and the location will appear.  Click **Next** when ready.

    ![SelectTemplate](workshop/0303-CloudFormationCreate2.png)

1. Enter a name for the stack.  Optionally change the `DaskImage` parameter value to your custom image URI (if you created one in the previous lab).  

   Alternatively you can leave the default `DaskImage` value, which is a pre-built public image stored in Amazon ECR `public.ecr.aws/j7x5r0l2/aws-dask-workshop:latest` Click **Next** when ready. 

   Examine the other parameter values but there is no need to change them - you may accept the defaults.

    ![Parameters](workshop/0304-CloudFormationParameters.png)

1. There is nothing to change on the **Stack Options** screen - click **Next** again

1. On the **Review** screen double check all of the parameter values, and click the checkbox to acknowledge that CloudFormation will create IAM resources, then click **Create Stack**

    ![CreateStack](workshop/0305-CloudFormationCreate3.png)

1. Monitor the stack creation events and wait until the stack enters the **CREATE_COMPLETE** state.  This will take around 10 minutes.

    ![StackComplete](workshop/0305-CloudFormationComplete.png)

## Check your dask services in the AWS ECS console
Once the CloudFormation stack has finished deployment, you can take a closer look at the container definitions, which are defined as services within Amazon Elastic Container Service (ECS).

1. Navigate to the Elastic Container Service in the AWS console, or click here: https://console.aws.amazon.com/ecs/home?region=us-east-1#

    ![ECS](workshop/0306-ECS.png)

1. You should see your cluster, with two services and a single task running (the `dask-scheduler`)

    ![ECSCluster](workshop/0307-ECSCluster.png)

1. Click on the cluster name to view more details about the services and tasks that are running.  At this stage there are no workers running, because we aren't ready for them yet.  We'll start them from within our notebook when we're ready to do some actual processing - otherwise they'll be running with nothing to do, costing money.

    ![ECSClusterServices](workshop/0308-ECSCluster2.png)

## Congratulations!
It's time to start using your dask environment!  Head to [lab 4](workshop-04.md) to begin.