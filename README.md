# istio-helm-values

Helm values for **Istio upstream charts** only, organized **one folder per chart** per cluster. Chart sources and versions are pinned in `argocd-applications`.

## Versioned layout for clean upgrades

Use version folders per cluster so each Istio upgrade is additive and easy to roll back:

`clusters/<cluster>/<istio-version>/<component>/values.yaml`

Example:

`clusters/management/1.29.1/istiod/values.yaml`

## Install order (sidecar / default profile)

Typical sync order (see Argo `sync-wave` annotations in Applications):

1. **cni** (optional, if using Istio CNI instead of init-container injection)
2. **base**
3. **istiod**
4. **gateway** (ingress or east-west; add more gateway folders if needed)

## Ambient profile

If you adopt ambient mesh, add **ztunnel** and follow Istio ambient documentation; remove or disable components that ambient replaces. The `ztunnel` Application is a stub for that path.

## Chart repository

Official charts: `https://istio-release.storage.googleapis.com/charts` (charts `base`, `istiod`, `gateway`, `cni`, `ztunnel`).

## Related repositories

| Repository | Role |
|------------|------|
| `argocd-applications` | `Application` manifests referencing this repo |
