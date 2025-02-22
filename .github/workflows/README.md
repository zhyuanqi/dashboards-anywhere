# OS/OSD GitHub Action Guide

## Summary

This document provides the guidance for the usage of GitHub actions.

The current workflows folder contains one deployment workflow(os-osd-deployment.yml) and two reusable workflows(deployment-template.yml and functional-test-template.yml). os-osd-deployment workflow will call deployment-template and functional-test-template with required inputs and secrets for the deployment and tests.

- os-osd-deployment.yml
- deployment-template.yml
- functional-test-template.yml
- trigger-build-osd-image.yml

## Prerequisites

- GitHub account
- Public repository
- GitHub action workflows


## Detail workflows

> os-osd-deployment.yml: 
>> This is a mainly deployment workflow for OpenSearch and OpenSearch Dashboards, it includes dev and prod two environment. 

> deployment-template.yml:
>> This is a reusable workflow for deployment. It requires couple inputs and secrets. The list of required inputs and secrets.
>> - inputs: helm-repo, it is offical helm release location of OpenSearch and OpenSearch Dashboards.
>> - inputs: deploy-env, it is the variable for environment, like as dev or prod.
>> - secrets: access-key-id, it is access id for EKS cluster.
>> - secrets: secret-access-key, it is access key for EKS cluster.
>> - secrets: region, it is cluster region.
>> - secrets: kube-config, it is client kube configuration which was used to connect to EKS cluster.

> functional-test-template.yml:
>> This is a reusable functional test workflows for OpeanSearch Dashboards. The required inputs and secrets as following:
>> - inputs: endpoint, the OpenSearch Dashboard endpoint.
>> - secrets: osd-user, the write access user of OpenSearch Dashboards.
>> - secrets: osd-user-password, the write access user's password for OpenSearch Dashboards.

> trigger-build-osd-image.yml:
>> This GitHub Actions workflow triggers the OSD Build Image Workflow. It is triggered manually using the `workflow_dispatch` event and accepts several input parameters:
>> - `python_version`: The Python version to use for the build. Default value is `'3.9.17'`.
>> - `node_version`: The Node.js version to use for the build. Default value is `'18.19.0'`.
>> - `osd_version`: The OpenSearch Dashboards version to use for the build. Default value is `'3.0.0'`.
>> - `additional_args`: JSON string of additional options for the build. Default value is `'{}'`.
>> - `build_number`: The build number. This parameter is optional.

## Appendix

- GitHub workflow: https://docs.github.com/en/actions/using-workflows/about-workflows

- Reusable workflow : https://docs.github.com/en/actions/using-workflows/reusing-workflows
