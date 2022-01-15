# Build a Kubernetes cluster using k3s via Ansible.

> This repository is now part of https://github.com/k3s-io/k3s-ansible official repo in contrib/ansible directory.
> Anyway I'll write updates in order to make PM in k3s.
> Be my guest and feel free to contribute.

## My blog post about these bunch of playbooks

Here is my post about [k3s and Ansible provisionning](https://www.it-wars.com/posts/cloud-native/kubernetes-avec-k3s-pour-sauver-la-planete/) (in French)

## K3s Ansible Playbook

Build a Kubernetes cluster using Ansible with k3s. The goal is easily install a Kubernetes cluster on machines running:

- [X] Debian 9
- [ ] Ubuntu 16.04
- [ ] CentOS 7

on processor architecture:

- [X] x64
- [X] arm64
- [X] armhf

## System requirements:

Deployment environment must have Ansible 2.4.0+
Master and nodes must have passwordless SSH access

## Usage

Add the system information gathered above into a file called hosts.ini. For example:

```
[master]
192.16.35.12

[node]
192.16.35.[10:11]

[kube_cluster:children]
master
node
```

Start provisioning of the cluster using the following command:

```
ansible-playbook site.yml
```

## Useful troubleshooting commands

export K3S_TOKEN=K10bad670bbf2f7c7e1af98bbcc1da126e1fd32c6c2f397acfeb2f3d4bf97253020::server:4062ab749e59d7288d004dd14c161447
export K3S_URL=https://192.168.4.241:6443
export KUBECONFIG=/Users/sbailey/.kube/config-rpi-k3s

k3s-killall.sh
k3s-uninstall.sh
k3s-agent-uninstall.sh

--

NAME: postgres
LAST DEPLOYED: Sat Jan 15 06:23:07 2022
NAMESPACE: default
STATUS: deployed
REVISION: 1
TEST SUITE: None
NOTES:
CHART NAME: postgresql
CHART VERSION: 10.16.1
APP VERSION: 11.14.0

** Please be patient while the chart is being deployed **

PostgreSQL can be accessed via port 5432 on the following DNS names from within your cluster:

    postgres-postgresql.default.svc.cluster.local - Read/Write connection

To get the password for "postgres" run:

    export POSTGRES_PASSWORD=$(kubectl get secret --namespace default postgres-postgresql -o jsonpath="{.data.postgresql-password}" | base64 --decode)

To connect to your database run the following command:

    kubectl run postgres-postgresql-client --rm --tty -i --restart='Never' --namespace default --image docker.io/bitnami/postgresql:11.14.0-debian-10-r28 --env="PGPASSWORD=$POSTGRES_PASSWORD" --command -- psql --host postgres-postgresql -U postgres -d postgres -p 5432



To connect to your database from outside the cluster execute the following commands:

    kubectl port-forward --namespace default svc/postgres-postgresql 5432:5432 &
    PGPASSWORD="$POSTGRES_PASSWORD" psql --host 127.0.0.1 -U postgres -d postgres -p 5432


    https://marclamberti.com/blog/airflow-on-kubernetes-get-started-in-10-mins/