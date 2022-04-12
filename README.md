ansible-ssl-certificates
=========
Simple Ansible role to generate SSL certificates. Can be either a selfsigned certificate or a fake root CA. For test purpose only. 


Requirements
------------
Ansible ver 2.9.


Role Variables
--------------

Variables are listed below: 

Folder where the certificates will be put:
```
cert_path: ""
```

Below are the mandatory that will be used to generate the CSR
```
COUNTRY: ""
CITY: ""
STATE: ""
O: "" #Organization
OU: "" #Organizational Unit.
COMMON_NAME: ""
```

For the Subjetcs alternative names. The values must be setup in a list like below:
```
sans:
  - ""
  - ""
```


By default the role will generate a selfsigned certitifate: 
```
certificate_type: "" #Set it to ownca to create a locale fake ca root
```

When certificate is set to ownca these two values must be set: 
```
secret_ca_passphrase: "" #You need a passphrase for a CA private key. 
ca_common_name: ""
```


Dependencies
------------

A list of other roles hosted on Galaxy should go here, plus any details in regards to parameters that may need to be set for other roles, or variables that are used from other roles.

Example Playbook
----------------

To run the playbook to generate a selfsigned certificate on your host. 
```
- name: Playbook to run certificate creation on localhost.
  hosts: localhost
  connection: local
  vars: 
    cert_path: <path>
    COUNTRY: "YOUR COUNTRY"
    CITY: "YOUR CITY"
    STATE: "YOUR STATE"
    O: "YOUR ORG"
    OU: "YOUR OU"
    COMMON_NAME: "testdomain.test.local"
    sans:
      - "testdomain.test.local"
      - "testdomain"
  roles:
    - role: ./ansible-ssl-certificates
```


To run the playbook to generate a certificate with its own CA on your local host: 

```
- name: Playbook to run certificate creation on localhost.
  hosts: localhost
  connection: local
  vars: 
    cert_path: <path>
    COUNTRY: "YOUR COUNTRY"
    CITY: "YOUR CITY"
    STATE: "YOUR STATE"
    O: "YOUR ORG"
    OU: "YOUR OU"
    COMMON_NAME: "testdomain.test.local"
    sans:
      - "testdomain.test.local"
      - "testdomain"
    certificate_type: "ownca"
    secret_ca_passphrase: "YourVeryComplicatedPassword" 
    ca_common_name: "YOUR CA COMMON NAME"

  roles:
    - role: ./ansible-ssl-certificates
```

License
-------
 GPL-3.0 

Author Information
------------------
Flavien Rugiano (Fultux ) 2022.
