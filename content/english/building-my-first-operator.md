+++
title = 'Building My First Operator'
url = 'post/building-my-first-operator'
date = 2024-04-28T16:05:00+02:00
Tags = ["kubernetes","operators"]
Categories = ["operations","kubernetes"]
draft = true
+++

## Introduction
[Kubernetes Operators](https://kubernetes.io/docs/concepts/extend-kubernetes/operator/) is the kubernetes native way to extend capabilities of kubernetes to suit your needs. You might have already been familiar with some commonly available operators like [Prometheus Operator](https://prometheus-operator.dev/) or [Certmanager Operator](https://cert-manager.io/docs/installation/operator-lifecycle-manager/). The prometheus operators allows you to create and manage Prometheus and it's auxiliary resources in kubernetes with YAML manifest files. The Certmanager Operator allows you to install and setup cert-manager and certificates with YAML manifest files.

You can make use of the Operator pattern to automate the some tedious operations within and outside kubernetes.

Kubernetes' main building block is it's API server, which allows you to interact with the kubernetes ecosystem in a declarative way. Every `kubectl` command you run in turns calls the kube-apiserver in the background and sends some kind of CRUD calls.

## Why Kubebuilder?
There are multiple frameworks to build a kubernetes operator like [kubebuilder](https://book.kubebuilder.io/), [operator-sdk](https://sdk.operatorframework.io/), [shell-operator](https://github.com/flant/shell-operator) to name a few. I chose to go with kubebuilder since, it's supported by kubernetes special interest group or SIG. Kubebuild is built on top of controller-runtime and controller-tools libraries. They also have a well explained example in their website.

Kubebuild lets you bootstrap your operators very easily. Run a few commands and you are good to write your code in golang.

## Installing kubebuilder
To install kubebuilder, you can run download the kubebuilder binary from their git [repository](https://github.com/kubernetes-sigs/kubebuilder/releases).
or run the following command
```bash
curl -L -o kubebuilder "https://go.kubebuilder.io/dl/latest/$(go env GOOS)/$(go env GOARCH)"
chmod +x kubebuilder && sudo mv kubebuilder /usr/local/bin/
```
