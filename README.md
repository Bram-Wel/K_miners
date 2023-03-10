# Kubernetes-Cryptocurrency-Mining

# Introduction
The aim of this project is to have a Kubernetes cluster maintaining Cryptocurrency Mining Containers automatically. It is a way to test my understanding of docker and kuberenetes.

# Resources and Prerequisites

ZCash miner docker image

To run local Vagrant Kops Box:
- Install Vagrant: https://www.vagrantup.com/downloads.html
- Have your terminal in the __kops-vagrant-box__ folder and run `vagrant up`.

# Architecture

### Local

Kops Vagrant Box configured to AWS to create and maintain Kubernetes cluster on AWS.

# How to Deploy
To create Kubernetes cluster on AWS with the Kops Vagrant Box:

    kops create cluster --name=MyKubernetesDomain --state=s3://MyAWSS3Bucket --zones=us-east-1c --node-count=2 --node-size=t2.micro --master-size=t2.micro --dns-zone=MyKubernetesDomain

Note that once this runs, to complete you must any further commands with the --state=s3://MyAWSS3Bucket.

To deploy the app, first copy the __zcashminer-deployment.yml__ to your Kops Vagrant Box. Then run:

    kubectl create namespace zcashminer
	kubectl create -f zcashminer-deployment.yml
	
# Useful Commands

### Commands to operate on containers

Status:

    kubectl exec --namespace=zcashminer CONTAINERNAME zcash-cli getinfo

Generate z-address for tranfer:

    kubectl exec --namespace=zcashminer CONTAINERNAME zcash-cli z_getnewaddress
	
Generate z-addresses in wallet:

    kubectl exec --namespace=zcashminer CONTAINERNAME zcash-cli z_listaddresses

Get balances:

    docker exec CONTAINERID zcash-cli z_getnewaddress ${ADDRESS}
	
# Current Accomplishments
A list of milestones and accomplishments:
- Dockerfile is located in docker-template/Dockerfile. Image is pushed to Docker Hub.
- Changed miner from etherium to zcash
- Cluster Deployed on AWS with 2 t2.micro nodes each running one container.
- Kubernetes Dashboard on public domain
- Updated kops to 1.6.0 (released on May 16, 2022)
