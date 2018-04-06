# Gitlab runner Stack

Creates an EC2, installs Docker, aws cli and the following Gitlab runners:
1. Docker, to build Docker images (uses dind)
2. Docker, to be able to run Docker commands
3. Generic, for those builds not requiring Docker commands
4. Cache, for possibility to cache e.g. npm packages.

> Read more about Gitlab runners <a href="https://docs.gitlab.com/ee/ci/runners/" target="_blank">here</a>

## Installing the runners
1. Run the `gitlabrunner-access.yml` to setup the correct access for the runner host
2. Run the `gitlabrunner-host.yml` with the parameters:
* `GitLabRegistrationToken` GitLab registration token from one of your repositories (repo -> Settings -> CI/CD -> Runner settings -> Registration token under specific runners).
* `GitlabServer` The Gitlab master to connect to. There is almost never a reason to change from the default value.
* `KeyName` A AWS keyname to be able to SSH to the host
* `RunnerName` The name of your runner to distinguish it from other runners. Suggestion; use your team name as runner name




    