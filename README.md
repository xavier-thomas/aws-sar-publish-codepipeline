<p align="center">
	<img alt="AWS CodePipeline to Publish to AWS SAR" title="AWS CodePipeline to Publish to AWS SAR" src="./assets/logo.png" width="128">
</p>

<h1 align="center">AWS CodePipeline to Publish to AWS SAR</h1>

<p align="center">
    <a href="#overview">Overview</a> |
  	<a href="#repository-structure">Repository Structure</a> |
	<a href="#instructions">Instructions</a> |
  	<a href="#authors">Authors</a> |
  	<a href="#licence">Licence</a>
</p>

## Overview

This repository contains an AWS Cloudformation template to create an AWS CodePipeline which can be used to publish to AWS Serverless Application Repository.


```bash

│   buildspec.yml                   <-- Build configuration to lint and test Cloudformation
│   CHANGELOG.MD					<-- Changelog
│   Pipfile							<-- Pipenv Config (https://github.com/pypa/pipenv)
│   README.md                       <-- This File
│
└───codepipeline
        pre-requisites.yaml         <-- Pre-requisites for the pipelines. Needs to be Manually deployed first.
        sar-publish-pipeline.yaml   <-- Pipeline to publish application into AWS SAR
```


## Instructions

1. From the AWS Console / CLI deploy the **[pre-requisites.yaml](./codepipeline/pre-requisites.yaml)**
   This sets up the S3 bucket used to hold the pipeline artefacts and also the application artefact which should be uploaded to the Serverless Application Repository
2. Pass in the Following Parameters.
	- GitHubOAuthToken     <-- This is your GitHub token which is stored in AWS SSM Parameter Store and read by the pipeline
2. From the AWS Console / CLI deploy the **[sar-publish-pipeline.yaml](./codepipeline/sar-publish-pipeline.yaml)**
3. Pass in the following Parameters
	- 


## Authors
**[Xavier Thomas](https://github.com/xavier-thomas)**

## Licence
**[3-Clause BSD](./LICENCE)**
