# Coverity Helm chart

## Notes

This script is unsupported; it is provided only as a reference.
There are many ways to deploy Coverity; this merely demonstrates one possible method.
This helm deploy script is specific to infra deployed through this project.  It will not work with different infra.
If deploying to different infra, you will have to modify this script.
Users of this script must be familiar with the details of their infra in order to modify this script correctly.
Any modifications to this script will also not be supported.

## Run the terraform output script

Run this [script](../environment/get-tf-outputs.sh) to get the required values for the deployment.

```bash
export COVERITY_CLUSTER_NAME=unique-prefix-cluster
export COVERITY_CLUSTER_REGION=???
export GCP_PROJECT_ID=???
export COVERITY_PGHOST=???
export COVERITY_PGUSER=postgres
export COVERITY_PGPASSWORD=???
export COVERITY_GCS_BUCKET_NAME=???
export COVERITY_GCS_SERVICE_ACCOUNT_FILE=???
```

## Helm chart install

Copy in a license:

```bash
cp path/to/license.dat .
```

Set environment variables:
```bash
# these values all come from your terraform output script
#   check the output to get the correct values
export COVERITY_CLUSTER_NAME=???
export COVERITY_CLUSTER_REGION=???
export GCP_PROJECT_ID=???
export COVERITY_PGHOST=???
export COVERITY_PGUSER=postgres
export COVERITY_PGPASSWORD=???
export COVERITY_GCS_BUCKET_NAME=???
export COVERITY_GCS_SERVICE_ACCOUNT_FILE=???

## Set additional env values
export COVERITY_NS=unique-prefix
```

Run deploy script:
```bash
./deploy.sh
```


## Access UI

### Find the HOSTS and ADDRESS details

Get the host name and address from your ingress object:

```bash
$ kubectl get ingress -n unique-prefix
NAME      CLASS    HOSTS                              ADDRESS         PORTS     AGE
unique-prefix   <none>   ???   ???   80, 443   12m
```

### Update your /etc/hosts file

Using the IP address and host from the above step, add this entry to your /etc/hosts file: (i.e. `sudo emacs /etc/hosts`)

```bash
???  ???
```

### Visit host in web browser

Open https://???:443 in your browser.