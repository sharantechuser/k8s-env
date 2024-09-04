# <p style="color:teal"> Environment Variables in Kubernetes Pods

Describes how ENV variables are being used in kuberenetes POD containers. 

## <p style="color:teal">Authors</p>

- [@sharantechuser](https://www.github.com/sharantechuser)


## <p style="color:teal">Install minikube & kubectl</p>
In prerequisites, install Homebrew


#### 1. Install minikube via Homebrew

```sh
    # Install minikube
    brew install minikube

    # Verify minikube
    minikube version
```

#### 2. Install kubectl via Homebrew

```sh
    # Install kubectl
    brew install kubectl

    # Verify kubectl
    kubectl version
```


## <p style="color:teal">Setup two nodes kubernetes cluster 

Setting up multi nodes kuberenetes cluster using minikube


#### 1. Start minikube cluster
1. This command creates and starts a Minikube VM or container with a Kubernetes cluster.
It creates 2 nodes one is master node and another one is worker node

```sh
    minikube start --nodes 2 -p local-k8s-cluster --driver=docker
```

#### 2. Verify the nodes
```sh
    kubectl get nodes
```
System shows two nodes *local-k8s-cluster* and *local-k8s-cluster-m02*  in Ready state.

#### 3. Verify cluster status 
```sh
    minikube status -p local-k8s-cluster
```

## <p style="color:teal">Build docker image</p>

#### 1. create pod manifest i.e nginx-pod.yaml
```
    docker build -t myweb .
```

## <p style="color:teal">Pods Deployments in kubernetes cluster</p>

#### 1. create pod manifest i.e nginx-pod.yaml
```
    apiVersion: v1
    kind: Pod
    metadata:
    name: env-vars-dev
    labels:
        purpose: env-vars-dev
    spec:
    containers:
    - name: env-vars-dev-container
        image: nginx
        env:
        - name: PROFILE_NAME
        value: "dev"
        - name: APP_VERSION
        value: "v1"
```

#### 2. create deployment
```sh
    kubectl apply -f nginx.yaml
```


#### 3. Verify the deployments and services
```sh
    kubectl get pods
```

## <p style="color:teal">Disable firewall</p>

```sh
    # disable firewall and allow the port 8001
    sudo firewall-cmd --zone=public --add-port=8001/tcp --permanent

    # After disabled the firewall, reload firewall settingd
    sudo firewall-cmd --reload
```

## <p style="color:teal">Kubernetes dashboard</p>

```sh
    # This create proxy URL for kubernetes dashboard
    minikube dashboard --url -p local-k8s-cluster
```

Open the URL from above response

## <p style="color:teal">Test the application</p>
<p>Test with below CURL command.</p>

```http
    curl http://localhost:30007
```