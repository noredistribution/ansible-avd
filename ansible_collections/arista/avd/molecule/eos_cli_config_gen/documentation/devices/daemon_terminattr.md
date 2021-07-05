# daemon_terminattr
# Table of Contents
<!-- toc -->

- [daemon_terminattr](#daemon_terminattr)
- [Table of Contents](#table-of-contents)
- [Management](#management)
  - [Management Interfaces](#management-interfaces)
    - [Management Interfaces Summary](#management-interfaces-summary)
      - [IPv4](#ipv4)
      - [IPv6](#ipv6)
    - [Management Interfaces Device Configuration](#management-interfaces-device-configuration)
- [Authentication](#authentication)
- [Monitoring](#monitoring)
  - [TerminAttr Daemon](#terminattr-daemon)
    - [TerminAttr Daemon Summary](#terminattr-daemon-summary)
    - [TerminAttr Daemon Device Configuration](#terminattr-daemon-device-configuration)
- [Internal VLAN Allocation Policy](#internal-vlan-allocation-policy)
  - [Internal VLAN Allocation Policy Summary](#internal-vlan-allocation-policy-summary)
- [Interfaces](#interfaces)
- [Routing](#routing)
  - [IP Routing](#ip-routing)
    - [IP Routing Summary](#ip-routing-summary)
    - [IP Routing Device Configuration](#ip-routing-device-configuration)
  - [IPv6 Routing](#ipv6-routing)
    - [IPv6 Routing Summary](#ipv6-routing-summary)
- [Multicast](#multicast)
- [Filters](#filters)
- [ACL](#acl)
- [Quality Of Service](#quality-of-service)

<!-- toc -->
# Management

## Management Interfaces

### Management Interfaces Summary

#### IPv4

| Management Interface | description | Type | VRF | IP Address | Gateway |
| -------------------- | ----------- | ---- | --- | ---------- | ------- |
| Management1 | oob_management | oob | MGMT | 10.73.255.122/24 | 10.73.255.2 |

#### IPv6

| Management Interface | description | Type | VRF | IPv6 Address | IPv6 Gateway |
| -------------------- | ----------- | ---- | --- | ------------ | ------------ |
| Management1 | oob_management | oob | MGMT | -  | - |

### Management Interfaces Device Configuration

```eos
!
interface Management1
   description oob_management
   vrf MGMT
   ip address 10.73.255.122/24
```

# Authentication

# Monitoring

## TerminAttr Daemon

### TerminAttr Daemon Summary

| CV Compression | Ingest gRPC URL | Ingest Authentication Key | Smash Excludes | Ingest Exclude | Ingest VRF | AAA Disabled |
| -------------- | --------------- | ------------------------- | -------------- | -------------- | ---------- | ------------ |
| gzip | 10.20.10.10:9910 | token, /tmp/token | ale,flexCounter,hardware,kni,pulse,strata | /Sysdb/cell/1/agent,/Sysdb/cell/2/agent | MGMT | True |
| gzip | www.arista.io:443 | token-secure, /tmp/cv-onboarding-token | ale,flexCounter,hardware,kni,pulse,strata | /Sysdb/cell/1/agent,/Sysdb/cell/2/agent | MGMT | True |
| gzip | 10.10.10.10:9910 | key, arastra | ale,flexCounter,hardware,kni,pulse,strata | /Sysdb/cell/1/agent,/Sysdb/cell/2/agent | MGMT | True |

### TerminAttr Daemon Device Configuration

```eos
!
daemon TerminAttr
   exec /usr/bin/TerminAttr -cvaddr=10.20.10.10:9910 -cvopt cvaas.addr=www.arista.io:443 -cvopt cvaas.auth=token-secure,/tmp/cv-onboarding-token -cvopt dublin.addr=10.10.10.10:9910 -cvopt dublin.auth=key,arastra -cvopt dublin.vrf=MGMT -cvopt dublin.obscurekeyfile -cvauth=token,/tmp/token -cvobscurekeyfile -cvvrf=MGMT -disableaaa -grpcaddr MGMT/0.0.0.0:6042 -grpcreadonly -smashexcludes=ale,flexCounter,hardware,kni,pulse,strata -ingestexclude=/Sysdb/cell/1/agent,/Sysdb/cell/2/agent -taillogs
   no shutdown
```

# Internal VLAN Allocation Policy

## Internal VLAN Allocation Policy Summary

**Default Allocation Policy**

| Policy Allocation | Range Beginning | Range Ending |
| ------------------| --------------- | ------------ |
| ascending | 1006 | 4094 |

# Interfaces

# Routing

## IP Routing

### IP Routing Summary

| VRF | Routing Enabled |
| --- | --------------- |
| default | false|
### IP Routing Device Configuration

```eos
```
## IPv6 Routing

### IPv6 Routing Summary

| VRF | Routing Enabled |
| --- | --------------- |
| default | false |

# Multicast

# Filters

# ACL

# Quality Of Service
