https://production-gitops.dev/guides/cp4i/mq/cluster-config/gitops-tekton-argocd/

# Configuring the cluster for GitOps
# Setup GitOps

export GIT_ORG=tutorial-org-1
echo $GIT_ORG
export GIT_ROOT=$HOME/Documents/GitHub/$GIT_ORG-root
echo $GIT_ROOT

<!-- cd /Users/auay/Documents/GitHub/tutorial-org-1-root -->

tree . -L 1
cd multi-tenancy-gitops
tree . -L 1

#Installing ArgoCD

oc login --token=sha256~yQ3Y_5gSyE4W2j_98sGdX0yD26808i5AQZUM2FGNMqA --server=https://c115-e.jp-tok.containers.cloud.ibm.com:32365

oc apply -f setup/ocp4x/

while ! oc wait crd applications.argoproj.io --timeout=-1s --for=condition=Established  2>/dev/null; do sleep 30; done
while ! oc wait pod --timeout=-1s --for=condition=Ready --all -n openshift-gitops 2>/dev/null; do sleep 30; done

oc get clusterrole custom-argocd-cluster-argocd-application-controller
oc get clusterrolebinding openshift-gitops-argocd-application-controller
oc get clusterrolebinding openshift-gitops-cntk-argocd-application-controller

oc delete gitopsservice cluster || true

#Creating a custom instance
cat setup/ocp4x/argocd-instance/argocd-instance.yaml

oc apply -f setup/ocp4x/argocd-instance/ -n openshift-gitops
while ! oc wait pod --timeout=-1s --for=condition=ContainersReady -l app.kubernetes.io/name=openshift-gitops-cntk-server -n openshift-gitops > /dev/null; do sleep 30; done

oc get route openshift-gitops-cntk-server -n openshift-gitops -o jsonpath='{"https://"}{.spec.host}{"\n"}'

oc extract secret/openshift-gitops-cntk-cluster -n openshift-gitops --keys="admin.password" --to=-

#Configuring the cluster infrastructure
#The sample GitOps repository
oc login --token=<token> --server=<server>
cd $GIT_ROOT
cd multi-tenancy-gitops
tree . -d -L 2
tree ./0-bootstrap/ -d -L 2
tree ./0-bootstrap/single-cluster/ -L 2
tree 0-bootstrap/single-cluster/1-infra/

#Tailor multi-tenancy-gitops

#Connect ArgoCD

#Customizing the bootstrap

#Understanding Kustomize

#More on ArgoCD

#Dynamic updates

#Configuration drift


#Installing services with ArgoCD
#Pre-requisites
export IBM_ENTITLEMENT_KEY=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJJQk0gTWFya2V0cGxhY2UiLCJpYXQiOjE2NTQxNjIzODYsImp0aSI6ImZhNDMxYzdiOTIxMjRjNDFiMGFkMWNiMWE2MjBhYjEyIn0.YvVPLoo8q60Oj5VhgHyRbi6hVRA0h5MbcHDSUeWj0lo

oc new-project tools || true
oc create secret docker-registry ibm-entitlement-key -n tools \
--docker-username=cp \
--docker-password="$IBM_ENTITLEMENT_KEY" \
--docker-server=cp.icr.io

#Installing Tekton for GitOps
export GIT_ORG=tutorial-org-1
export GIT_BRANCH=master
export GIT_ROOT=$HOME/Documents/GitHub/$GIT_ORG-root
cd $GIT_ROOT
cd multi-tenancy-gitops

echo $GIT_BRANCH
echo $GIT_ORG
echo $GIT_ROOT

<!-- export GIT_BRANCH=master
export GIT_ORG=<your organization name>
export GIT_ROOT=$HOME/git/$GIT_ORG-root -->

#Deploy services to the cluster



#Preparing for application componen
#Explore the -apps repository
#ArgoCD example
#Tailor the -apps repository

#Building MQ Queue Managers
#The sample queue manager repository
#Install the kubeseal operator into the cluster
#Configure access to IBM Entitled Registry
#Configure connection to the IBM Entitled Registry
export IBM_ENTITLEMENT_KEY=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJJQk0gTWFya2V0cGxhY2UiLCJpYXQiOjE2NTQxNjIzODYsImp0aSI6ImZhNDMxYzdiOTIxMjRjNDFiMGFkMWNiMWE2MjBhYjEyIn0.YvVPLoo8q60Oj5VhgHyRbi6hVRA0h5MbcHDSUeWj0lo

#Configure the pipeline for QM1 source repository
export GIT_TOKEN=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
export GIT_USER=phaithoona
#Deploy applications to the cluster¶

#Running the Pipeline
#Run the queue manager pipeline
Explore the pipeline
Understanding the QM1 kustomize resources

# Deploying and using the queue manager
## ArgoCD application for QM1
## Explore the deployed Kubernetes resources for QM1

# Continuous updates
