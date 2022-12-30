# Kubernetes terminology


## Kubernete Cluster

A collection of nodes + a master to manage them. 

## Node 

A virtual machine that will run our containers

## Pod 

Pod wraps up one or many containers. More or less a running container. Technically, a pod can run multiple containers. 

## Deployment

Monitors a set of pods, make sure they are running and restarts them, if they crash

## Service 

Provides an easy-to-remember URL to access running container 

## Kubernetes Config Files

* tell Kubernetes about the different Deployments, Pods and Services (referred to as 'Objects') that we want to create
* written in YAML syntax

## Common Kubectl Commands

    // list all running pods
    kubectl get pods

    // execute the given comman in a running pod
    kubectl exec -it [pod_name] [cmd]

    // print out logs from the given pod
    kubctl logs [pod_name]

    // delete given pod
    kubectl delete pod [pod_name]

    // process config file in current directory
    kubectl apply -f [config file name e.g. posts.yaml]

    // print out some information about the running pod
    kubectl describe pod [pod_name]



## Deployments Commands

    // list all running deployments
    kubectl get deployments

    // print out details about a specific Deployment
    kubectl describe deployment [name of deployment]

    // create a deployment our of yaml file
    kubectl apply -f [yaml file name]

    // deleting deployment and all associated pods
    kubectl delete deployment [name of deployment]
