## FluxV2 - Kustomize Example

### Setup:

1. Create development k3s cluster using k3d:
    ```bash
    k3d cluster create development --api-port 6550 --servers 1 --port 443:443@loadbalancer --wait --k3s-server-arg '--no-deploy=traefik'
    ```

2. Bootstrap flux:
    ```bash
    # export github token (must have "repo" access rights)
    export GITHUB_TOKEN="ghp_tD*********************"

    # bootstrap flux
    flux bootstrap github \
        --owner=ashrafgt \
        --repository=flux-kustomize-example \
        --branch=develop \
        --network-policy=false \
        --path=clusters/development
    ```
