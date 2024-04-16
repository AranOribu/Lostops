# How it works

# Continuous Integration pipeline

When creating a merge request or pushing on main, all unit tests is launched to ensure that we doesn't get any regressions on this application.

The step are to setting up application on a docker container, then migrate changes and execute unit tests.

![Example of unit test when merging code.](images/ci.png)
[Pipeline available here](https://github.com/lostops-stg5/lostops-app/actions/runs/8686864446)

## Build pipeline

There are three steps when creating a release version (more information [here](https://docs.github.com/en/repositories/releasing-projects-on-github/managing-releases-in-a-repository)), you need to match a number version according to :

`<Major>.<Minor>.<Revision>`

The first one is the building of docker image version, annoted by tag latest and version number (example: 1.0.0). After that, this image will be pushed inside our artifact registry, [hosted by github](https://github.com/orgs/lostops-stg5/packages/container/package/lostops-app).

The second one is the security scanning of our recently built image, that indicate how many security issues with high or critical security are present. This result is sent inside artifacts. This part is not required to be successfull, because there will be many differents security issues.

The last one take care about connecting to remote server, and updating the version of our application by using docker.

![Example of unit test when merging code.](images/ci.png)
[Pipeline available here](https://github.com/lostops-stg5/lostops-app/actions/runs/8686574086)

# Tools used

![Github action icon](images/GithubActions-Dark.svg) Github action : used to orchestrate every ci/cd pipelines, and automate actions.

---

![Docker icon](images/docker.svg) Docker : used to isolate and simplify every setup action for our application.

---

![Trivy icon](images/trivy.svg) Trivy : security scanning for docker images.

---

![Ansible icon](images/Ansible_logo.svg) Ansible : connect to remote server using SSH and do automated scripts.

# Results

## Version 1.0.0 & 1.0.1

**Usefull links :**

[Link of the pipeline for 1.0.0](https://github.com/lostops-stg5/lostops-app/actions/runs/8601634689).
[Link of the pipeline for 1.0.1](https://github.com/lostops-stg5/lostops-app/actions/runs/8686574086).

After scanning theses versions, we found many differents docker image security issues :

- 16 CRITICAL security issues, mainly from apache and curl
- 162 HIGH security issues, and needs deep analysis about

## Version 1.0.2 and more

_Work in progress, will be released soon.._
