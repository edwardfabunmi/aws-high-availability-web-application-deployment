#!/bin/bash
set -e
# changing the Server hostname
#=============================
sudo hostnamectl set-hostname Jumper-Server-01

# updating the server
#====================
sudo apt update -y
sudo apt upgrade -y

# create a folder to mount to efs
#================================
mkdir -p /home/ubuntu/webserver

# installing EFS client dependencies
#====================================
sudo apt -y install nfs-common stunnel4 git binutils

# adding the efs acces point to fstab
#=====================================
sudo tee -a /etc/fstab > /dev/null <<EOF
fs-04f8361194a2bfdf4.efs.us-east-1.amazonaws.com:/ /home/ubuntu/webserver nfs4 nfsvers=4.1,rsize=1048576,wsize=1048576,hard,timeo=600,retrans=2,noresvport,_netdev 0 0
EOF

# mount efs
#===========
sudo mount -a

# connect to datadog
#===================

DD_API_KEY=27dd3cfe5f6fb36fa7eb640622cf7915 \
DD_APP_KEY=ddapp_fOwh3CllNTn9iQUNOxM4dxb2Umg925XTD9 \
DD_SITE="datadoghq.com" \
DD_APM_INSTRUMENTATION_ENABLED=host \
DD_APM_INSTRUMENTATION_LIBRARIES=java:1,python:4,js:5,php:1,dotnet:3,ruby:2,nginx:1 \
DD_APPSEC_ENABLED=true \
DD_IAST_ENABLED=true \
DD_APPSEC_SCA_ENABLED=true \
DD_RUNTIME_SECURITY_CONFIG_ENABLED=true \
DD_COMPLIANCE_CONFIG_ENABLED=true \
DD_SBOM_CONTAINER_IMAGE_ENABLED=true \
DD_SBOM_HOST_ENABLED=true \
DD_DATA_STREAMS_ENABLED=true \
DD_PROFILING_ENABLED=auto \
DD_ENV=dev \
DD_OTELCOLLECTOR_ENABLED=true \
DD_RUM_ENABLED=true \
DD_RUM_APPLICATION_ID=7d111228-031d-4ee2-ba43-62f6460f48b2 \
DD_RUM_CLIENT_TOKEN=pubfe00d654305e7abcc99942edbec0c666 \
DD_RUM_REMOTE_CONFIGURATION_ID=c31208eb-32fb-4b8a-9fe5-3ba1ab47898c \
DD_RUM_SITE=datadoghq.com \
DD_PRIVATE_ACTION_RUNNER_ENABLED=true \
DD_PRIVATE_ACTION_RUNNER_ACTIONS_ALLOWLIST=com.datadoghq.script.runPredefinedScript \
bash -c "$(curl -L https://install.datadoghq.com/scripts/install_script_agent7.sh)"
