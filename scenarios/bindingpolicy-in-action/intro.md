# KubeStellar: BindingPolicy in Action

In this scenario, you will see **why BindingPolicy is central to how KubeStellar works**.

In traditional multi-cluster environments, changing where a workload runs usually means:
- Editing manifests
- Reapplying resources
- Managing clusters individually

KubeStellar takes a different approach.

---

## What you will do

In this scenario, you will:

- Install KubeStellar in a fresh environment
- Create two Workload Execution Clusters (WECs)
- Deploy a workload **once**
- Use a BindingPolicy to control where the workload runs
- Change workload placement **without changing the workload**

---

## What you will NOT do

- You will not redeploy the workload
- You will not apply manifests directly to WEC clusters
- You will not manage clusters one by one

All placement changes will be driven by **policy**, not deployment logic.

---

## Key idea to keep in mind

> **BindingPolicy expresses intent.**  
> When intent changes, behavior changes automatically.

In the next step, you will install KubeStellar and set up a multi-cluster environment.
