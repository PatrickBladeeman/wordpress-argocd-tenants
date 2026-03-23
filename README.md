WordPress ArgoCD Tenants
========================

This repo is the tenant-facing GitOps input for a KubePlus + ArgoCD demo.

It assumes these prerequisites are already in place on the target cluster:

- KubePlus is installed.
- A provider has already applied the `GitopsWPService` `ResourceComposition`.
- The CRD `gitopswpservices.platformapi.kubeplus` exists.
- ArgoCD is installed in the cluster.

What this repo manages
----------------------

- Tenant instances of `GitopsWPService`
- The ArgoCD `Application` that syncs those tenant instances

What this repo does not manage
------------------------------

- KubePlus installation
- ArgoCD installation
- Provider-only `ResourceComposition` creation

Quick start
-----------

1. Update `argocd-tenants-app.yaml` with your Git repo URL, branch, and target namespace.
2. Apply the ArgoCD application:

   `kubectl apply -f argocd-tenants-app.yaml -n argocd`

3. Verify tenant creation:

   `kubectl get gitopswpservices.platformapi.kubeplus -n default`
   `kubectl get ns | grep wp-`
   `kubectl get pods -n wp-tenant1`
   `kubectl get pods -n wp-tenant2`
