

# Azure Pipelines CI Trigger

A brief description of what this project does and who it's for

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






### Caveats

-You cannot use variables in triggers, as variables are evaluated at runtime (after the trigger has fired).

-If you use templates to author YAML files, then you can only specify triggers in the main YAML file for the pipeline. You cannot specify triggers in the template files.
