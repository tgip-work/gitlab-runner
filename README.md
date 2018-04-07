# Gitlab runner host

Creates an EC2, installs Docker, aws cli and a vanilla Gitlab runner for CI/CD builds. Option to install other runner types for e.g. Docker and Docker in Docker.


> <a href="https://docs.gitlab.com/ee/ci/runners" target="_blank">Read more about Gitlab runners here.</a>

## Installing the runner
Click [![Launch Stack](https://cdn.rawgit.com/buildkite/cloudformation-launch-stack-button-svg/master/launch-stack.svg)](https://console.aws.amazon.com/cloudformation/home#/stacks/new?stackName=gitlab-runner&amp;templateURL=https://s3-eu-west-1.amazonaws.com/scaniadevtools-aws-templates/gitlabrunner-host.yml/gitlabrunner-host.yml) 

You can also upload the file `gitlabrunner-host.yml` in the AWS Cloudformation console of the AWS account where you want to have the runner.

