# Peak IT - Brașov - 2020
**Table of Contents**  
- [Description](#description)  
- [Presentation Slides](#slides) 
- [References](#references)  
- [CI Pipeline](#ci-pipeline)  
- [Docker Commands](#docker-commands)

[![Build Status](https://dev.azure.com/satrapu/peak-it-2020/_apis/build/status/ci-pipeline?branchName=main)](https://dev.azure.com/satrapu/peak-it-2020/_build/latest?definitionId=8&branchName=main) [![Quality Gate Status](https://sonarcloud.io/api/project_badges/measure?project=satrapu_peak-it-2020&metric=alert_status)](https://sonarcloud.io/dashboard?id=satrapu_peak-it-2020)

<a name="description">Description</a>
--
This repo contains the resources to be used during the "Use Docker Compose when running integration tests with Azure Pipelines" presentation 
at the 3rd edition of the [Peak IT](https://peakit.ro/) conference, which will take place in Brașov between October 17th and 18th 2020 (online event due to COVID-19).  

This presentation is based on this article: [Use Docker Compose when running integration tests with Azure Pipelines](https://crossprogramming.com/2020/09/03/use-docker-compose-when-running-integration-tests-with-azure-pipelines.html).  

<a name="slides">Presentation Slides</a>
--
TODO

<a name="references">References</a>
--

* Azure Pipelines  
  * [Home](https://azure.microsoft.com/en-us/services/devops/pipelines/)
  * [YAML reference](https://docs.microsoft.com/en-us/azure/devops/pipelines/yaml-schema?view=azure-devops&tabs=schema%2Cparameter-schema)
  * One can use [multi-stage pipeline](https://docs.microsoft.com/en-us/azure/devops/pipelines/process/stages?view=azure-devops&tabs=yaml) to implement complex automation flows
  * [Announcing Azure Pipelines with unlimited CI/CD minutes for open source](https://azure.microsoft.com/en-us/blog/announcing-azure-pipelines-with-unlimited-ci-cd-minutes-for-open-source/)
* Docker
  * [Home](https://www.docker.com/)
  * [What is a Container?](https://www.docker.com/resources/what-container)
  * [Get Started with Docker](https://www.docker.com/get-started)
* Docker Compose 
  * [Home](https://docs.docker.com/compose/)
  * [Docker Compose healthcheck](https://docs.docker.com/compose/compose-file/#healthcheck)
  * [Compose CLI reference](https://docs.docker.com/compose/reference/)
  * [Getting Started with Docker Compose](https://docs.docker.com/compose/gettingstarted/)
  * For learning Docker & Docker Compose I highly recommend the following course by [Bret Fisher](https://www.bretfisher.com/): [Docker Mastery](https://www.udemy.com/course/docker-mastery/) (not free, but worth every penny)
  * Orchetrators to use when using more than just one Docker host
    * [Docker Swarm](https://docs.docker.com/engine/swarm/)
    * [Kubernestes](https://kubernetes.io/)
    * [Apache Mesos](http://mesos.apache.org/)
    * [Nomad](https://www.nomadproject.io/)
    * Others
* PostgreSQL
  * [Home](https://www.postgresql.org/)
  * Linux containers
    * [Docker image](https://hub.docker.com/_/postgres)
    * [Dockerfile](https://github.com/docker-library/postgres/blob/master/12/alpine/Dockerfile)
  * Windows containers
    * [Docker image](https://hub.docker.com/r/stellirin/postgres-windows)
    * [Dockerfile](https://github.com/stellirin/docker-postgres-windows/blob/master/Dockerfile)
* ASP.NET Core Web APIs
  * [Home](https://dotnet.microsoft.com/apps/aspnet/apis)
  * [Documentation](https://docs.microsoft.com/en-us/aspnet/core/?view=aspnetcore-3.1)
  * [Tutorial: Create a web API with ASP.NET Core](https://docs.microsoft.com/en-us/aspnet/core/tutorials/first-web-api?view=aspnetcore-3.1&tabs=visual-studio)
* Entity Framework Core 
  * [Home](https://github.com/dotnet/efcore)
  * [Documentation](https://docs.microsoft.com/en-us/ef/)
* Coverlet 
  * [Home](https://github.com/coverlet-coverage/coverlet)
* ReportGenerator 
  * [Home](https://danielpalme.github.io/ReportGenerator/)
* SonarCloud 
  * [Home](https://sonarcloud.io)
  * [Documentation](https://sonarcloud.io/documentation)
  
<a name="ci-pipeline">CI Pipeline</a>
--
In order to have a clear image of the CI pipeline used to build the source code from this repo, please visit: https://github.com/satrapu/aspnet-core-logging.

<a name="docker-commands">Docker Commands</a>
--

* Start compose services
```bash
# Start compose services founder under a specific project
docker-compose --file="docker-compose.yml" --project-name="peak-it-2020" up --detach
```

* List running Docker containers found under a specific compose project
```bash
docker container ls -a --filter "label=com.docker.compose.project=peak-it-2020" --format "{{ .ID }}"
```

* Display details of a particular Docker container
```bash
docker container inspect --format "{{ json .Config.Labels }}" peak-it-2020-db-dev
```

* Check the health state of a particular Docker container
```bash
docker container inspect --format "{{.State.Health.Status}}" peak-it-2020-db-dev
```

* List all ports exposed by a particular Docker container
```bash
docker container port peak-it-2020-db-dev
```
