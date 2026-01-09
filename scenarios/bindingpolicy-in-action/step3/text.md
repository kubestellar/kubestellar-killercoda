# Change Intent: Update BindingPolicy

In this step, you will change **only the BindingPolicy** and observe how workload placement changes automatically.

The workload itself will **not** be modified or redeployed.

---

## Remove the existing BindingPolicy

First, delete the BindingPolicy that targets `wec1`.

```bash
kubectl delete bindingpolicy demo-nginx-to-wec1
```{}

---

## Define a new BindingPolicy for wec2

Create a new BindingPolicy that targets **only `wec2`**.

```bash
cat <<EOF > bindingpolicy-wec2.yaml
apiVersion: control.kubestellar.io/v1alpha1
kind: BindingPolicy
metadata:
  name: demo-nginx-to-wec2
spec:
  clusterSelectors:
  - matchLabels:
      kubestellar.io/cluster-name: wec2
  downsync:
  - objectSelectors:
    - matchLabels:
        app: demo-nginx
EOF
```{}

---

## Apply the updated BindingPolicy

Apply the new policy from the control environment:

```bash
kubectl apply -f bindingpolicy-wec2.yaml
```{}

> The workload manifest has **not** changed.

---

## Observe workload movement

Verify that the workload is **no longer running on `wec1`**:

```bash
kubectl --context wec1 get pods
```{}

You should see **no pods** for this workload on `wec1`.

Now verify that the workload is running on **`wec2`**:

```bash
kubectl --context wec2 get pods
```{}

You should see the `demo-nginx` pod running on `wec2`.

---

## Key takeaway

- Workload placement changed without redeploying the workload
- The only change was to **intent**, expressed as a BindingPolicy
- This is fundamentally different from traditional multi-cluster workflows

Continue to the final step to summarize what you learned.
