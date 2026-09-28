# 10 - Network Topology

This section documents the network topology of the CyberShield Active Directory Lab.

A Cisco Packet Tracer topology was created to provide a clear visual representation of how the physical home network, Hyper-V host, and virtual Active Directory environment relate to each other.

---

## 10.1 Network Architecture

The CyberShield lab is hosted on a Windows 11 Pro computer running Microsoft Hyper-V.

The overall environment is represented as:

**Internet → Home Router → Windows 11 Hyper-V Host → CyberShield Active Directory Lab**

Inside Hyper-V, the domain controller and Windows client communicate through the `CyberShield-Lab` Internal Virtual Switch.

### Lab Network Configuration

| Component | Configuration |
|---|---|
| Hyper-V Host | `JAHIDUL-LAPTOP` |
| Host OS | Windows 11 Pro |
| Virtual Switch | `CyberShield-Lab` |
| Switch Type | Hyper-V Internal Virtual Switch |
| Lab Network | `10.50.0.0/24` |
| Domain Controller | `DC01` |
| DC01 OS | Windows Server 2022 |
| DC01 IP | `10.50.0.10/24` |
| DC01 Roles | Active Directory Domain Services (AD DS), DNS |
| Active Directory Domain | `cybershield.test` |
| Client Workstation | `CLIENT01` |
| CLIENT01 OS | Windows 11 Pro |
| CLIENT01 IP | `10.50.0.20/24` |
| CLIENT01 DNS | `10.50.0.10` |
| CLIENT01 Status | Joined to `cybershield.test` |

---

## 10.2 Network Topology Diagram

The following diagram provides a conceptual representation of the CyberShield lab infrastructure.

![CyberShield Active Directory Lab Network Topology](network-topology/cybershield-network-topology.png)

The editable Cisco Packet Tracer project file is also included in the repository:

[CyberShield-Network-Topology.pkt](network-topology/CyberShield-Network-Topology.pkt)

---

## 10.3 Hyper-V Internal Network

The virtual machines are connected through the `CyberShield-Lab` Hyper-V **Internal Virtual Switch**.

This provides network communication between:

- `DC01`
- `CLIENT01`
- The Hyper-V host

The lab uses the private IPv4 network:

`10.50.0.0/24`

This design keeps the Active Directory environment logically separated from the normal home network while still allowing controlled communication between the lab systems and the Hyper-V host.

---

## 10.4 Active Directory DNS Design

`DC01` provides DNS services for the Active Directory environment.

The domain controller uses:

`10.50.0.10`

`CLIENT01` therefore uses `10.50.0.10` as its DNS server rather than an external DNS service.

This allows the workstation to resolve Active Directory resources within:

`cybershield.test`

Correct DNS configuration is essential for Active Directory operations including domain authentication, domain joins, Group Policy processing, and locating domain services.

---

## 10.5 Packet Tracer Representation

Cisco Packet Tracer was used to create a visual representation of the lab.

The diagram includes:

- Internet connection
- Home router
- Windows 11 Hyper-V host
- Hyper-V virtual network
- `DC01`
- `CLIENT01`

The Cisco 2960 switch shown in the Packet Tracer topology is used **conceptually to represent the Hyper-V Internal Virtual Switch**.

It does not represent a physical Cisco switch deployed in the environment.

This distinction ensures that the diagram accurately communicates the logical design of the virtual lab without implying that additional physical networking hardware is present.

---

## 10.6 Skills Demonstrated

This section demonstrates practical experience with:

- Network topology design
- Cisco Packet Tracer
- Microsoft Hyper-V networking
- Internal virtual switches
- IPv4 addressing and subnetting
- Windows Server networking
- Active Directory DNS architecture
- Domain client DNS configuration
- Virtual network isolation
- Physical versus virtual network concepts
- Infrastructure documentation

---

## 10.7 Outcome

A documented network topology was created for the CyberShield Active Directory Lab.

The topology provides a clear overview of how the Windows 11 Hyper-V host, virtual network, domain controller, DNS service, and domain-joined workstation interact within the environment.

Both the visual topology image and editable Cisco Packet Tracer project file are retained in the repository for documentation and future development.
