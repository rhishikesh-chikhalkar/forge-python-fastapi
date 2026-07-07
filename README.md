# forge-python-fastapi

A production-grade FastAPI starter project generator built with [Copier](https://copier.readthedocs.io/).

This template generates a robust backend project following hexagonal architecture, ready for deployment to AWS EKS with Terraform and Helm.

## Features

- **FastAPI** with Pydantic v2
- **Hexagonal Architecture** (Domain, Services, Repositories)
- **SQLAlchemy 2.0** (async) + Alembic migrations
- **Docker** multi-stage builds (dev/prod)
- **Terraform** for AWS EKS, VPC, ECR, Secrets Manager, CloudWatch
- **Helm** chart with IRSA, HPA, and External Secrets integration
- **CI/CD** via AWS CodePipeline (or GitHub Actions ready)
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
copier copy gh:you/forge-python-generic my-new-project
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
3. Test locally by running: `copier copy . /tmp/test-project`
