<p align="center"><img alt="Logo - RAGapp" src="docs/logo.png"></p>

<p align="center"><strong>The easiest way to use Agentic RAG in any enterprise.</strong></p>

<p align="center">As simple to configure as <a href="https://openai.com/index/introducing-gpts" target="_blank">OpenAI's custom GPTs</a>, but deployable in your own cloud infrastructure using Docker. Built using <a href="https://github.com/run-llama/llama_index">LlamaIndex</a>.</p>

<p align="center">
  <a href="#get-started"><strong>Get Started</strong></a> ·
  <a href="#endpoints"><strong>Endpoints</strong></a> ·
  <a href="#deployment"><strong>Deployment</strong></a> ·
  <a href="#contact"><strong>Contact</strong></a> 
</p>

<br/>
<img alt="Screenshot" src="docs/screenshot.png">


# RagApp Docker Setup

This repository contains the Docker Compose configuration for running RagApp with persistent data storage.


## Get Started

```yml

version: '3.8'

services:
  ragapp:
    image: ragapp/ragapp
    container_name: ragapp
    ports:
      - "8005:8000"
    volumes:
      - ~/.ragapp:/app/data
    restart: unless-stopped

```


## Prerequisites

- Docker installed on your system
- Docker Compose installed on your system

## Installation Steps

1. Create a new directory for your project:
   ```bash
   mkdir ragapp-docker
   cd ragapp-docker
   ```

2. Download the docker-compose.yml file to your project directory:
   ```bash
   # Copy the docker-compose.yml content from above into this file
   ```

3. Create the directory for persistent storage:
   ```bash
   mkdir -p ~/.ragapp
   ```

4. Start the application:
   ```bash
   docker compose up -d
   ```

5. The application will be available at: http://localhost:8005

## Management Commands

- To stop the application:
  ```bash
  docker compose down
  ```

- To view logs:
  ```bash
  docker compose logs
  ```

- To restart the application:
  ```bash
  docker compose restart
  ```

## Data Storage

All data is persisted in the `~/.ragapp` directory in your home folder. This ensures your data survives container restarts and updates.

## Notes

- The container will automatically restart unless explicitly stopped
- Port 8005 must be available on your host system
- Make sure you have appropriate permissions to create and access the ~/.ragapp directory

To run, start a docker container with our image:

```shell
docker run -p 8000:8000 ragapp/ragapp
```

Then, access the Admin UI at http://localhost:8000/admin to configure your RAGapp.

You can use hosted AI models from OpenAI or Gemini, and local models using [Ollama](https://ollama.com/).

> _Note_: To avoid [running into any errors](https://github.com/ragapp/ragapp/issues/22), we recommend using the latest version of Docker and (if needed) Docker Compose.

## Endpoints

The docker container exposes the following endpoints:

- Admin UI: http://localhost:8000/admin
- Chat UI: http://localhost:8000
- API: http://localhost:8000/docs

> _Note_: The Chat UI and API are only functional if the RAGapp is configured.

## Security

### Authentication

Just the RAGapp container doesn't come with any authentication layer by design. This is the task
of an API Gateway routing the traffic to RAGapp.
This step heavily depends on your cloud provider and the services you use.
For a pure Docker Compose environment, you can look at our [RAGapp with management UI](./deployments/multiple-ragapps) deployment.

### Authorization

Later versions of RAGapp will support restricting access based on access tokens forwarded from an API Gateway or similar.

## Deployment

### Using Docker Compose

You can easily deploy RAGapp to your own infrastructure with one of these Docker Compose deployments:

1. [RAGapp with Ollama and Qdrant](./deployments/single)
2. [Multiple RAGapps with a management UI](./deployments/multiple-ragapps)

### Kubernetes

It's easy to deploy RAGapp in your own cloud infrastructure. Customized K8S deployment descriptors are coming soon.

## Development

### RAGApp:

> _Important_: Parts of this project's source code is dynamically retrieved from the [create-llama](https://github.com/run-llama/create-llama) project. Before committing changes, make sure to update the source code by calling `make build-frontends`.

Move to [src/ragapp](src/ragapp) directory and start with these commands:

```shell
export ENVIRONMENT=dev
poetry install --no-root
make build-frontends
make dev
```

Then, to check out the admin UI, go to http://localhost:3000/admin.

> _Note_: Make sure you have [Poetry](https://python-poetry.org/) installed.

## Contact

Questions, feature requests or found a bug? [Open an issue](https://github.com/ragapp/ragapp/issues/new/choose) or reach out to [marcusschiesser](https://github.com/marcusschiesser).

## Star History

[![Star History Chart](https://api.star-history.com/svg?repos=ragapp/ragapp&type=Date)](https://star-history.com/#ragapp/ragapp&Date)
