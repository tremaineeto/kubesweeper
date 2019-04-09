# Kythera Kubernetes Deployment Crawler 

Automatically crawls through resources in a lab Kubernetes cluster and acts according to [certain conditions outlined here](#configuration-defaults). As of now, Kubernetes Deployment Crawler will delete deployments and their associated resources if the waiting reason and/or pod restart counts dictate.

If your lab Kubernetes clusters are filling up with non-Running pods, then the Kubernetes Deployment Crawler's automatic deletion
can assist. Future iterations of this project can involve other actions based on crawling through Kubernetes cluster resources, such as generating reports per namespace without actually deleting. 

<p align="center">
    <a href="https://github.com/att-cloudnative-labs/kythera-k8s-deployment-crawler/graphs/contributors" alt="Contributors">
		<img src="https://img.shields.io/github/contributors/att-cloudnative-labs/kythera-k8s-deployment-crawler.svg">
	</a>
	<a href="https://github.com/att-cloudnative-labs/kythera-k8s-deployment-crawler/commits/master" alt="Commits">
		<img src="https://img.shields.io/github/commit-activity/m/att-cloudnative-labs/kythera-k8s-deployment-crawler.svg">
	</a>
	<a href="https://github.com/att-cloudnative-labs/kythera-k8s-deployment-crawler/pulls" alt="Open pull requests">
		<img src="https://img.shields.io/github/issues-pr-raw/att-cloudnative-labs/kythera-k8s-deployment-crawler.svg">
	</a>
	<a href="https://github.com/att-cloudnative-labs/kythera-k8s-deployment-crawler/pulls" alt="Closed pull requests">
    	<img src="https://img.shields.io/github/issues-pr-closed-raw/att-cloudnative-labs/kythera-k8s-deployment-crawler.svg">
	</a>
	<a href="https://github.com/att-cloudnative-labs/kythera-k8s-deployment-crawler/issues" alt="Issues">
		<img src="https://img.shields.io/github/issues-raw/att-cloudnative-labs/kythera-k8s-deployment-crawler.svg">
	</a>
	</p>
<p align="center">
	<a href="https://github.com/att-cloudnative-labs/kythera-k8s-deployment-crawler/stargazers" alt="Stars">
		<img src="https://img.shields.io/github/stars/att-cloudnative-labs/kythera-k8s-deployment-crawler.svg?style=social">
	</a>	
	<a href="https://github.com/att-cloudnative-labs/kythera-k8s-deployment-crawler/watchers" alt="Watchers">
		<img src="https://img.shields.io/github/watchers/att-cloudnative-labs/kythera-k8s-deployment-crawler.svg?style=social">
	</a>	
	<a href="https://github.com/att-cloudnative-labs/kythera-k8s-deployment-crawler/network/members" alt="Forks">
		<img src="https://img.shields.io/github/forks/att-cloudnative-labs/kythera-k8s-deployment-crawler.svg?style=social">
	</a>	
</p>
<p align="center">
  <a href="https://goreportcard.com/badge/github.com/att-cloudnative-labs/kythera-k8s-deployment-crawler" alt="Go Report Card">
    <img src="https://goreportcard.com/badge/github.com/att-cloudnative-labs/kythera-k8s-deployment-crawler">
  </a>	
</p>

## Deployment

First, build the Docker image.

```bash
$ docker build -t kubecrawler .
```

Deploy the image in your Kubernetes cluster as a Kubernetes CronJob or as a Knative Cron Job Source.

### Deploying as a Kubernetes CronJob

In the appropriate lab Kubernetes cluster, copy over the ```install``` directory, and then run:

```bash
$ kubectl apply -f install/
```

This will create the following Kubernetes resources: Namespace (*kythera-system*), ServiceAccount, ClusterRole, ClusterRoleBinding, and finally, CronJob. 

The default CronJob is configured to run at 10:00 A.M. once every day. In order to change this, edit the CronJob resource's cron expression.

## Configuration Defaults

Under the ```configs``` folder, the ```config.yaml``` has the following default configurations:

* Pod waiting reasons
  * CrashLoopBackOff
  * ImagePullBackOff
  * ErrImagePull
  * Completed
  * Failed
* Pod restart threshold
  * 144
    * If the pod restart threshold is at least this number *and* has a pod waiting reason of ```CrashLoopBackOff```, then Kubernetes Deployment Crawler will delete the associated resources


## Contributing

1. [Fork Kubernetes Deployment Cleaner](https://github.com/att-cloudnative-labs/kythera-k8s-deployment-crawler/fork)
2. Create your feature branch (`git checkout -b feature/fooBar`)
3. Commit your changes (`git commit -am 'Add some fooBar'`)
4. Push to the branch (`git push origin feature/fooBar`)
5. Create a new Pull Request

## Additional info

<p align="center">
  <a href="https://kythera.io" alt="Kythera">
    <img src="./images/kythera.png" height="40%" width="40%">
  </a>	
</p>

Part of Kythera: Kubernetes Projects for Developers and Operators – [kythera.io](https://kythera.io). 

<p align="center">
  <a href="https://github.com/att-cloudnative-labs" alt="AT&T Cloud Native Labs">
    <img src="./images/cloud_native_labs.png" height="50%" width="50%">
  </a>	
</p>

Maintained and in-use by the Platform Team @ AT&T Entertainment Cloud Native Labs.

Distributed under the AT&T MIT license. See ``LICENSE`` for more information.
