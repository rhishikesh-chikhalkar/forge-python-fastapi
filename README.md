# forge-python-fastapi

[![Copier](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/copier-org/copier/master/img/badge/badge-grayscale-inverted-border-orange.json)](https://github.com/copier-org/copier)
[![Python](https://img.shields.io/badge/Python-3.11+-blue.svg)](https://www.python.org)
[![FastAPI](https://img.shields.io/badge/FastAPI-0.111.0+-00a393.svg)](https://fastapi.tiangolo.com)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

A production-grade FastAPI starter project generator built with [Copier](https://copier.readthedocs.io/).

This template generates a robust backend project following hexagonal architecture, ready for deployment to **AWS EKS** or **Oracle Cloud OKE** with Terraform and Helm.

## Features

- **FastAPI** with Pydantic v2
- **Hexagonal Architecture** (Domain, Services, Repositories)
- **SQLAlchemy 2.0** (async) + Alembic migrations
- **Docker** multi-stage builds (dev/prod)
- **Cloud Provider** (choose one):
  - **AWS** — VPC, EKS, ECR, Secrets Manager, CloudWatch
  - **OCI** — VCN, OKE, OCIR, Vault, Monitoring (dev defaults use Always Free–eligible shapes)
- **Helm** chart with HPA, External Secrets, and cloud-native ingress
- **CI/CD** (choose one):
  - **AWS CodePipeline** — CodeBuild + CodePipeline
  - **OCI DevOps** — Build + Deployment Pipelines
  - **GitHub Actions** — full build, push, and deploy workflow
- **Celery** support (optional)
- **ArgoCD** GitOps manifests (optional)

---

## Getting-Started Checklist

### 1. Install Copier

```bash
pip install copier
# or
uv tool install copier
```

### 2. Generate a Project

```bash
copier copy gh:rhishikesh-chikhalkar/forge-python-fastapi my-new-project
# Answer the prompts (project_name, author, database, etc.)
```

### 3. Set Up the Project

```bash
cd my-new-project
cp .env.example .env         # Edit with your actual values
make install                 # Installs deps via uv + sets up pre-commit
make test                    # Run the full test suite
make run                     # Start the dev server at http://localhost:8000
```

### 4. Verify

- Open `http://localhost:8000/docs` for interactive API docs
- Hit `GET /api/v1/ping` to verify the health check
- Run `make lint` and `make typecheck` to verify code quality

### 5. Pull Template Updates Later

From inside your generated project:

```bash
copier update
# Copier reads .copier-answers.yml, pulls the latest template,
# re-renders files, and shows you a diff to review.
```

---

## Development

If you want to modify this template:

1. Clone this repository
2. Make your changes
3. Test locally:

```bash
# Test AWS + CodePipeline (default)
copier copy --defaults --data project_name="Test" --data author_name="Test" \
  --data author_email="t@t.com" --data github_username="test" . /tmp/test-aws

# Test OCI + OCI DevOps
copier copy --defaults --data project_name="Test" --data author_name="Test" \
  --data author_email="t@t.com" --data github_username="test" \
  --data cloud_provider=oci --data ci_cd_provider=oci_devops \
  --data oci_compartment_id="ocid1.compartment.oc1..example" . /tmp/test-oci

# Test OCI + GitHub Actions
copier copy --defaults --data project_name="Test" --data author_name="Test" \
  --data author_email="t@t.com" --data github_username="test" \
  --data cloud_provider=oci --data ci_cd_provider=github_actions \
  --data oci_compartment_id="ocid1.compartment.oc1..example" . /tmp/test-oci-gh
```
