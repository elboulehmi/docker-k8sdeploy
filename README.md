# Kubernetes deployment helper image

This repository contains a Docker image that can be used for utility/deployment containers to build and deploy containerized applications on Kubernetes. One example usage might be in a CI pipeline.

Included components:

- Docker (CLI only)
- kubectl
- helm

## GitLab CI example

```yaml
deploy:
  stage: deploy
  image: quay.io/martinhelmich/k8s-deploy:v1.0.0
  script:
    - docker build -t your-application:${CI_COMMIT_TAG} .
    - docker push your-application:${CI_COMMIT_TAG}
    - helm upgrade --install --set image.tag=${CI_COMMIT_TAG} ./chart ${CI_PROJECT_NAME}
    - kubectl get pods -l release=${CI_PROJECT_NAME}
```