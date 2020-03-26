# :zap: serverless-ssm-publish
[![serverless](http://public.serverless.com/badges/v3.svg)](http://www.serverless.com)
[![npm version](https://badge.fury.io/js/serverless-ssm-publish.svg)](https://badge.fury.io/js/serverless-ssm-publish)
[![npm downloads](https://img.shields.io/npm/dt/serverless-ssm-publish.svg?style=flat&logo=npm)](https://www.npmjs.com/package/serverless-ssm-publish)
[![MIT licensed](https://img.shields.io/badge/license-MIT-blue.svg)](https://raw.githubusercontent.com/ColdFire87/serverless-ssm-publish/master/LICENSE)
[![Coverage Status](https://coveralls.io/repos/github/ColdFire87/serverless-ssm-publish/badge.svg?branch=develop)](https://coveralls.io/github/ColdFire87/serverless-ssm-publish?branch=develop)
[![Build Status](https://travis-ci.org/ColdFire87/serverless-ssm-publish.svg?branch=develop)](https://travis-ci.org/ColdFire87/serverless-ssm-publish)

Publish custom data to AWS SSM Parameter Store from serverless.yaml.

## Install

* Install with your choice of npm/yarn
`npm install serverless-ssm-publish --save-dev`
* Add the plugin to your `plugins` section in the serverless.yaml
```yaml
plugins:
  - serverless-ssm-publish
```

## Usage

### During deployment

Add any params you want published to SSM to your serverless.yaml custom section.
Ssm publish compares existing values and will only write if no value exists/ the value has changed.

```yaml
custom:
  secretToken: ${opt:secretToken}

  ssmPublish:
    enabled: true                             # Needs to be set to true
    params:
      - path: /global/tokens/secretToken
        value: ${self:custom.secretToken}
        description: Super Secret Token       # description is optional
        secure: true                          # defaults to true
      - path: /service/config/storageBucket
        value: !Ref StorageBucket
        secure: false
```

### From the CLI

You can also call the plugin directly in order to update SSM params without running deployment/packaging.

`sls ssmPublish`

## [Changelog](./CHANGELOG.md)

## Version History
*0.1.0
  - Initial release
