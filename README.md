# fauna-circle-repro

This repo contains a small repro for the incompatibility between
[the Fauna Dev docker image](https://docs.fauna.com/fauna/current/build/tools/dev)
and [CircleCI](https://circleci.com/docs/2.0/high-uid-error/).

The issue popped up with v4.23 of the Docker image.

The CI runs for this repo are visible here:
https://app.circleci.com/pipelines/github/jrr/fauna-circle-repro

The symptom looks like this (happens on branches `fauna-docker-4.23` and
`fauna-docker-latest`):

```
Build-agent version 1.0.187186-94b07954 (2023-06-27T15:43:38+0000)
System information:
 Server Version: 20.10.18
 Storage Driver: overlay2
  Backing Filesystem: xfs
 Cgroup Driver: cgroupfs
 Cgroup Version: 1
 Kernel Version: 5.15.0-1030-aws
 Operating System: Ubuntu 20.04.5 LTS
 OSType: linux
 Architecture: x86_64

Starting container cimg/base:stable
cimg/base:stable:
  using image cimg/base@sha256:35e5e29930ab565475a4f2aa9b4124998ed67dbc7b0e2dd5f420a4189d08d0d2
  pull stats: Image was already available so the image was not pulled
  time to create container: 28ms
Starting container fauna/faunadb:4.23.0
Warning: No authentication provided, using CircleCI credentials for pulls from Docker Hub.
  image is cached as cimg/base:stable, but refreshing...
stable: Pulling from cimg/base
Digest: sha256:35e5e29930ab565475a4f2aa9b4124998ed67dbc7b0e2dd5f420a4189d08d0d2
Status: Image is up to date for cimg/base:stable
Warning: No authentication provided, using CircleCI credentials for pulls from Docker Hub.
  image cache not found on this host, downloading fauna/faunadb:4.23.0
4.23.0: Pulling from fauna/faunadb


f56be85fc22e: Pulling fs layer 
(...)
a8b8d12981cf: Extracting [==================================================>]  40.27MB/40.27MB

CircleCI was unable to start the container because of a userns remapping failure in Docker.

This typically means the image contains files with UID/GID values that are higher than Docker and CircleCI can use.

Checkout our docs https://circleci.com/docs/2.0/high-uid-error/ to learn how to fix this problem.
Original error: CircleCI was unable to start the container because of a userns remapping failure in Docker.

This typically means the image contains files with UID/GID values that are higher than Docker and CircleCI can use.

Checkout our docs https://circleci.com/docs/2.0/high-uid-error/ to learn how to fix this problem.
Original error: failed to register layer: Error processing tar file(exit status 1): Container ID 110779 cannot be mapped to a host ID
```
