## FluxV2 - Kustomize Example

### Setup:

1. Create two k3s clusters using k3d:
    ```bash
    # create a "development" cluster
    k3d cluster create development --api-port 6550 --servers 1 --port 443:443@loadbalancer --wait --k3s-server-arg '--no-deploy=traefik'

    # create a "staging" cluster
    k3d cluster create staging --api-port 6551 --servers 1 --port 444:443@loadbalancer --wait --k3s-server-arg '--no-deploy=traefik'
    ```

2. Switch to the development cluster and bootstrap flux:
    ```bash
    # switch context
    kubectl config use-context k3d-development

    # export github token (must have "repo" access rights)
    export GITHUB_TOKEN="ghp_tD*********************"

    # bootstrap flux
    flux bootstrap github \
        --owner=ashrafgt \
        --repository=flux-kustomize-example \
        --branch=master \
        --network-policy=false \
        --path=clusters/development
    ```

3. Run the same instructions for the staging environment:
    ```bash
    # switch context
    kubectl config use-context k3d-staging

    # bootstrap flux
    flux bootstrap github \
        --owner=ashrafgt \
        --repository=flux-kustomize-example \
        --branch=master \
        --network-policy=false \
        --path=clusters/staging
    ```
