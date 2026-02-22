# UNCG ILRS - Information Library Research Sciences

## Introduction

Welcome to the UNCG ILRS (Information Library Research Sciences) repository!
This repository is designed to provide resources, tools, and documentation for
students and researchers involved in library and information sciences. Whether
you're just getting started or looking for advanced materials, this guide will
help you navigate the repositories effectively.

## Getting Started

To get started with any UNCG ILRS repository, follow these steps:

1. Clone the repository to your local machine:
```bash
git clone <repository-url>
```

2. Navigate to the repository directory:
```bash
cd <repository-name>
```

3. Each repository contains its own `Containerfile` and `requirements.txt`.
   Refer to the individual repository's `README.md` for specific setup instructions.

### Branch Information

The repository uses two primary branches:

- **main**: This is the stable branch containing the latest production-ready
  code and resources. Always refer to this branch for the most reliable materials.
- **develop**: This is the _default_ branch where active development occurs.
  It may contain experimental features or updates not yet finalized. Use this
  branch to contribute or test new features.

To switch between branches:
```bash
git checkout <branch-name>
```

### Container Setup

Each repository includes its own `Containerfile` to ensure a reproducible
environment. Refer to the individual repository's documentation for specific
container instructions. General steps are as follows:

1. Install [Docker](https://docs.docker.com/get-docker/) or
   [Podman](https://podman.io/getting-started/installation)

2. Build the container:
```bash
docker build -t <repo-name> .
# or with Podman
podman build -t <repo-name> .
```

3. Run the container:
```bash
docker run -it --rm -v $(pwd):/app <repo-name>
# or with Podman
podman run -it --rm -v $(pwd):/app <repo-name>
```

## Course Information and Summaries

Below is a summary of the courses available in this repository:

- **IAN 604 - Machine Learning and Predictive Analytics**
  - *insert*
  
- **IAN 630 - Fundamentals of Health & Sport Infomratics**
  - *insert*
