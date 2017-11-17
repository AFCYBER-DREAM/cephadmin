Ceph Admin
===========

The purpose of this role is to install ceph-admin node that will be used to install and administer a ceph cluster.

Requirements
------------

Because a ceph-ansible package is not available for CentOS this role currently only works on RHEL (only 7 tested).

Role Variables
--------------

The default variables are stored in **defaults/main.yml** and are:

* packages_to_install: list of yum packages that should be installed. Some default packages have been defined.
* rhcs_version: The version of RedHat Ceph Storage that will be used in the cluster. A default packages have been defined.
* osd_devices: The devices that will be used for both the osd and journals. If not defined then no devices will be set. See example below.
* ansible_keys_dir: Location on the node to store ceph keys for deployment.
* monitor_interface: Which network interface the monitor will be listening on.
* ceph_mon_rpms: Enable or disable this repository. Default is yes.
* ceph_osd_rpms: Enable or disable this repository. Default is yes.
* ceph_installer_rpms: Enable or disable this repository. Default is yes.
* ceph_tools_rpms: Enable or disable this repository. Default is yes.

osd_devices example:

    osd_devices:
      - device: sdb
        journal: sdc

Variables that should be set in either host or group vars are:

* ceph_public_network: public network for the ceph cluster.
* ceph_cluster_network: Private network used for ceph osd replication and re-balancing.
* reposerver: IP or DNS name of the server that has the needed RedHat ceph packages. If undefined then it is assumed that the user will use subscription-manager to set up the yum.repo.d file.

Dependencies
------------

None

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - import_playbook: infrastructure.yml

    - name: Set up a ceph-admin node
      hosts: ceph-admin
      become: True
      gather_facts: true

      roles:
        - cephadmin

License
-------

MIT

Author Information
------------------

The Development Range Engineering, Architecture, and Modernization (DREAM) Team.
