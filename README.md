# fleet-infra

# Recipe for clusty
```
flux create source git infra --url=https://gitlab.com/insanitywholesale/infra --branch=master --interval=75s --export > clusters/clusty/core/infra-source.yml
```
