TODO: add charts and values files from installation folder + turn installer parameters below into values files in the cc/secrets repo. They are passed to helm as commandline paramters

install.sh  --deployment-type=cloud --namespace=vora --docker-registry=hub.global.cloud.sap --docker-repository-domain=monsoon --vora-admin-username=admin --vora-admin-password=***

List of issues and workarounds
------------------------------

Kubernetes 1.9 not supported yet:
* change regex in install script to accept version 1.9

Generated pipeline images produced by modeller are always published into 'vora' organisation
* Added a local registry (unprotected), exposed via node port

Generated pipeline images always use registry host name as respository name
* Added a DNS entry pointing to registry IP address 

Pipeline modeller cannot build images because docker build has no internet
* Changed deployment vflow-... to use dnsPolicy: ClusterFirstWithHostNet (instead of ClusterFirst)
* Change docker daemon to use bride-network by default (instead of None). In /etc/systemd/system/docker.service.d/20-docker-opts.conf
change --bridge parameter to docker0
