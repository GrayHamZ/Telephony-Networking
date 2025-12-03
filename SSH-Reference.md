# SSH Access Reference

## Login Credentials
- **Username:** admin
- **Password:** cisco

## SSH Command Format
```
ssh -l admin <ip-address>
```

---

## Main Branch (Test Network)

### Routers
| Device | IP Address | Command |
|--------|------------|---------|
| Router-Test-1 | 192.168.99.2 | `ssh -l admin 192.168.99.2` |
| Router-Test-2 | 192.168.99.3 | `ssh -l admin 192.168.99.3` |

### Multilayer Switches
| Device | IP Address | Command |
|--------|------------|---------|
| MLS-Test-1 | 192.168.99.21 | `ssh -l admin 192.168.99.21` |
| MLS-Test-2 | 192.168.99.22 | `ssh -l admin 192.168.99.22` |

### Access Switches
| Device | Department | IP Address | Command |
|--------|-----------|------------|---------|
| SW-Test-1 | Department A | 192.168.99.11 | `ssh -l admin 192.168.99.11` |
| SW-Test-2 | Department B | 192.168.99.12 | `ssh -l admin 192.168.99.12` |
| SW-Test-3 | Department C | 192.168.99.13 | `ssh -l admin 192.168.99.13` |
| SW-Test-4 | Department D | 192.168.99.14 | `ssh -l admin 192.168.99.14` |
| SW-Test-5 | Department E | 192.168.99.15 | `ssh -l admin 192.168.99.15` |
| SW-Test-6 | Department F & H | 192.168.99.16 | `ssh -l admin 192.168.99.16` |
| SW-Test-7 | Department G | 192.168.99.17 | `ssh -l admin 192.168.99.17` |

---

## Branch 1

| Device | Department | IP Address | Command |
|--------|-----------|------------|---------|
| Router-Branch1 | All | 192.168.199.1 | `ssh -l admin 192.168.199.1` |
| SW-Branch1-1 | Department I | 192.168.199.2 | `ssh -l admin 192.168.199.2` |
| SW-Branch1-2 | Department J & K | 192.168.199.3 | `ssh -l admin 192.168.199.3` |

---

## Branch 2

| Device | Department | IP Address | Command |
|--------|-----------|------------|---------|
| Router-Branch2 | All | 192.168.254.1 | `ssh -l admin 192.168.254.1` |
| SW-Branch2-1 | Department L | 192.168.254.2 | `ssh -l admin 192.168.254.2` |
| SW-Branch2-2 | Department M & N | 192.168.254.3 | `ssh -l admin 192.168.254.3` |

---

## Notes

- All devices are accessible via their VLAN 99 (Management VLAN) IP addresses
- SSH is configured on all devices with the same credentials
- You can SSH from any VLAN to any device due to inter-VLAN routing
- Management IPs are organized by location:
  - **Main Branch:** 192.168.99.x
  - **Branch 1:** 192.168.199.x
  - **Branch 2:** 192.168.254.x
