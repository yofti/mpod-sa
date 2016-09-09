ABOUT
=====
This git repository contains the source code for MPOD-SA labs.

SETTING UP LAB ENVIRONMENT
==========================

The following sections describe technical requirements to setup the environment.

PREPARING GIT BACKEND FOR LAB
-----------------------------

```console

export MPODFLOATINGIP=<mpod_td_backend_floating_ip>
export PATHTOSOURCE=/your/path/to/source
export GIT_SSH_COMMAND=ssh -i ${PATHTOSOURCE}/keys/mpod-admin.key

mkdir ~/mpod-sa
cd ~/mpod-sa

mkdir -p {keys,heat}
cp -r ${PATHTOSOURCE}/kube-yaml/concrete5 ~/mpod-sa/
cp -r ${PATHTOSOURCE}/kube-yaml/jenkins ~/mpod-sa/
cp -r ${PATHTOSOURCE}/kube-yaml/nginxlb ~/mpod-sa/
cp -r ${PATHTOSOURCE}/kube-yaml/rocketchat ~/mpod-sa/
cp -r ${PATHTOSOURCE}/keys/mpod.key* ~/mpod-sa/keys
cp -r ${PATHTOSOURCE}/heat/heat-deploy-coreos_etcd2_cluster.yaml ~/mpod-sa/heat
cp -r ${PATHTOSOURCE}/heat/heat-deploy-gitlab_v2.yaml ~/mpod-sa/heat
cp -r ${PATHTOSOURCE}/heat/heat-deploy-kube_master_centos7.yaml ~/mpod-sa/heat
cp -r ${PATHTOSOURCE}/heat/heat-deploy-kube_minion_centos7.yaml ~/mpod-sa/heat
cp -r ${PATHTOSOURCE}/heat/heat-deploy-nfs_server_v2.yaml ~/mpod-sa/heat
cp -r ${PATHTOSOURCE}/heat/heat-deploy-devbox_v2.yaml ~/mpod-sa/heat
cp -r ${PATHTOSOURCE}/heat/heat-deploy-tier_vol.yaml ~/mpod-sa/heat

git init
git config --local user.name "Administrator"
git config --local user.email "mpodadmin@dev.local"
git remote add origin git@${MPODFLOATINGIP}:root/mpod-sa.git
git add concrete5/* concrete5/.gitlab-ci.yml jenkins/* nginxlb/* rocketchat/* keys/* heat/* README_MPOD-SA.md
git commit -m "MPOD-SA v1.0"
git push -u origin master

````

The final content fo the repository
```console

mpod-sa/
├── concrete5
│   ├── 1-mariadb-pod.yaml
│   ├── 2-mariadb-svc.yaml
│   ├── 3-concrete5-vol.yaml
│   ├── 4-concrete5-rc.yaml
│   ├── 5-concrete5-svc.yaml
│   └── Makefile
├── containers
│   └── concrete5.7.tar
├── heat
│   ├── heat-deploy-coreos_etcd2_cluster.yaml
│   ├── heat-deploy-devbox_v2.yaml
│   ├── heat-deploy-gitlab_v2.yaml
│   ├── heat-deploy-kube_master_centos7.yaml
│   ├── heat-deploy-kube_minion_centos7.yaml
│   ├── heat-deploy-nfs_server_v2.yaml
│   └── heat-deploy-tier_vol.yaml
├── jenkins
│   ├── 1-jenkins-vol.yaml
│   ├── 2-jenkins-svc.yaml
│   ├── 3-jenkins-rc.yaml
│   └── Makefile
├── keys
│   ├── mpod.key
│   └── mpod.key.pub
├── nginxlb
│   ├── Dockerfile
│   ├── Makefile
│   └── nginxlb.conf
├── README.md
└── rocketchat
    ├── 1-mongo-pod.yaml
    ├── 2-mongo-svc.yaml
    ├── 3-rocketchat-rc.yaml
    ├── 4-rocketchat-svc.yaml
    └── Makefile

```


PREPARING STUDENT ENVIRONMENT
-----------------------------

Tenant Environment:
- Group Number: X (1-9)
- Name: TenantX
- Key-Pair: mpod-key
- Subnet: 10.X0.0.0/24
- NFS Server: nfs_server (HOT)
- Jumphost/Dev Station: devbox (HOT)

Heat Orchestration Teamples (HOT):
- NFS Server: heat-deploy-nfs_server_v2.yaml
- Jumphost: heat-deploy-devbox_v2.yaml


LICENSE AND CONTACT
===================

This work is licensed under the Creative Commons Attribution 4.0 International License. To view a copy of this license, visit http://creativecommons.org/licenses/by/4.0/.

Copyright (C)2016 William Caban <william.caban@gmail.com>
