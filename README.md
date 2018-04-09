# Gitlab runner host

<a href="https://console.aws.amazon.com/cloudformation/home#/stacks/new?stackName=gitlab-runner&amp;templateURL=https://s3-eu-west-1.amazonaws.com/scaniadevtools-aws-templates/gitlabrunner-host.yml" target="_blank"><img src="https://cdn.rawgit.com/buildkite/cloudformation-launch-stack-button-svg/master/launch-stack.svg"></a>

![Gitlab](https://github.com/scaniadevtools/architecture.png "Architecture")

This repo contains a Cloudformation template that creates an EC2 Ubuntu machine, installs Docker, AWS CLI and four Gitlab runners on it. The runners have the following tags:

**vanilla** - A generic runner that can be used for builds not requiring Docker. This runner can pick up untagged builds as well as jobs tagged with "vanilla".

**docker** - A runner for builds requiring Docker commands. Jobs need to be tagged with "docker" to be picked up by this runner.

**dind** - A Docker-in-Docker runner for builds making Docker images (i.e. `docker build` command). Jobs need to be tagged with "dind" to be picked up by this runner.

**cache** - A runner for builds where you want artifacts to be cached between builds, e.g. npm packages. The packages will be cached on the runner host.  Jobs need to be tagged with "cache" to be picked up by this runner.

> <a href="https://docs.gitlab.com/ee/ci/runners" target="_blank">Read more about Gitlab runners here.</a>

An AWS role, policy and instance-profile that allows the Gitlab runner to assume other roles will be created. This is useful for builds that create AWS resources, e.g. deploying Cloudformation templates, which require AWS permissions to work. 
> <a href="https://docs.aws.amazon.com/STS/latest/APIReference/API_AssumeRole.html" target="_blank">Read more about assuming roles in AWS here.</a>

The runner host will be deployed to a security group allowing Internet access and option to do remote login to the host using SSH. 
> <a href="https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/authorizing-access-to-an-instance.html" target="_blank">Read more about remote login here.</a>

## Installing the runner

### Before you start

To deploy the Gitlab runner template you need to have the following ready:

- An AWS account
- An  account on the Gitlab server you want to connect the runner to. Could be [gitlab.com](https://gitlab.com/) or an enterprise Gitlab server.
- A Gitlab project on the Gitlab server. If you want to hit the ground running deploying AWS resources using this Gitlab runner you can fork the <a href="https://gitlab.com/scaniadevtools/gitlab-samples/HelloWorld-CF" target="_blank">HelloWorld-CF</a>. 


You should also collect the following information to provide as parameters during the deployment process:

- The AWS VPC id where you want to deploy the runner. (<a href="https://console.aws.amazon.com/vpc" target="_blank">Check your VPCs and subnets</a>)
- The Subnet Id of a subnet with Internet access in the VPC. 
- If you want to be able to log in remotely using SSH for e.g. debugging you need:
  - An AWS key pair name (<a href="https://console.aws.amazon.com/ec2/v2/home#KeyPairs:sort=keyName" target="_blank">AWS Keys</a>)

  - The CIDR block you want to be able to remotely SSH login from. E.g. if you want to login with SSH from your current IP adress and it is `123.234.111.222` then enter `123.234.111.222/32` as CIDR.
    Your current IP adress can be found <a href="http://checkip.amazonaws.com/" target="_blank">here.</a>

    > **If you don't need SSH login you can ignore both AWS key pair name and CIDR.**
- The Gitlab server URL the runner should connect to. Defaults to https://gitlab.com. 
> If you are connecting to your organization's Gitlab Enterprise server use that Gitlab's URL. Make sure your runner host is allowed to connect to that server. Talk to your Gitlab enterprise system administration before you deploy this template.
- The Gitlab project registration token to connect the runner to the project.
  From your Gitlab project navigate to *Settings -> CI/CD -> Runner settings -> Registration token* under Specific runners.
  > <a href="https://docs.gitlab.com/ee/ci/runners/#registering-a-specific-runner-with-a-project-registration-token" target="_blank">Read more about registering runners here.</a> 


### Setup and install

#### Using the AWS console

Click  <a href="https://console.aws.amazon.com/cloudformation/home#/stacks/new?stackName=gitlab-runner&amp;templateURL=https://s3-eu-west-1.amazonaws.com/scaniadevtools-aws-templates/gitlabrunner-host.yml" target="_blank"><img src="https://cdn.rawgit.com/buildkite/cloudformation-launch-stack-button-svg/master/launch-stack.svg"></a> 


You can also upload the file `gitlabrunner-host.yml` in the AWS Cloudformation console of the AWS account where you want to deploy the runner. (<a href="https://eu-west-1.console.aws.amazon.com/cloudformation/home#/stacks/new" target="_blank">Click to open AWS Cloudformation console</a>)

Then follow the Cloudformation console instructions.

#### Using AWS CLI

Coming soon.