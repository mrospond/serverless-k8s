# Serverless Kubernetes-based Resource Manager

Course work for Vrije Universiteit Amsterdam's X_400130 Distributed Systems (2024).

# Prerequisites

1. Install [Docker](https://www.docker.com/).
2. Have a [Docker Hub](https://hub.docker.com/) account for pushing the Docker image.
3. Install Knative:
   1. Install [kind](https://kind.sigs.k8s.io/docs/user/quick-start).
   2. Install [Kubernetes CLI (kubectl)](https://kubernetes.io/docs/tasks/tools/).
   3. Install [Knative](https://knative.dev/docs/getting-started/quickstart-install/). We recommend install with the `quickstart` plugin.
   4. Install [Knative Serving components](https://knative.dev/docs/install/yaml-install/serving/install-serving-with-yaml/#install-the-knative-serving-component), [networking layer](https://knative.dev/docs/install/yaml-install/serving/install-serving-with-yaml/#install-a-networking-layer) and [configure DNS](https://knative.dev/docs/install/yaml-install/serving/install-serving-with-yaml/#configure-dns). You can also do it with `make install-knative-dependencies`.

# Setup

1. Update the variable `NAMESPACE=YOUR_NAMESPACE_HERE` in `Makefile` to your Docker namespace.
2. Run the following command to update all namespaces in the services yaml.

```sh
make update-namespace
```

3. Obtain the etcd certificates for allowing the services to have access to it.

```sh
make get-etcd-certs
```

4. Build and deploy the services.

```sh
make build-deploy-all
```

5. Find the URL for accessing the services.

```sh
kubectl get ksvc
```

6. Take down the services.

```sh
make take-down-all
```

# Useful Commands

## Checking etcd configuration

```sh
docker exec -it knative-control-plane sh
cat /etc/kubernetes/manifests/etcd.yaml
```

# Acknowledgments

This project makes use of Auger maintained by the etcd Development and Communities. Please check out their work [etcd-io/auger](https://github.com/etcd-io/auger).
