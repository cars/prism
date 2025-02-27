# Installation

For many, the easiest way to install Prism is as a node module.

```bash
npm install -g @stoplight/prism-cli
# or
yarn global add @stoplight/prism-cli
```

## Executable Binaries

For users without Node and/or NPM/Yarn, we provide standalone binaries for [all major platforms](https://github.com/stoplightio/prism/releases). The quickest way to install the appropriate package for your operating system is via this shell script:

```bash
curl -L https://raw.githack.com/stoplightio/prism/master/install | sh
```

<!-- theme: info -->

> The binaries do _not_ auto-update, so you will need to run it again to install new versions.

## Docker

Prism is available as a Docker image. We recommend specifying the major version you'd like to use as a tag:

```bash
docker run --init -p 4010:4010 stoplight/prism:4 mock -h 0.0.0.0 api.oas2.yml
```

If the document you want to mock is on your computer, you'll need to mount the directory where the file resides as a volume:

```bash
docker run --init --rm -v $(pwd):/tmp -p 4010:4010 stoplight/prism:4 mock -h 0.0.0.0 "/tmp/file.yaml"
```

If you want to start the proxy server, you can run a command like this:

```bash
docker run --init --rm -d -p 4010:4010 -v $(pwd):/tmp -P stoplight/prism:4 proxy -h 0.0.0.0 "/tmp/file.yml" http://host.docker.internal:8080 --errors
```

## Docker Compose

Alternatively, you may wish to use prism as part of a docker compose file to aid development environment portability. Below is a minimal example of a working `docker-compose.yml` supporting mocking:

```yaml
---
version: "3.9"
services:
  prism:
    image: stoplight/prism:4
    command: "mock -h 0.0.0.0 /tmp/api.oas3.yml"
    volumes:
      - ./api.oas3.yml:/tmp/api.oas3.yml:ro
    ports:
      # Serve the mocked API locally as available on port 8080
      - "8080:4010"
```
The above can be expanded if you with to [support TLS termination](../guides/10-nginx-tls-proxy.md).

Now everything is installed, let's look at some of the [concepts](./02-concepts.md).
