# Docker Image Versioning

When working with Docker images, you can specify a version, also known as a tag. If you don't specify a tag, Docker defaults to using the `latest` tag.

## The `latest` Tag

The `latest` tag is a convention used for the most recent stable build of an image. When you pull an image without specifying a tag, Docker assumes you mean `latest`.

For example, the following two commands are equivalent:

```bash
docker pull mysql
```

```bash
docker pull mysql:latest
```

## Specifying a Version

It is a good practice to specify a version tag to ensure you are using a specific, predictable version of an image. This helps to avoid unexpected changes that might be introduced in the `latest` version.

For example, to pull a specific version of MySQL, you can use:

```bash
# Pulls MySQL version 8.0
docker pull mysql:8.0
```

You can find available tags for an image on its Docker Hub page.
