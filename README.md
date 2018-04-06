# Gitlab runner Stack

Creates an EC2, installs Docker, aws cli and a vanilla Gitlab runner for those builds not requiring Docker commands


> Read more about Gitlab runners <a href="https://docs.gitlab.com/ee/ci/runners/" target="_blank">here</a>

## Installing the runners
1. Run the `gitlabrunner-host.yml` with the parameters:
* `GitLabRegistrationToken` GitLab registration token from one of your repositories (repo -> Settings -> CI/CD -> Runner settings -> Registration token under specific runners).
* `GitlabServer` The Gitlab master to connect to. There is almost never a reason to change from the default value.
* `KeyName` A AWS keyname to be able to SSH to the host
* `RunnerName` The name of your runner to distinguish it from other runners. Suggestion; use your team name as runner name





    