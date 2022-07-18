# fleet-infra

# Recipe for clusty
This doesn't include creating `kustomization.yaml` which are manual afaict
```
flux create source git infra --url=https://gitlab.com/insanitywholesale/infra --branch=master --interval=75s --export > clusters/clusty/core/infra-source.yml
flux create source helm nfs-subdir-external-provisioner --url=https://kubernetes-sigs.github.io/nfs-subdir-external-provisioner --interval=10m --export > clusters/clusty/core/nfs-subdir-source.yml
flux create kustomization core --namespace flux-system --interval 2m --prune true --path ./clusters/clusty/core --source GitRepository/flux-system --export > clusters/clusty/base/core.yml
flux create helmrelease nfs-subdir-external-provisioner --source HelmRepository/nfs-subdir-external-provisioner --chart nfs-subdir-external-provisioner --interval 3m --values ./clusters/clusty/values/nfs-subdir-values.yml --export > clusters/clusty/core/nfs-subdir-chart.yml
flux create kustomization todo --namespace flux-system --interval 5m --prune true --path ./kube/manifests/todo --source GitRepository/infra --export > clusters/clusty/apps/todo/todo-kustomization.yml
```
