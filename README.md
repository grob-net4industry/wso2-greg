klousiaj.wso2-greg
=========
A role that installs an instance of the [WSO2 Governance Registry](http://wso2.com/products/governance-registry/) on CentOS. This role installs the instance as a service that will start on boot.

Requirements
------------
Created and validated to run on Ansible v1.9.4

This role assumes that a Java JDK has already been installed on the target machine. If it doesn't already exist, a new service user will be created. By default, this user is created as `wso2`. The installation zip file is not downloaded from the WSO2 website. It must be provided and is assumed to be named as `wso2greg-5.1.0.zip` and in the `files` directory. This can be overwritten by setting the `wso2_greg_archive` variable.

Role Variables
--------------
The following variables are defined in the `defaults/main.yml` file.

    # defaults file for klousiaj.wso2-greg
    wso2_user: wso2
    carbon_base: "/opt/wso2/{{wso2_app}}"
    carbon_home: "{{carbon_base}}/current"
    
    # these are the default ports for wso2 products
    # changing these will not alter the installation port 
    # port changes must be done with the offset.
    wso2_default_https_port: 9443
    wso2_default_http_port: 9763 
    # used to set the port
    wso2_greg_offset: 0
    
    # wso2-greg
    wso2_app: wso2-greg 
    wso2_greg_version: 5.1.0
    wso2_greg_directory: "wso2greg-{{ wso2_greg_version }}"
    wso2_greg_https_port: "{{ wso2_default_port + wso2_greg_offset }}"
    wso2_greg_http_port: "{{ wso2_default_port + wso2_greg_offset }}"
    
    wso2_greg_archive: "{{ wso2_greg_directory }}.zip"
    
    # this is only used if you are installing the sample data
    # vars/main.yml:wso2_greg_sample_data == true
    apache_ant_version: 1.9.6
    apache_ant_home: /opt/apache/ant/current
    apache_base: "/opt/apache"
    apache_ant_base: "{{ apache_base }}/ant"
    apache_mirror: "http://apache.osuosl.org"

Dependencies
------------
N/A

Example Playbook
----------------

    ---
    - hosts: *
      roles:
        - { role: klousiaj.wso2-greg, java_home: "/usr/java/default" }

License
-------

MIT
