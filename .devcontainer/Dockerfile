# syntax=docker/dockerfile:1.5

ARG BASE
ARG PYTHON_PACKAGE_MANAGER=conda

FROM ${BASE} as pip-base

RUN DEBIAN_FRONTEND=noninteractive \
    apt update -y \
 && apt install -y libdw-dev \
 && rm -rf /var/tmp/* /var/cache/apt/* /var/lib/apt/lists/*

ENV DEFAULT_VIRTUAL_ENV=legate

FROM ${BASE} as conda-base

ENV DEFAULT_CONDA_ENV=legate

FROM ${PYTHON_PACKAGE_MANAGER}-base

ARG CUDA
ENV CUDAARCHS="all-major"
ENV CUDA_VERSION="${CUDA_VERSION:-${CUDA}}"

ARG PYTHON_PACKAGE_MANAGER
ENV PYTHON_PACKAGE_MANAGER="${PYTHON_PACKAGE_MANAGER}"

ENV PYTHONSAFEPATH="1"
ENV PYTHONUNBUFFERED="1"
ENV PYTHONDONTWRITEBYTECODE="1"

ENV SCCACHE_REGION="us-east-2"
ENV SCCACHE_BUCKET="rapids-sccache-devs"
ENV VAULT_HOST="https://vault.ops.k8s.rapids.ai"
ENV HISTFILE="/home/coder/.cache/._bash_history"

ENV PROJECT_MANIFEST_YML="/home/coder/devcontainers/.devcontainer/manifest.yaml"
