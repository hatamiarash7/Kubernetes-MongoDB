# Kubernetes MongoDB
 Deploy MongoDB replica set in Kubernetes

## Prerequisites

You should disable THP ( transparent huge pages ). There is many ways to do that.
* Write a startup script using `gcr.io/google-containers/startup-script`
* Use `busybox` image and make DaemonSet to do this in all deployments.

This one is not a critical problem. `gcr.io/google-containers/startup-scriptis` 12.5MB, but since we are essentially just running a shell script, it can be changed to a slimmer image, like `busybox` which has an image size of 1.15MB. Of course `busybox` is lacking the startup functionality of `gcr.io/google-containers/startup-script`. For this we can utilize `initContainers` which were unavailable at the time.

Use [this one](https://gist.github.com/hatamiarash7/ae7fcc9c7155722df77ebbf459d467f5)

```
kubectl apply -f https://gist.githubusercontent.com/hatamiarash7/ae7fcc9c7155722df77ebbf459d467f5/raw/178d7bb870a266f86de2e881d795ebf57f6e6d77/daemon.yml
```

## Install

```
kubectl apply -f replicaset.yml
kubectl apply -f services.yml
```

## Usage

```
mongodb://localhost:27017/?readPreference=primary&ssl=false
```
