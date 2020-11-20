# SSO to ANY PingFederate environment with My Ping

## Prerequisites

Here are the items you will need for this tutorial.

- Git
- devops user and key
- ping-devops tool
- helm *
- MyPing (Trial) Account
- AWS EKS cluster access *
- k9s

---

1. [Register](https://pingidentity-devops.gitbook.io/devops/getstarted/prod-license#obtaining-a-ping-identity-devops-user-and-key) for a PingIdentity customer account to obtain your DevOps user and key.
2. [Install](https://pingidentity-devops.gitbook.io/devops/devopsutils/pingdevopsutil#installation-and-upgrades) and configure the devops tool.
3. [Create](https://helm.pingidentity.com/getting-started/#create-ping-devops-secret) a Ping DevOps secret.
4. [Install](https://helm.pingidentity.com/getting-started/#install-helm-3) helm 3.
   a. Continue to follow the instructions to add the Ping DevOps repo and charts.   
5. Install k9s
   a. `brew install derailed/k9s/k9s`
6. Create a workspace and clone the myping-enablement workspace.
   a. > `cd ~ `
   b. > `mkdir gsa-enablement`
   c. > `cd gsa-enablement`
   d. > git clone 

## Setup My Ping

Lets setup My Ping to enable SSO to your PF environment.

1. First we will need to update the PingOne directory schema and add a "role" to your My Ping administrator user.
   
    a. Here are some awesome [instructions](https://confluence.pingidentity.com/display/~aldenshiverick/My+Ping+SSO+to+PingFederate) that will walk you through the process.
2. Create an PingOne Application Connection for the PingFederate Admin Console. You can follow the same instruction link from step 1.
   
    a. Note: When first providing the redirect uri value, you can use a temporary value such as: https://localhost. This will allow you to advance the application creation workflow. You can add the correct value later, once it is known.

## Configure PF helm values

Now that you have the metadata for your PingFederate administration console OIDC client.

1. Open the `p1-plus-pf.yaml` file in your favorite editor.
2. Provide the PingOne OIDC settings to your yaml file.

## Lets install the helm chart.

 1. Run the following command: > `helm install p1-sso-<your-username> pingidentity/devops -f p1-plus-pf.yaml`
 2. Fire up k9s. In another terminal window/tab run the following command:  > `k9s`
 3. Back to the k9s interface and lets locate the ingress host value for the pingfederate admin console.
 4. Access My Ping and lets add another environment that includes PingFederate. 
    a. Build the URL using the ingress host value from step 3.
    b. ex: https://pingfederate-admin.p1-plus-pf.ping-devops.com/pingfederate/app?service=finishsso




