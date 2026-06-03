# ga-prac

Small learning repository for experimenting with GitHub Actions workflows.

Purpose
- Practice creating and reusing workflows under `.github/workflows/`.
- Build and store Docker images as CI artifacts or push them to a container registry.

Workflows of interest
- `.github/workflows/docker-build.yml` — builds the Docker image and uploads it as an artifact.
- `.github/workflows/reusable.yml` — a reusable workflow that builds and uploads a Docker image.

Quick local commands
- Build the image locally (run from the repository root where the `Dockerfile` lives):

```bash
docker build -t my-node-app:latest .
docker save -o image.tar my-node-app:latest
```

- Compress the image before uploading (optional):

```bash
gzip -9 image.tar
```

CI notes
- GitHub Actions runs in the checked-out repo workspace; use `.` as the Docker build context unless your `Dockerfile` is elsewhere.
- CI cannot directly upload a Docker tag — export the image with `docker save` (or push to a registry such as GHCR).

Next steps
- Add any registry auth secrets and update workflows to push images to GHCR or Docker Hub if you want long-term storage.

This repo is intentionally minimal — use it as a sandbox for learning workflows.
