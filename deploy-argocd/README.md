# deploy-argocd

GitOps layout used to test Percona Operator for PostgreSQL under Argo CD.
Branch `argocd-test` is cut from tag `v3.1.0`; everything else in the repo is untouched.

| Path | Argo CD Application | Content |
| --- | --- | --- |
| `deploy/` (`crd.yaml`, `rbac.yaml`, `operator.yaml`) | `pg-operator` | stock 3.1.0 operator manifests, synced with ServerSideApply |
| `deploy-argocd/cluster/cr.yaml` | `pg-cluster` | stock `deploy/cr.yaml` 3.1.0 with PostgreSQL 17 (`postgresVersion: 17`, image `17.11.1-1`) |
| `deploy-argocd/ops/*.yaml` | `pg-ops` | `PerconaPGBackup` / `PerconaPGRestore` / `PerconaPGUpgrade` scenarios |

Scenario files are kept as `*.yaml.disabled`; rename to `*.yaml` and push to run one,
rename back to remove the object (the app has `prune: true`).

The Application manifests themselves are not in this repo, see
`experiments/PGARGOCD/argocd-apps/` and the test plan next to it.
