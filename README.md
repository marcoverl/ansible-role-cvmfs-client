marcoverl.cvmfs_client
======================

Ansible role to install CernVM-FS Client with or w/o its containerd snapshotter

Requirements
------------

Python is required on host to run ansible.

Variables
---------

``server_url``: set cvmfs server url (e.g. ip address or domain, default: ``rgw.cloudveneto.it/cvmfswp6dc``).

``repository_name``: set cvmfs server repository name (default: ``unpacked.infn.it``).

``cvmfs_server_url``: sert cvmfs server complete url (default: ``'http://{{ server_url }}/cvmfs/{{ repository_name }}``).

``cvmfs_public_key_path``: set path for cvmfs keys (default: ``/etc/cvmfs/keys/infn.it``).

``cvmfs_public_key``: set cvfms public key, usually `<repository_name.pub>` (default: ``{{ repository_name }}.pub``).

``cvmfs_preconfigured``: allow to mount cvmfs volumes importing preconfigured file: works for cern.ch and egi.eu repos (default: ``false``)

``proxy_url``: set proxy name (default: ``DIRECT``).

``proxy_port``: set proxy port (default: ``80``).

``cvmfs_http_proxy``: set proxy complete url (default: ``http://{{ proxy_url }}:{{ proxy_port }}``).

``cvmfs_mountpoint``: set cvmfs mount point (default: ``/cvmfs``). If set to ``/cvmfs`` the role will use ``cvmfs_config probe`` to mount the repository.

``add_fstab_entry``: add fstab entry to automatically mount the repository (default: ``true``).

``snapshotter``: install and configure the cvmfs-snapshotter (default: ``false``).

``snapshotter_path``: path where to install the cvmfs-snapshotter software (default: ``/usr/local/share``).

Example Playbook
----------------

The role takes the default values but one of the repositories of INFN-Cloud

```yaml
  - hosts: localhost
    roles:
      - role: marcoverl.cvmfs_client
        repository_name: 'unpacked.infn.it'
```

Here it installs the client and the snapshotter.

```yaml
  - hosts: localhost
    roles:
      - role: marcoverl.cvmfs_client
        repository_name: 'unpacked.infn.it'
        snapshotter: true
```

Here it install the client and mounts the wenmr.egi.eu repository (all is preconfigured in the cvmfs-config-default package)

```yaml
  - hosts: localhost
    roles:
      - role: marcoverl.cvmfs_client
        repository_name: 'wenmr.egi.eu'
        cvmfs_preconfigured: true
```


License
-------

Apache Licence v2: http://www.apache.org/licenses/LICENSE-2.0

Reference
---------

Official cvmfs documentation: http://cvmfs.readthedocs.io/en/stable/cpt-repo.html

NIKHEF documentation: https://wiki.nikhef.nl/grid/Adding_a_new_cvmfs_repository
