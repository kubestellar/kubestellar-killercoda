# Initial Placement Using BindingPolicy

In this step, you will deploy a workload **once** and use a **BindingPolicy** to place it on **one Workload Execution Cluster (WEC)**.

Initially, the workload will run only on **wec1**.

---

## Define the workload

Create a simple Deployment.  
This workload does not reference any cluster.

```bash
cat <<EOF > workload.yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: demo-nginx
  namespace: default
spec:
  replicas: 1
  selector:
    matchLabels:
      app: demo-nginx
  template:
    metadata:
      labels:
        app: demo-nginx
    spec:
      containers:
      - name: nginx
        image: nginx:stable
        ports:
        - containerPort: 80
EOF
```{}

---

## Define a BindingPolicy for a single WEC

Create a BindingPolicy that targets **only `wec1`**.

```bash
cat <<EOF > bindingpolicy-wec1.yaml
apiVersion: control.kubestellar.io/v1alpha1
kind: BindingPolicy
metadata:
  name: demo-nginx-to-wec1
spec:
  clusterSelectors:
  - matchLabels:
      kubestellar.io/cluster-name: wec1
  downsync:
  - objectSelectors:
    - matchLabels:
        app: demo-nginx
EOF
```{}

---

## Apply the workload and policy

Apply both resources **once**, from the control environment.

```bash
kubectl apply -f workload.yaml
kubectl apply -f bindingpolicy-wec1.yaml
```{}

> ⚠️ Do **not** apply these manifests directly to `wec1`.
> KubeStellar handles distribution automatically.

---

## Observe workload placement

Verify that the workload is running on **wec1**:

```bash
kubectl --context wec1 get pods
```{}

You should see a `demo-nginx` pod running.

Now verify that the workload is **not** running on `wec2`:

```bash
kubectl --context wec2 get pods
```{}

You should see **no pods** for this workload on `wec2`.

---

## Key takeaway

- The workload was deployed **once**
- Placement was controlled entirely by **BindingPolicy**
- The workload runs only where the policy allows

In the next step, you will change **only the BindingPolicy** and observe how placement changes automatically.
