# my-app

A demonstration project showcasing a modern DevOps pipeline combining Java application development with Kubernetes deployment automation.

## Tech Stack

- **Java 11** — Application code
- **Maven** — Build and dependency management
- **Helm** — Kubernetes package manager
- **GitLab CI/CD** — Automated pipeline
- **Kubernetes** — Container orchestration

## Project Structure

```
my-app/
├── my-java-app/                        # Java application
│   ├── src/
│   │   ├── main/java/com/myapp/
│   │   │   ├── App.java                # Entry point
│   │   │   └── Calculator.java         # Business logic
│   │   └── test/java/com/myapp/
│   │       └── CalculatorTest.java     # Unit tests
│   └── pom.xml                         # Maven configuration
├── templates/                          # Helm templates
│   ├── deployment.yaml
│   ├── service.yaml
│   └── configmap.yaml
├── Chart.yaml                          # Helm chart metadata
├── values.yaml                         # Default configuration
└── .gitlab-ci.yml                      # CI/CD pipeline definition
```

## CI/CD Pipeline

The pipeline runs automatically on Merge Requests and pushes to `main`.

| Stage    | Job              | Trigger  |
|----------|------------------|----------|
| build    | `maven-build`    | MR only  |
| test     | `maven-test`     | MR only  |
| test     | `maven-package`  | MR only  |
| lint     | `helm-lint`      | MR only  |
| template | `helm-template`  | MR only  |
| deploy   | `helm-deploy`    | main only|

### Pipeline Flow

```
Merge Request → build → test → lint → template ✅
                                              ↓
                                         Code Review
                                              ↓
Merge to main →                           deploy 🚀
```

## Getting Started

### Prerequisites

- Kubernetes cluster
- Helm 3+
- Java 11+
- Maven 3+

### Run Locally

```bash
cd my-java-app
mvn package
java -cp target/my-java-app-1.0-SNAPSHOT.jar com.myapp.App
```

### Deploy to Kubernetes

```bash
helm upgrade --install my-release . --reset-values
```

### Run Tests

```bash
cd my-java-app
mvn test
```

## Helm Configuration

Key values in `values.yaml`:

| Parameter            | Default    | Description                  |
|----------------------|------------|------------------------------|
| `replicaCount`       | `3`        | Number of pod replicas       |
| `image.repository`   | `nginx`    | Docker image                 |
| `service.type`       | `ClusterIP`| Kubernetes service type      |
| `service.port`       | `80`       | Service port                 |
| `configMap.enabled`  | `true`     | Enable ConfigMap             |

## GitLab CI/CD Configuration

The `.gitlab-ci.yml` defines two workflow triggers:

```yaml
workflow:
  rules:
    - if: $CI_PIPELINE_SOURCE == "merge_request_event"
    - if: $CI_COMMIT_BRANCH == "main"
```

- **On Merge Request** — runs all checks (build, test, lint, template)
- **On merge to main** — runs only deploy

## Kubernetes Resources

Helm chart deploys the following Kubernetes resources:

- **Deployment** — manages pod replicas
- **Service** — exposes the application within the cluster
- **ConfigMap** — stores application configuration

## Rollback

```bash
# View release history
helm history my-release

# Rollback to previous revision
helm rollback my-release 1
```
