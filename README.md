avinetworks.avicontroller-ovirt
=========

*This role is under development as is **NOT** finished yet*
**You have been warned!**

Deploys Avi Controllers into a RHEV environment.

Order of operations:
* Installs the prereqs
* Creates a temporary VM
* Creates a template from the temporary VM
* Deletes the temporary VM
* Creates the Avi required metadata and uploads this to the ISO storage
* Builds the Avi controllers from the template
* Attaches the relevant metadata ISO to each VM
* Starts each controller VM

Requirements
------------

* qemu-img
* genisoimage

Role Variables
--------------

* Loads - TBD

Dependencies
------------

* None so far but I reckon there will be at some point

Example Playbook
----------------

    ---
    - hosts: rhev-engine
      gather_facts: false
      vars:
        con_rhev_user: admin@internal
        con_rhev_pass: <password>
        iso_storage_domain: <iso_storage>
        controllers:
          - name: ctrl1
            ip_address: 10.1.1.1
            netmask: 255.255.255.0
            gateway: 10.1.1.254
          - name: ctrl2
            ip_address: 10.1.1.2
            netmask: 255.255.255.0
            gateway: 10.1.1.254
          - name: ctrl3
            ip_address: 10.1.1.3
            netmask: 255.255.255.0
            gateway: 10.1.1.254
        template:
          name: avi_controller_template
          cluster: <rhev_compute_cluster>
          memory: <in GB>
          cpu: <some>
          network: ovirtmgmt
          storage_domain: hosted_storage
          qcow2: <avi_controller.qcow2>
      roles:
      - avinetworks.avicontroller-ovirt

License
-------

* NA

Author Information
------------------

* Me
