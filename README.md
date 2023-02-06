# System Monitoring APP

Provides system information and a realtime monitoring screen with dials showing CPU, memory, IO and process information.

The app is constructed with cloud native containers in mind, in order to provide a real working application for deployment. 

## Screenshots

Page: main
![main](screenshots/main.png)

Page: Monitor
![monitor](screenshots/monitoring.png)

Page: Info
![monitor](screenshots/info.png)

## Building & Running Locally

### Pre-reqs

- Be using Linux, WSL or MacOS, with bash, make etc
- [Python 3.8+](https://www.python.org/downloads/) - for running locally, linting, running tests etc
- [Docker](https://docs.docker.com/get-docker/) - for running as a container, or image build and push
- [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli-linux) - for deployment to Azure

Clone the project to any directory where you do development work

```
git clone https://github.com/benc-uk/python-demoapp.git
```

### Makefile

A standard GNU Make file is provided to help with running and building locally.

```text
help                 💬 This help message
lint                 🔎 Lint & format, will not fix but sets exit code on error
lint-fix             📜 Lint & format, will try to fix errors and modify code
image                🔨 Build container image from Dockerfile
push                 📤 Push container image to registry
run                  🏃 Run the server locally using Python & Flask
deploy               🚀 Deploy to Azure Web App
undeploy             💀 Remove from Azure
test                 🎯 Unit tests for Flask app
test-report          🎯 Unit tests for Flask app (with report output)
test-api             🚦 Run integration API tests, server must be running
clean                🧹 Clean up project
```

Make file variables and default values, pass these in when calling `make`, e.g. `make image IMAGE_REPO=blah/foo`

| Makefile Variable | Default                |
| ----------------- | ---------------------- |
| IMAGE_REG         | ghcr<span>.</span>io   |
| IMAGE_REPO        | benc-uk/python-demoapp |
| IMAGE_TAG         | latest                 |
| AZURE_RES_GROUP   | temp-demoapps          |
| AZURE_REGION      | uksouth                |
| AZURE_SITE_NAME   | pythonapp-{git-sha}    |

The app runs under Flask and listens on port 5000 by default, this can be changed with the `PORT` environmental variable.

# Containers

<!-- Public container image is [available on GitHub Container Registry](https://github.com/users/packages/container/package/python-demoapp)

Run in a container with:

```bash
docker run --rm -it -p 5000:5000 ghcr.io//python-demoapp:latest
```

Should you want to build your own container, use `make image` and the above variables to customise the name & tag. -->

## Kubernetes

The app can easily be deployed to Kubernetes using Helm, see [deploy/kubernetes/readme.md](deploy/kubernetes/readme.md) for details

# GitHub Actions CI/CD

A working set of CI and CD release GitHub Actions workflows are provided `.github/workflows/`, automated builds are run in GitHub hosted runners



## Running in Azure App Service (Linux)

If you want to deploy to an Azure Web App as a container (aka Linux Web App), a Bicep template is provided in the [deploy](deploy/) directory

For a super quick deployment, use `make deploy` which will deploy to a resource group, temp-demoapps and use the git ref to create a unique site name

```bash
make deploy
```

## Running in Azure App Service (Windows)

Just don't, it's awful 
