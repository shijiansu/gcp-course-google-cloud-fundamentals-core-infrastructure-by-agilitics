
```shell
# For your convenience, place the zone that Qwiklabs assigned you to into an environment variable called MY_ZONE. At the Cloud Shell prompt, type this partial command:
export MY_ZONE=
# followed by the zone that Qwiklabs assigned you to. Your complete command will look like this:
export MY_ZONE=us-central1-f
export DEVSHELL_PROJECT_ID=xxxxxxxxxxxx
# At the Cloud Shell prompt, download an editable Deployment Manager template:
gsutil cp gs://cloud-training/gcpfcoreinfra/mydeploy.yaml mydeploy.yaml
# Insert your Google Cloud Platform project ID into the file in place of the string PROJECT_ID using this command:
sed -i -e 's/PROJECT_ID/'$DEVSHELL_PROJECT_ID/ mydeploy.yaml
# Insert your assigned Google Cloud Platform zone into the file in place of the string ZONE using this command:
sed -i -e 's/ZONE/'$MY_ZONE/ mydeploy.yaml
```

```yaml
# cat mydeploy.yaml
resources:
  - name: my-vm
    type: compute.v1.instance
    properties:
      zone: us-central1-a
      machineType: zones/us-central1-a/machineTypes/n1-standard-1
      metadata:
        items:
        - key: startup-script
          value: "apt-get update"
      disks:
      - deviceName: boot
        type: PERSISTENT
        boot: true
        autoDelete: true
        initializeParams:
          sourceImage: https://www.googleapis.com/compute/v1/projects/debian-cloud/global/images/debian-9-stretch-v20180806
      networkInterfaces:
      - network: https://www.googleapis.com/compute/v1/projects/qwiklabs-gcp-dcdf854d278b50cd/global/networks/default
        accessConfigs:
        - name: External NAT
          type: ONE_TO_ONE_NAT
```

```shell
# Build a deployment from the template:
gcloud deployment-manager deployments create my-first-depl --config mydeploy.yaml

# nano mydeploy.yaml
      value: "apt-get update; apt-get install nginx-light -y"

# Return to your Cloud Shell prompt. Enter this command to cause Deployment Manager to update your deployment to install the new startup script:
gcloud deployment-manager deployments update my-first-depl --config mydeploy.yaml
```
