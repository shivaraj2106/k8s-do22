installation:
git clone https://github.com/kubernetes/autoscaler.git                        ─╯
cd autoscaler/vertical-pod-autoscaler
git checkout origin/vpa-release-1.0
REGISTRY=registry.k8s.io/autoscaling TAG=1.0.0 ./hack/vpa-process-yamls.sh apply


apply hamster:
kubectl apply -f https://github.com/kubernetes/autoscaler/raw/master/vertical-pod-autoscaler/examples/hamster.yaml
kubectl get pods -l app=hamster


kubectl get pods -w -l app=hamster

kubectl get pod -l app=hamster -o jsonpath='{.items[0].spec.containers[0].resources}'