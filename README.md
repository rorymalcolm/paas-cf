# paas-release-ci

This repository contains the scripts and Terraform configurations required to set up a Concourse pipeline for building Bosh releases. Releases each have their own repository and are stored in an S3 bucket when they are built.

## Requirements

* A running Concourse instance. Currently we use [paas-bootstrap](https://github.com/alphagov/paas-bootstrap) to set up an environment, which contains instructions in its README.

## Setup

* Run `make <env> pipelines`
* Visit your running Concourse instance in a browser and trigger the `setup` pipeline.

A pipeline should be created for each Bosh release this repository is currently building releases for. The `build-dev-release` jobs should trigger when pull requests are raised against the Bosh release's repository. The `build-final-release` job should trigger when new commits are added to the branch used to build final releases.

You can override some variables to customise the deployment:
 * `BRANCH` current branch to pull and use. e.g. `BRANCH=$(git rev-parse --abbrev-ref HEAD)`
 * `CONCOURSE_URL`, `CONCOURSE_ATC_PASSWORD`: to point to a different concourse with the given credentials.
 * `STATE_BUCKET_NAME`, `RELEASES_BUCKET_NAME`: use alternative state and releases buckets.

