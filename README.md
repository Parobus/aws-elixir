# Amazon Linux Elixir Image
build from [official image](https://github.com/aws/amazon-linux-docker-images)

## Features

Erlang is installed, Elixir is installed.

## Usage
```
docker run -d parobus/amazonlinux-elixir:latest
```

## Updating

This image is based off several office images:

1) The most recent [Amazon linux](https://github.com/aws/amazon-linux-docker-images)
2) The relevant [Erlang release](https://github.com/rabbitmq/erlang-rpm)
3) The relevant [Elixir image](https://github.com/c0b/docker-elixir)

To upgrade copy the most recent `Dockerfile` to another, and then you will need
to either change the FROM to a specific amazon linux version, or edit the install
rpm url for erlang, or edit the copied over contents of the Elixir Dockerfile, then:

1 - `docker build <target dir>`
2 - `docker tag <resulting image> parobus/amazonlinux-elixir:<target>`
3 - `docker push parobus/amazonlinux-elixir:<target>`

Note you will need to be logged in as some with DockerHub priviledges.
