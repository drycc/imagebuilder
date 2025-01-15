# Drycc imagebuilder v3
[![Build Status](https://woodpecker.drycc.cc/api/badges/drycc/imagebuilder/status.svg)](https://woodpecker.drycc.cc/drycc/imagebuilder)

Drycc (pronounced DAY-iss) Workflow is an open source Platform as a Service (PaaS) that adds a developer-friendly layer to any [Kubernetes](http://kubernetes.io) cluster, making it easy to deploy and manage applications on your own servers.

For more information about the Drycc Workflow, please visit the main project page at https://github.com/drycc/workflow.

We welcome your input! If you have feedback, please [submit an issue][issues]. If you'd like to participate in development, please read the "Development" section below and [submit a pull request][prs].

# Build config

The V3 version of imagebuilder unifies the building model, uses the latest CNCF [buildpack](https://github.com/buildpacks) building program, and also supports the dockerfile format.

You can use `DRYCC_STACK` specifies the construction mode. Currently, you can choose two construction formats: `container` and `buildpack`.

## Build arg config

In Container Build, build arguments (ARG) a means to pass information into the build process. You can use them to parameterize the build, allowing for more flexible and configurable builds.

It can be configured through `.build-arg`, argument=value to supply to the builder, this configuration file is universal in both container and buildpack scenarios.

## Container config

Normally, in container mode, as long as there is a Dockerfile in the root directory, it is sufficient, but we can use [drycc config path](https://www.drycc.cc/docs/applications/using-dryccpath/) to configure the build process more finely.

## Buildpack config

Add an empty `.clean_cache` file, clear image's associated cache before building.

## Development

The Drycc project welcomes contributions from all developers. The high level process for development matches many other open source projects. See below for an outline.

* Fork this repository
* Make your changes
* [Submit a pull request][prs] (PR) to this repository with your changes, and unit tests whenever possible.
  * If your PR fixes any [issues][issues], make sure you write Fixes #1234 in your PR description (where #1234 is the number of the issue you're closing)
* The Drycc core contributors will review your code. After each of them sign off on your code, they'll label your PR with LGTM1 and LGTM2 (respectively). Once that happens, the contributors will merge it

[issues]: https://github.com/drycc/imagebuilder/issues
[prs]: https://github.com/drycc/imagebuilder/pulls
[s3-api]: http://docs.aws.amazon.com/AmazonS3/latest/API/APIRest.html
