# os-hardening

Ansible role to apply [CIS benchmark](https://learn.cisecurity.org/benchmarks) recommendations.

CIS benchmarks & recommendations are grouped into two levels - Level 1 & Level 2.

*Level 1*
Items in this profile intend to:

* be practical and prudent;
* provide a clear security benefit; and
* not inhibit the utility of the technology beyond acceptable means.

*Level 2*
This profile extends the "Level 1 - Server" profile. Items in this profile exhibit one or
more of the following characteristics:

* are intended for environments or use cases where security is paramount.
* acts as defense in depth measure.
* may negatively inhibit the utility or performance of the technology.

## Example

```YAML
- hosts: myhost

  vars:
    os_hardening_dist_upgrade: true
    os_hardening_exclusions: [ '3.6.5', '1.8' ]   # CIS IDs of recommendations to exclude.

  roles:
    - os-hardening
```

## Testing

To test this role, run:

```bash
kitchen test
```

## Supported OS

* Ubuntu 14.04
* Ubuntu 16.04

## Dependencies

* o2-priority.ntp
* o2-priority.auditd

## Issues

* 3.1.1 - ip_forward should be disabled. Docker requires this to be enabled. https://github.com/moby/moby/issues/2396. Pass daemon flag when starting Docker to enable only when required https://github.com/moby/moby/pull/3801
* 3.6.2 - can't apply default DROP policy until each service has it's firewall rules configured. That should be the responsibility of the service to configure.

## Execution

This role is called from [Jenkins](https://github.com/o2-priority/infra-priority-tools/blob/master/jenkinsfiles/apply-cis-os-hardening-Jenkinsfile)