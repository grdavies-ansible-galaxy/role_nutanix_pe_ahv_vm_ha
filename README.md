# Nutanix Role to configure VM HA for AHV in Prism Element

This Ansible role sets the VM HA configuration for a cluster running AHV via Prism Element.

## Role Variables

| Variable                                      | Required | Default  | Choices                                                                         | Comments                                                                                                                                                                                                                          |
|-----------------------------------------------|----------|----------|---------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| role_nutanix_pe_ahv_vm_ha_host                | yes      |          |                                                                                 | The IP address or FQDN for the Prism (Element only) to which you want to connect.                                                                                                                                                 |
| role_nutanix_pe_ahv_vm_ha_host_username       | yes      |          |                                                                                 | A valid username with appropriate rights to access the Nutanix API.                                                                                                                                                               |
| role_nutanix_pe_ahv_vm_ha_host_password       | yes      |          |                                                                                 | A valid password for the supplied username.                                                                                                                                                                                       |
| role_nutanix_pe_ahv_vm_ha_host_port           | no       | 9440     |                                                                                 | The Prism TCP port.                                                                                                                                                                                                               |
| role_nutanix_pe_ahv_vm_ha_host_validate_certs | no       | false    | true / false                                                                    | Whether to check if Prism UI certificates are valid.                                                                                                                                                                              |
| role_nutanix_pe_ahv_vm_ha_debug               | no       | false    | true / false                                                                    | Enable debug logging                                                                                                                                                                                                              |
| role_nutanix_pe_ahv_vm_ha_desired_state       | yes      |          | ['BestEffort', 'HighlyAvailable']                                               | The target HA state. BestEffort has no reservation and will restart VMs as long as there is sufficient capacity. HighlyAvailable reserves capacity for all powered on VMs and therefore guarantees capacity to power VMs back on. |

## Dependencies

- grdavies.role_nutanix_prism_api
- grdavies.role_nutanix_prism_monitor_task

## Example Playbook

This playbook will set the VM HA state to highly available (ie. VM reservation).

```
- hosts: localhost
  gather_facts: false
  roles:
    - role: grdavies.role_nutanix_pe_ahv_vm_ha
  vars:
    role_nutanix_pe_ahv_vm_ha_host: 10.38.185.37
    role_nutanix_pe_ahv_vm_ha_host_username: admin
    role_nutanix_pe_ahv_vm_ha_host_password: nx2Tech165!
    prism_desired_ha_state: HighlyAvailable
```

This playbook will set the VM HA state to best effort.

```
- hosts: localhost
  gather_facts: false
  roles:
    - role: grdavies.role_nutanix_pe_ahv_vm_ha
  vars:
    role_nutanix_pe_ahv_vm_ha_host: 10.38.185.37
    role_nutanix_pe_ahv_vm_ha_host_username: admin
    role_nutanix_pe_ahv_vm_ha_host_password: nx2Tech165!
    prism_desired_ha_state: BestEffort
```

## License

See LICENSE.md

## Author Information

Ross Davies
/Users/ross.davies/Documents/GitHub/nutanix_ansible_galaxy_roles/role_nutanix_pe_ahv_vm_ha/README.md