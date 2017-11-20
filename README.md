# serverless-plugin-cicd
[![serverless](http://public.serverless.com/badges/v3.svg)](http://www.serverless.com)
[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)
[![npm version](https://badge.fury.io/js/serverless-plugin-cicd.svg)](https://badge.fury.io/js/serverless-plugin-cicd)

Serverless plugin for creating a CI/CD pipeline that watches a GitHub repo.

# About The Black Tux
The Black Tux is reinventing the formalwear rental industry so guys can show up at their best on the days that matter most. The company designs and manufactures modern rental suits and tuxedos that actually fit—made of 100% wool, ordered online or in one of our showrooms, and delivered for free. Using a combination of machine learning, tailor-trained fit specialists, and industry-leading customer service, The Black Tux guarantees a perfect fit every time.

To support this elevated customer experience we rely on lots of technology. From time to time we release things we build to the open source community when we feel they might be useful by others as well, and of course don't include anything proprietary.

# Getting Started

## Prerequisites
Make sure you have the following installed before starting:
* [nodejs](https://nodejs.org/en/download/)
* [npm](https://www.npmjs.com/get-npm)
* [serverless](https://serverless.com/framework/docs/providers/aws/guide/installation/)

## Installation
First install the package:

```
npm install serverless-plugin-cicd --save
```

Then add the plugin to your `serverless.yml` file:
```yaml
plugins:
  - serverless-plugin-cicd
```

There are a number of parameters that you then can use:
```yaml
custom:
  cicd:
    image: 'the aws codebuild image'
    branch: 'the git branch you want to watch'
    owner: 'the GitHub repository owner where your project can be found'
    repository: 'the GitHub repository where your project can be found'
    githubtoken: 'the GitHub OAuth token if this project is private'
    excludestages:
      - '[name of a stage to exclude]'
      - '[another stage name to exclude]'
```

Or you can also store some parameters per stage by using the following (let us know if more should be per-stage):
```yaml
custom:
  staging:
    branch: 'the git branch you want to watch for the stage called staging'
  prod:
    branch: 'a different branch you want to watch for the stage called prod'
```

### Some details on these parameters
Parameter | Info | Default | More Information
------ | ------ | ------ | ------
image (node) | If the runtime is nodeJS | aws/codebuild/nodejs:6.3.1 | [Lookup other image identifiers](http://docs.aws.amazon.com/codebuild/latest/userguide/build-env-ref-available.html)
image (python) | If the runtime is python | aws/codebuild/python:3.5.2 | [Lookup other image identifiers](http://docs.aws.amazon.com/codebuild/latest/userguide/build-env-ref-available.html)
image (other) | If the runtime is something else | aws/codebuild/ubuntu-base:14.04 | [Lookup other image identifiers](http://docs.aws.amazon.com/codebuild/latest/userguide/build-env-ref-available.html)
branch | The git branch CodePipeline monitors | master | [More on how CodePipeline starts](http://docs.aws.amazon.com/codepipeline/latest/userguide/pipelines-about-starting.html)
owner | The owner of the GitHub repository | *blank* | Required as no default
repository | The GitHub repository CodePipeline monitors | The name of your service | [More on how CodePipeline starts](http://docs.aws.amazon.com/codepipeline/latest/userguide/pipelines-about-starting.html)
githubtoken | The GitHub OAuth token for private repos | *blank* | [How to get a token](https://help.github.com/articles/creating-a-personal-access-token-for-the-command-line/)
excludestages | Stages you don't want CICD for | *blank* | [Serverless stages](https://serverless.com/framework/docs/providers/aws/guide/workflow#using-stages)


## Deploying
---------
The plugin will be packaged with the lambda when deployed as normal using Serverless:
```
serverless deploy
```

# Support
All support is conducted through GitHub issues. This is released basically "as is" but we will answer questions as we can.

# Contributing
Please open a GitHub issue before contributing code changes.
