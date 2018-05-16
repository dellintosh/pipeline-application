# pipeline-application

## Usage

Changes pushed to any branch except master should trigger the following actions:

  - build a container image tagged with the build ID suitable for deploying to a staging cluster
  - clone the [pipeline-application-infra-staging](https://github.com/dellintosh/pipeline-application-infra-staging) repo
  - patch the pipeline deployment configuration file with the staging container image and commit the changes to the `pipeline-application-infra-staging` repo

> The `pipeline-application-infra-staging` repo will deploy any updates committed to the master branch.

Tagging this repo should trigger the following actions:

  - build a container image tagged with the tag name suitable for deploying to a qa cluster
  - clone the [pipeline-application-infra-qa](https://github.com/dellintosh/pipeline-application-infra-qa) repo
  - patch the pipeline deployment configuration file with the qa container image and commit the changes to the `pipeline-application-infra-qa` repo

> The `pipeline-application-infra-qa` repo will deploy any updates committed to the master branch and issue a pull request to the `pipeline-application-infra-production` repo

See the [.drone.yml](.drone.yml) file for more details.