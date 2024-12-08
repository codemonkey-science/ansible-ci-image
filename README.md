# ansible-ci-image

[![Build and Push Docker Image](https://github.com/codemonkey-science/ansible-ci-image/actions/workflows/build-and-push.yaml/badge.svg)](https://github.com/codemonkey-science/ansible-ci-image/actions/workflows/build-and-push.yaml)

Container image used for Ansible-based GitHub Actions. Without this image, every time you run an Ansible job, it takes a bit to install and update software. Instead, this has:

1. An updated OS.
2. Python3 and `pip` installed and updated.
3. Ansible installed.

So, if you start from this image, you can get right to the business of running your playbooks.

## Getting Started

To use this base image, in your `.github/workflows/` workflow, specify this image something like this:

```yaml
jobs:
  run-playbook:
    runs-on: self-hosted
    container:
      image: ghcr.io/codemonkey-science/ansible-ci-image:latest
```

Since this is a public container image, you won't need to log in.
