<h1 align="center">AWS CodePipeline to Publish to AWS SAR</h1>

[![Quality Gate Status](https://sonarcloud.io/api/project_badges/measure?project=xavier-thomas_aws-sar-publish-codepipeline&metric=alert_status)](https://sonarcloud.io/dashboard?id=xavier-thomas_aws-sar-publish-codepipeline)
![Tests](https://github.com/xavier-thomas/aws-sar-publish-codepipeline/workflows/Tests/badge.svg)

<p align="center">
    <a href="#overview">Overview</a> |
	<a href="#instructions">Instructions</a> |
  	<a href="#authors">Authors</a> |
  	<a href="#licence">Licence</a>
</p>

## Overview

This repository contains an AWS Cloudformation template to create an AWS CodePipeline which can be used to publish to AWS Serverless Application Repository. This pipeline is generic and can be used for to publish any SAR application.


```bash

│   buildspec.yml                   <-- Build configuration to lint and test Cloudformation
│   CHANGELOG.MD                    <-- Changelog
│   Pipfile                         <-- Pipenv Config (https://github.com/pypa/pipenv)
│   README.md                       <-- This File
│   example-publish-buildspec.yml   <-- EXAMPLE Buildspec. Copy to the repository that holds your SAR App.
|
└───codepipeline
        pre-requisites.yaml         <-- Pre-requisites for the pipelines. Needs to be Manually deployed first.
        sar-publish-pipeline.yaml   <-- Pipeline to publish application into AWS SAR
```


## Instructions

1. From the AWS Console / CLI deploy the **[pre-requisites.yaml](./codepipeline/pre-requisites.yaml)**
   This sets up the S3 bucket used to hold the pipeline artefacts and also the application artefact which should be uploaded to the Serverless Application Repository
   * **Note: This only needs to be done once per AWS Account, per Region. All subsequent pipelines are set up to use the same artefact bucket and parameter**
2. Pass in the Following Parameters.
	- `GitHubOAuthToken`        <-- This is your GitHub token which is stored in AWS SSM Parameter Store and read by the pipeline
3. From the AWS Console / CLI deploy the **[sar-publish-pipeline.yaml](./codepipeline/sar-publish-pipeline.yaml)**
4. Pass in the following Parameters
	- Repository Settings
		- `RepoOwner`           <-- The Owner of the GitHub Repository. i.e. Your Github Organization ID / User ID.
		- `RepoName`            <-- The Name of the GitHub Repository.
		- `SourceBranch`        <-- The branch to deploy from.
	- Build Settings
		- `EnableWebhooks`      <-- Enable webhook to automatically run the pipeline on commit push. Disable to run pipeline manually.
		- `BuildSpecPath`       <-- Path to the buildspec file for CodeBuild. Defaults to `buildspec.yml` in the repo root.
		                            The **[example-publish-buildspec.yml](./example-publish-buildspec.yml)** can be used as a template for the buildspec in your repo.
	- Parameter Store References (Do Not Change!)
		- `GitHubTokenSSMParam` <-- Leave this to default of `/github/rw/id`. Used to read the value from Parameter Store.
5. The Check the CodePipeline to ensure that it's set up and running. A quick link to the pipeline can be found in the CloudFormation Stack outputs.


## Authors
**[Xavier Thomas](https://github.com/xavier-thomas)**

## Licence
**[3-Clause BSD](./LICENCE)**
