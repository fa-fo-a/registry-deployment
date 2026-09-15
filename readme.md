# prerequisites

Repository main goal is to get reused by author and, maybe, by people who find it useful. Currently author's setup is baremetal home server with [k3s](https://k3s.io) installed on it. So whole repository for sure works on k3s if folow installation guide below.<br>
As result of effort done you gonna get launched instance of application, with domain you configure and ssl above it

# installation
- Get the repo files, place them whenever it needed
- (optional) change namespace<br>
for handiness namespace in repo is "registry", so it can be replaced in any comfortable way by mass replace. If you want use default one - just remove namespace from every manifest from metadata.<br>
Keep in mind if you change namespace you will have to tweak accordingly some commands below
- (optional) change name<br>
same as with namespace app name in repo "registry". same can be replaced by mass replace
- apply namespace by `kubectl create namespace registry`<br>
heads up in here. if you changed namespace - tweak command accordingly
- `kubectl apply -f pvc.yaml`<br>
this creates a PersistentVolume backed by hostPath `/home/alex/registry` on the node, and a PersistentVolumeClaim bound to it, so registry data survives pod restarts. Change the `hostPath.path` if you want data stored elsewhere. Since hostPath ties data to a specific node, this only works reliably on a single-node cluster (e.g. k3s) unless you add a node affinity/selector
- `kubectl apply -f deployment.yaml`<br>
make sure it works (get pods) - if not, something of previos was done wrong. If error with image pull, cause no latest tag expected in your set up you may fix it by optional commands below
- `kubectl apply -f service.yaml`

# knowledge sources
- https://kubernetes.io/docs/tasks/configure-pod-container/pull-image-private-registry/
- https://cert-manager.io/docs/troubleshooting/acme/
- https://kubernetes.io/docs/concepts/configuration/secret/
