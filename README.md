# fleet-infra

# Recipe for clusty
This doesn't include creating `kustomization.yaml` which are manual afaict
```
flux create source git infra --url=https://gitlab.com/insanitywholesale/infra --branch=master --interval=75s --export > clusters/clusty/core/infra-source.yml
flux create source helm nfs-subdir-external-provisioner --url=https://kubernetes-sigs.github.io/nfs-subdir-external-provisioner --interval=10m --export > clusters/clusty/core/nfs-subdir-source.yml
flux create kustomization core --namespace flux-system --interval 2m --prune true --path ./clusters/clusty/core --source GitRepository/flux-system --export > clusters/clusty/base/core.yml
```
