# Mosquitto MQTT

Lightweight MQQT Broker

## Sources

https://mosquitto.org
https://github.com/eclipse/mosquitto


### Setup Sealed Secrets

You have to have Selead Secret operator running for Sealed Secrets to work!

Generate all needed Secrets locally and seal them, so that you are able to store it in GIT. Just store the yaml Files with the sealed Secrets,
do not save your Real Passwords or the Secrets from Kubernetes, they are just Base64 Encoded, its easy to decode and therefore not safe!
For sealing you have to install Sealed Secrets from Bitnami. Find a tutorial with Kustomize and Argo CD in my repo [Sealed Secrets Kustomize](https://github.com/wep4you/sealed-secrets-kustomize) 

A sample password file is stored in  (overlays/sample/password_file.txt). Change the settings there and use strong passwors. Also make shure,
to not check in this file, this should only be present locally!

Now generate a Sealed Secret for your file, this new generated file could be checked in.

    kubectl --namespace mqtt create secret generic mosquitto-password --dry-run=client \
    --from-file password_file.txt=./overlays/sample/password_file.txt \
    --output json | kubeseal | tee overlays/sample/sealedsecret.yml    

## Install with Argo CD

Use a central repository which links to all Apps which has to be deployed,
and add the App desciption there, or deploy the App for manually.
Find a sample in my [App of Apps Repo](https://github.com/wep4you/k8s-apps.git),

## Install manual with kubectl

To add your own configuration, copy ```overlays/sample``` to a new folder and change the files to your needs.
It's standard Kustomize format you can use.

    ```
    kubectl apply -k overlays/sample
    ```