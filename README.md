# minikube-ppc64le-binary
minikube binary file

To install Minikube on Power, You should following these steps.  

### Install Docker

Add Repo :  
~~~sh
$ cat > /etc/yum.repos.d/docker.repo << EOF
[docker]
name=Docker
baseurl=http://ftp.unicamp.br/pub/ppc64el/rhel/7/docker-ppc64el/
enabled=1
gpgcheck=0
EOF
~~~

Install Docker :  
~~~sh
$ sudo yum install -y docker-ce
$ sudo systemctl enable docker
$ sudo systemctl start docker
$ sudo systemctl status docker
~~~  

### Install Kubectl
~~~sh
$ cat <<EOF > /etc/yum.repos.d/kubernetes.repo
[kubernetes]
name=Kubernetes
baseurl=https://packages.cloud.google.com/yum/repos/kubernetes-el7-ppc64le
enabled=1
gpgcheck=1
repo_gpgcheck=1
gpgkey=https://packages.cloud.google.com/yum/doc/yum-key.gpg https://packages.cloud.google.com/yum/doc/rpm-package-key.gpg
EOF
~~~

~~~sh
$ sudo yum install -y kubectl
~~~

### Install Minikube

~~~sh
$ wget https://github.com/GRuuuuu/minikube-ppc64le-binary/releases/download/v1.7.3/minikube
~~~

~~~sh
$ chmod +x minikube
$ ./minikube start --vm-driver=none
~~~

Result will be like this:  
~~~sh
* minikube v1.7.3 on Redhat 8.1 (ppc64le)
* Using the none driver based on user configuration
* Running on localhost (CPUs=4, Memory=7640MB, Disk=61424MB) ...
* OS release is Red Hat Enterprise Linux 8.1 (Ootpa)
* Preparing Kubernetes v1.17.3 on Docker 18.03.1-ce ...
    > kubelet.sha256: 65 B / 65 B [--------------------------] 100.00% ? p/s 0s
    > kubectl.sha256: 65 B / 65 B [--------------------------] 100.00% ? p/s 0s
    > kubeadm.sha256: 65 B / 65 B [--------------------------] 100.00% ? p/s 0s
    > kubeadm: 36.12 MiB / 36.12 MiB [---------------] 100.00% 73.03 MiB p/s 1s
    > kubectl: 40.00 MiB / 40.00 MiB [---------------] 100.00% 51.93 MiB p/s 1s
    > kubelet: 102.52 MiB / 102.52 MiB [-------------] 100.00% 55.16 MiB p/s 2s
* Launching Kubernetes ...
* Enabling addons: default-storageclass, storage-provisioner
* Configuring local host environment ...
*
! The 'none' driver provides limited isolation and may reduce system security and reliability.
! For more information, see:
  - https://minikube.sigs.k8s.io/docs/reference/drivers/none/
*
! kubectl and minikube configuration will be stored in /root
! To use kubectl or minikube commands as your own user, you may need to relocate them. For example, to overwrite your own settings, run:
*
  - sudo mv /root/.kube /root/.minikube $HOME
  - sudo chown -R $USER $HOME/.kube $HOME/.minikube
*
* This can also be done automatically by setting the env var CHANGE_MINIKUBE_NONE_USER=true
* Waiting for cluster to come online ...
* Done! kubectl is now configured to use "minikube"
* For best results, install kubectl: https://kubernetes.io/docs/tasks/tools/install-kubectl/
~~~

To confirm :   
~~~sh
$ ./minikube status
~~~

~~~sh
host: Running
kubelet: Running
apiserver: Running
kubeconfig: Configured
~~~

----