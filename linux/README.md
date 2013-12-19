# Couchbase Server Ansible Orchestration



               .CCCCC                       CCCCC.
              .CCCCCC                       CCCCCC.
              .CCCCCC                       CCCCCC.
              .CCCCCC                       CCCCCC.
              .CCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCC.
              .CCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCC.
              .CCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCC.
               .CCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCC.

[Couchbase Server](http://www.couchbase.com/couchbase-server/overview) is a
high performance NoSQL document database available in Community and Enterprise
editions for several operating system environments.

This project provides documentation and a collection of scripts to help you
automate the deployment of Couchbase Server Enterprise Edition using the [Ansible](http://www.ansibleworks.com/)
orchestration engine. These are the instructions for deploying a staging or
production cluster on CentOS or Ubuntu.

The documentation and scripts are merely a starting point designed to both
help familiarize you with the processes and quickly bootstrap an environment.
You may wish to expand on them and customize the steps in this guide with
additional features specific to your needs later.

## Linux Staging or Production Deployment

This section describes deployment of a Couchbase Server cluster
using the following technologies:

* [Couchbase Server](http://www.couchbase.com/couchbase-server/overview)
* [Ansible](http://www.ansibleworks.com/)

The Ansible playbooks refine OS configuration, download and install Couchbase
Server, and initialize the nodes into a ready to use cluster.

## Quick Start

1. Install [Ansible](http://www.ansibleworks.com/docs/intro_installation.html) on the system you'll use to orchestrate Couchbase Sever cluster deployment.
   This  computer must have SSH access to the cluster nodes.
2. Define the cluster node hosts in either `hosts_centos` or `hosts_ubuntu`
   depending on which OS you will use.
3. Specify the Couchbase Server version (`version`) and SHA-256 checksum
   (`sha256`) of the package file in the `group_vars/all` file.
4. Define cluster node parameters, such as the cluster RAM quota
   (`server_ram`), data and index storage paths (`data_path`, `index_path`),
   physical disk information (`data_storage`, `index_storage`), and network
   interface (`network`).
5. Execute the top level Ansible playbook:
   `ansible-playbook -i centos site.yml
   (replace *centos* with *ubuntu* if you're using Ubuntu based nodes)

## Detailed Guide

If you'd like to follow a more detailed installation process with additional
explanation of the steps and technologies, see the following sections of
this guide.

### Prerequisites

Before you begin with the steps in this guide, please ensure that you have
the following prerequisites configured and installed.

#### Ansible

Install Ansible using `pip` based on the
[installation documentation](http://www.ansibleworks.com/docs/intro_installation.html#latest-releases-via-pip). Provided you are willing to install into your system
Python, the steps are simple and involve just 2 commands:

```
sudo easy_install pip
sudo pip install ansible
```

Alternatively, you can use a
[virtualenv](http://www.virtualenv.org/en/latest/) and install Ansible
into that.

### Bootstrap the Cluster

Now it's time for bootstrapping the Couchbase Server cluster.

Open a terminal, change into the `linux` subdirectory of this project's
top level directory and execute the top level Ansible playbook with a
command like the following:

```
ansible-playbook -i <hosts> site.yml
```

Replace *<hosts>* with `centos` or `ubuntu` depending on the operating system
you're using for your cluster nodes.

After some time to configure the OS, download and install Couchbase Server,
and initialize the cluster, you'll soon be ready to try out your new cluster.

### Give it a Try

Once the Ansible playbooks complete without error, you can open a browser and
access the primary Couchbase Server cluster node with a URL like:

```
http://couchbase.local:8091
```

Substitute *couchbase.local* with the hostname of your
Couchbase Server primary node.

The administrator username and password as configured by this project
are:

* Username: **Administrator**
* Password: **couchbase**

Once you've logged in and verified that the cluster is available, you're now
ready to create buckets and begin using your new Couchbase Server development
cluster.

## Notes

1. Review the different operating system tuning changes in the following
   files to adjust or add your own:
   * `roles/bootstrap/common/templates/etc_rc.local.j2`
   * `roles/bootstrap/common/templates/iptables.j2`
   * `roles/couchbase-server/centos/templates/iptables.j2`
   * `roles/couchbase-server/ubuntu/templates/iptables.j2`

## References

1. http://www.couchbase.com/couchbase-server/overview
2. http://www.ansibleworks.com/
