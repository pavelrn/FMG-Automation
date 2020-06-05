# FortiManager/FortiGate Automation using Ansible
This Ansible playbook can be used to manage FortiGate static URL filters via FortiManager.
The playbook uploads URL filter into FortiManager and starts Policy Package install procedure.

### How to install

Install ansible 2.5+. Example installation for ubuntu/trusty64:

```
sudo apt update
sudo apt -y install git python-pip python-dev python3-dev libssl-dev
sudo pip install setuptools bcrypt cffi enum cryptography markupsafe pyasn1 pynacl urllib3 requests
sudo pip install ansible
```

Clone this repo:
```
git clone https://github.com/solidex/FMG-Automation
```

The playbook is using FortiManager JSON-RPC API using the library (included). The library can be found here:

```
https://github.com/networktocode/fortimanager-ansible
```

Install dependencies:
```
cd FMG-Automation
pip install -r requirements.txt
```

### How to configure playbook

Configure settings in the `vars/group_vars/all`.

### How to configure FortiManager

FortiManager must have workspace-mode enabled for playbook to run properly:
```
config system global
set workspace-mode normal
end
```
API user must have following permissions to change configuration without issues:
```
config system admin user
 edit "ansible"
  set rpc-permit read-write
 end
end
```
### Sample usage
To use the playbook the working directory should contain prepared URL list in JSON format. See `urls.json` as an example.
Sample usage:
```
ansible-playbook install-url-filter.yml
```

### Troubleshooting
Look into `logs` directory for troubleshooting info.

### Tested environment
FortiManager OS 6.0.4, 6.0.8.  
FortiGate FortiOS 5.6.3.    
Use <`ansible 2.7.8`, `python 2.7`> or <`ansible 2.9.9`, `python 3.6`>
