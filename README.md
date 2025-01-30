# StaticJinjaPlus Docker Port
A set of dockerfiles for creating different images and containers of [StaticJinjaPlus](https://github.com/MrDave/StaticJinjaPlus) project.  
Built images can be taken from [DockerHub](https://hub.docker.com/repository/docker/paraigor/static-jinja-plus/tags).
## How to build
Docker should be [installed](https://docs.docker.com/engine/install/) on your system.

There are 4 Dockerfiles with different base and for building images with different versions of project.  
Two of them based on Ubuntu 24.04 image, `Dockerfile-latest` and `Dockerfile-versioned`.  
And two on Python 3.12.8-slim image, `Dockerfile-slim` and `Dockerfile-versioned-slim`.

To build images with latest version of project, use following commands in folder where dockerfile is:
```sh
$ docker build -t static-jinja-plus:latest -f Dockerfile-latest .
$ docker build -t static-jinja-plus:slim -f Dockerfile-slim .
```
To build images with different versions of project, will need some additional actions.  
Get download link of project from GitHUb:
> https://github.com/MrDave/StaticJinjaPlus/archive/refs/tags/[TAG_VERSION].tar.gz # For tags
> https://github.com/MrDave/StaticJinjaPlus/archive/[COMMIT_HASH].tar.gz # For develop (last commit) version

Get hash for archive files:
```sh
$ curl -sL https://github.com/MrDave/StaticJinjaPlus/archive/refs/tags/[TAG_VERSION].tar.gz | sha256sum
```
Build an image:
```sh
$ docker build -t static-jinja-plus:0.1.0 -f Dockerfile-versioned . --build-arg VERSION_URL=https://github.com/MrDave/StaticJinjaPlus/archive/refs/tags/0.1.0.tar.gz --build-arg VERSION_HASH=[HASH]
...
$ docker build -t static-jinja-plus:develop-slim -f Dockerfile-versioned-slim . --build-arg VERSION_URL=https://github.com/MrDave/StaticJinjaPlus/archive/e19f029cf633bf8d65ac3d330d60a58bd116005d.tar.gz --build-arg VERSION_HASH=[HASH]
```
## How to run
Navigate to folder where your `templates` are and run container:
```sh
$ docker run --rm -v $(pwd):/opt/StaticJinjaPlus/data static-jinja-plus:[IMAGE_VERSION]
```
As result, `build` folder with rendered files will be created near `templates` folder.
## Project Goals
The code is written for educational purposes on online-course for web-developers dvmn.org.
