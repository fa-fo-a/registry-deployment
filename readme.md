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
- `kubectl apply -f deployment.yaml`<br>
make sure it works (get pods) - if not, something of previos was done wrong. If error with image pull, cause no latest tag expected in your set up you may fix it by optional commands below
- `kubectl apply -f service.yaml`
- edit issuer.yaml by placing your mail in placeholder
- edit ingress.yaml by replacing placeholders of domain in there to preferred one
- `kubectl apply -f ingress.yaml`
  - keep in mind that secrets have to be [base64-encoded strings](https://kubernetes.io/docs/concepts/configuration/secret/#restriction-names-data).
  -  To apply them [here's example how to](https://kubernetes.io/docs/concepts/configuration/secret/#use-cases)<br />
Do not forget to `kubectl apply -f secrets.yaml`
- (optional) if you apply secrets you may apply (as i do) them as env variables in container. check `deployment.yaml`, uncomment and tweak according to own needs example in there, reapply deployment

# knowledge sources
- https://kubernetes.io/docs/tasks/configure-pod-container/pull-image-private-registry/
- https://cert-manager.io/docs/troubleshooting/acme/
- https://kubernetes.io/docs/concepts/configuration/secret/
