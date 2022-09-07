# Mosquitto MQTT

Lightweight MQQT Broker

## Sources

https://mosquitto.org
https://github.com/eclipse/mosquitto

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