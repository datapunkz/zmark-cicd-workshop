# JFrog X-ray Pipeline Scanning Integrations

This branch demonstrates how to configure, implement and utilize JFrog X-ray source and Docker image vulnerability scans within CircleCI CI/Cd pipelines.

## Prerequisites

- Signup for a JFrog Cloud account (It's a 14 Day trial)
- Create a new [Docker Repository](https://jfrog.com/help/r/jfrog-artifactory-documentation/set-up-a-docker-repository) In this example used the name `cicd-docker` for the docker repo.
- [Configure the docker repo](https://jfrog.com/help/r/jfrog-artifactory-documentation/set-up-a-docker-repository) 
- [Setup your Docker client](https://jfrog.com/help/r/jfrog-artifactory-documentation/use-docker-client-with-artifactory-cloud)
- [Configure the following CircleCI context variables](https://circleci.com/docs/contexts/#create-and-use-a-context)
  - ARTIFACTORY_API_KEY: Assign your Artifactory API Key
  - ARTIFACTORY_URL: Assign your Artifactory URL
  - ARTIFACTORY_USER: Assign your Artifactory username
  - PWD_DOCKER: Assign your [Docker Hub Account](https://docs.docker.com/security/for-developers/access-tokens/) password or api token
  - URL_DOCKER: Assign you [Docker Hub account](https://docs.docker.com/security/for-developers/access-tokens/) username
- [Configure CircleCI project environment variables](https://circleci.com/docs/set-environment-variable/)
  - SNYK_TOKEN: assign your [Snyk Api Token](https://docs.snyk.io/snyk-cli/authenticate-the-cli-with-your-account#steps-to-authenticate-using-your-api-token)


## TASK: Build a pipeline
1.Use any software project of your choice (open source or self-written) as your project source code
2.Build a CI/CD pipeline with your choice of tool with the following steps:
 - Build the project
 - Run tests
 - Package the project as a runnable Docker image
 - Implement security scanning in your pipeline
 - Include any JFrog tooling

## Deliverables

The following list the deliverables;

- Github Link: [jf-test branch](https://github.com/datapunkz/cicd-workshop/tree/jf-test)
- CI/CD Pipeline:
  - [.circleci/config.yml](https://github.com/datapunkz/cicd-workshop/blob/jf-test/.circleci/config.yml)
  - [CircleCI Pipeline Dashboard View](https://app.circleci.com/pipelines/github/datapunkz/cicd-workshop/123/workflows/b10fd04c-8e42-4b63-baf5-e7be308d963a)
- [Build the project](https://app.circleci.com/pipelines/github/datapunkz/cicd-workshop/123/workflows/b10fd04c-8e42-4b63-baf5-e7be308d963a/jobs/521)
- [Run tests](https://app.circleci.com/pipelines/github/datapunkz/cicd-workshop/123/workflows/b10fd04c-8e42-4b63-baf5-e7be308d963a/jobs/521/parallel-runs/0/steps/0-109)
- [Package project as Docker Image](https://app.circleci.com/pipelines/github/datapunkz/cicd-workshop/123/workflows/b10fd04c-8e42-4b63-baf5-e7be308d963a/jobs/520)
- [Build Docker Image](https://app.circleci.com/pipelines/github/datapunkz/cicd-workshop/123/workflows/b10fd04c-8e42-4b63-baf5-e7be308d963a/jobs/520/parallel-runs/0/steps/0-103)
- [Implement security scanning in your pipeline](https://app.circleci.com/pipelines/github/datapunkz/cicd-workshop/123/workflows/b10fd04c-8e42-4b63-baf5-e7be308d963a/jobs/520):
  - [Xray scan source code](https://app.circleci.com/pipelines/github/datapunkz/cicd-workshop/123/workflows/b10fd04c-8e42-4b63-baf5-e7be308d963a/jobs/521/parallel-runs/0/steps/0-113)
  - [X-ray scan Docker Image](https://app.circleci.com/pipelines/github/datapunkz/cicd-workshop/123/workflows/b10fd04c-8e42-4b63-baf5-e7be308d963a/jobs/520/parallel-runs/0/steps/0-104)
  - [Snyk App and Docker image Scans](https://app.circleci.com/pipelines/github/datapunkz/cicd-workshop/123/workflows/b10fd04c-8e42-4b63-baf5-e7be308d963a/jobs/519)
- Applicable build definition file: [config.yml](https://github.com/datapunkz/cicd-workshop/blob/jf-test/.circleci/config.yml)
- Project Docker definition: [DockerFile](https://github.com/datapunkz/cicd-workshop/blob/jf-test/Dockerfile)


## Execution

This pipeline demonstrates how to configure a CI/CD workflow to build, test, scan and images for vulnerabilities and finally deploying the image to a JFrog Docker registry along with deploying the to a publicly available Docker Hub registry. The Docker images have been scanned for vulnerabilities using JFrog X-ray and Snyk. To execute this container we'll use the publicly available docker image built and deployed image to Docker hub.

Execute these commands to pull and run this Docker image locally:

```
# Pull the docker image locally
docker pull ariv3ra/cicd-workshop

# Run the container locally 
docker run -d --name jfrog-demo -p5000:5000 ariv3ra/cicd-workshop
```

In a web browser goto `http:/localhost:5000`  and you should the Welcome page.

To stop the container run: `docker stop jfrog-demo`

