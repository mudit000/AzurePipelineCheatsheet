
# Azure Pipelines CI Trigger



## Single Repo CI Triggers

-The repository in which the YAML file is present is called self repository. By default, this is the repository that your pipeline builds.

-Continuous integration (CI) triggers cause a pipeline to run whenever you push an update to the specified branches or you push specified tags.

#### Simple Branch CI Triggers
Specify the full name of the branch or a wildcard as below to trigger the build on master branch or on all release branch.

```javascript
trigger:
- master
- releases/*
```
#### Specific Branch CI Triggers
Below syntax triggers a build for all master and release branches except the release branches which starts with old.

```javascript
trigger:
  branches:
    include:
    - master
    - releases/*
    exclude:
    - releases/old*
```
#### Tag Based CI Triggers
We can also configure triggers based on tags by using the following format:
```javascript
trigger:
  branches:
    include:
      - refs/tags/{tagname}
    exclude:
      - refs/tags/{othertagname}
```

#### Batching CI Runs
While teams are always developing and committing frequently and parallelly,setting batch property to true helps in batching the CI runs.

If we set batch to true, when a pipeline is running, the system waits until the run is completed, then starts another run with all changes that have not yet been built.

In ideal scenario for such cases, it is recommended that we split our CI/CD process into two pipelines - one for build (with batching) and one for deployments so that one stage is completed,the other batch one doesn't conflict with previous CI run.

```javascript
# specific branch build with batching
trigger:
  batch: true
  branches:
    include:
    - master
```

#### Path based CI Triggers 
We can specify file paths to include or exclude.


```javascript
trigger:
  branches:
    include:
    - master
    - releases/*
  paths:
    include:
    - docs
    exclude:
    - docs/README.md
```

#### CI Triggers for specific tags
We can directly specify tags to include or exclude:
```javascript
trigger:
  tags:
    include:
    - v2.*
    exclude:
    - v2.0
```

### Skipping CI 

#### Disabling the CI trigger
 ```javascript
# A pipeline with no CI trigger
trigger: none
```

#### Skipping CI for individual commits
For Azure Pipelines to skip running a pipeline that a commit would normally trigger,Just include below message in the commit message.

 ```javascript
[skip ci] or [ci skip]
skip-checks: true or skip-checks:true
[skip azurepipelines] or [azurepipelines skip]
[skip azpipelines] or [azpipelines skip]
[skip azp] or [azp skip]
***NO_CI***
```




### Caveats

-You cannot use variables in triggers, as variables are evaluated at runtime (after the trigger has fired).

-If you use templates to author YAML files, then you can only specify triggers in the main YAML file for the pipeline. You cannot specify triggers in the template files.

-You cannot use variables in paths, as variables are evaluated at runtime (after the trigger has fired).
