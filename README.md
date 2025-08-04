# Ansible AWX Execution Environment with GCP, Kubernetes and Helm 

## Table of contents

* [What is it?](#what-is-it)
* [Versioning](#versioning)
* [AWX configuration](#awx-configuration)
* [Installation details](#installation-details)
* [Troubleshooting](#troubleshooting)
    * [Job is not using the correct execution environment](#job-is-not-using-the-correct-execution-environment)
* [Please contribute!](#please-contribute)

-----

<a name="what-is-it"></a>

## What is it?

This project contains the configuration of an Ansible AWX Execution Environment container image with commonly used libraries.

It is based on the official Ansible AWX EE image and mainly includes:

* Cloud provider dependencies:

    * Google Cloud Platform (GCP)

* Kubernetes & Helm

<a name="versioning"></a>

## Versioning

The versioning of this project follows the one of the official Ansible AWX EE containers.

* If based on an existing AWX EE tag, the release will be the same as the EE one.
* If based on the latest EE tag, the release will have a `-SNAPSHOT` suffix to indicate the changing nature of the parent.

<a name="awx-configuration"></a>

## AWX configuration

This image can be set up in AWX by:

1. Navigating to AWX > `Administration` > `Execution Environments`
2. Adding a new Execution Environment with the following details:

    * Name: `Custom AWX Execution Environment`
    * Image: `docker.io/PRAVALER/awx-ee-gcp:latest`
    * Pull policy: `Only pull if not present before running`

3. Applying the execution environment on the relevant job templates.

<a name="installation-details"></a>

## Installation details

In addition to using this image for AWX's execution environment, remember to define the list of Ansible Galaxy packages your project relies on in `/collections/requirements.yml`. That file has the following format:

    ---
    # Official documentation:
    # https://docs.ansible.com/ansible/devel/user_guide/collections_using.html
    
    collections:
    - collection1
    - collection2

In this example, `collection1` and `collection2` must of course be replaced by one of the values listed below.

Depending on your needs, the following collections are supported and can be added to the above file:

* Cloud providers:

    * [GCP](https://galaxy.ansible.com/google/cloud): `google.cloud`
* [General](https://galaxy.ansible.com/community/general): `community.general`
* [Kubernetes](https://galaxy.ansible.com/kubernetes/core): `kubernetes.core`

<a name="troubleshooting"></a>

## Troubleshooting

<a name="job-is-not-using-the-correct-execution-environment"></a>

### Job is not using the correct execution environment

Upon running a job, errors might appear which seem to be pointing to missing dependencies.

This is a common misconfiguration, remember to make sure your job templates are using the correct execution environment.
