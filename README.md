# k8s on DO

Note: This is a quick and dirty solution to quickly bring up k8s cluster. Do not use for production!!!

## setup droplets

master, worker-01, worker-02.

Write IPs to [hosts](./hosts) inventory file.

## Install k8s on servers

```bash
ansible-playbook -i hosts ./provision-cluster.yml
```

## Access cluster

- scp to kubeconfig from master to local
  - `scp root@<master_ip>:/home/centos/.kube/config ~/.kube/do-config`

## Create users and generate config for them

I've found [some script](https://gist.github.com/innovia/fbba8259042f71db98ea8d4ad19bd708) generating `kube/config` from service account.

I've tweaked it a bit and saved it in [this repo](./scripts/create_sa_user.sh).

To create access for user, do `./scripts/create_sa_user.sh <NAMESPACE>`
