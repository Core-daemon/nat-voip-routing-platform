# Verified Technical Evidence

## NAT-Traversing Multi-Network VoIP Routing & SIP Media Interworking Platform

**Author:** Mohammad Sorower Jahan  
**Evidence inspection date:** 25 September 2026  
**Evidence source:** Retained Proxmox, VOS3000 and Asterisk server environment

---

## 1. Purpose

This document separates technical facts directly verified from the retained server environment from historical project information documented through other evidence.

The infrastructure was inspected in September 2026.

Current server configuration, logs and call-detail records should not be interpreted as having been captured during the original 2025 development period.

---

## 2. Proxmox Infrastructure

The retained environment is hosted on a Proxmox VE server.

### Verified information

- Proxmox VE version displayed: 5.4-15
- Proxmox host name: `dell`
- VM 101: CentOS 6.2 Softswitch environment
- VM 102: CentOS 7 Asterisk environment

The physical host contains additional virtual machines that are not treated as part of this documented VoIP architecture.

---

## 3. VM 101 - Softswitch

### Operating System

Verified from the running virtual machine:

- CentOS release 6.2 (Final)
- Architecture: x86_64
- Network interface: eth0
- Internal IP address: 10.10.10.10/24

### Softswitch Application

The running Softswitch environment contains the `mbx3000` application associated with the VOS3000 installation.

Verified executable:

`/home/kunshi/mbx3000/bin/mbx3000`

Verified application directory:

`/home/kunshi/mbx3000/`

Observed application directories include:

- bin
- cdr
- etc
- log
- logbak
- trace

Running telecommunications-related processes were observed, including `mbx3000`.

The exact VOS3000 software release/version has not been independently identified in this evidence review.

---

## 4. VM 102 - Asterisk Server

### Operating System

Verified from the running virtual machine:

- CentOS Linux 7.9.2009
- Architecture: x86_64

### Asterisk

The running telecommunications application was verified as:

**Asterisk 16.23.0**

The traditional SIP channel driver `chan_sip.so` is loaded and running.

---

## 5. Asterisk Network Interfaces

The Asterisk server uses two network interfaces.

### Internal Interface

`ens18`

Address:

`10.10.10.11/24`

This interface communicates with the internal Softswitch environment.

### Provider-Facing Interface

`ens19`

Address:

`100.64.78.194/30`

This interface provides connectivity towards the external telecommunications provider network.

---

## 6. Provider Static Routing

The Linux routing table contains dedicated host routes towards the provider signalling and media destinations.

### SIP signalling endpoint

Destination:

`100.64.0.20`

Route:

`100.64.0.20 via 100.64.78.193 dev ens19`

### RTP media endpoint

Destination:

`100.64.0.21`

Route:

`100.64.0.21 via 100.64.78.193 dev ens19`

Route lookup confirmed that traffic to both destinations uses:

- gateway `100.64.78.193`
- interface `ens19`
- source address `100.64.78.194`

This verifies the network routing architecture used to reach separate provider signalling and media destinations.

---

## 7. Internal SIP Gateway

Asterisk contains a SIP peer identified as `jio`.

Verified peer information includes:

- Address: `10.10.10.10:5060`
- Context: `from-trunk`
- Dynamic: No
- Transport: UDP
- Symmetric RTP: Yes
- Direct Media: No
- Status during inspection: OK
- Supported codecs include G.729, G.711 μ-law and G.711 A-law

Asterisk also contains a SIP registration configuration towards:

`10.10.10.10:5060`

During the September 2026 inspection the registration state displayed:

`No Authentication`

Therefore, the retained configuration proves that the registration relationship is configured but does not prove that SIP registration was successful at the time of inspection.

---

## 8. Provider SIP Peer

Asterisk contains a provider-facing SIP peer identified as `jio500`.

Verified configuration:

- SIP destination: `100.64.0.20:5060`
- Context: `from-trunk`
- Transport: UDP
- Symmetric RTP: Yes
- Direct Media: No
- Supported codecs: G.729, G.711 μ-law and G.711 A-law

The provider SBC address is explicitly configured in:

`/etc/asterisk/sip.conf`

The peer was `UNREACHABLE` during the September 2026 inspection.

This verifies the configuration but does not establish present-day provider service availability.

---

## 9. SIP Activity Evidence

Historical Asterisk message logs contain repeated `chan_sip` entries involving:

`100.64.0.20:5060`

The logs contain Asterisk call identifiers and SIP processing messages associated with the provider endpoint.

This provides evidence that the retained Asterisk server previously exchanged SIP transactions with the configured provider SBC.

The logs inspected do not independently establish the original 2025 project implementation date.

---

## 10. Dialplan Evidence

The Asterisk dialplan contains the `from-trunk` context and provider-facing call-routing logic.

An observed outbound routing rule includes a `Dial()` operation through the provider-facing `jio500` SIP peer.

The configuration also contains inbound and IVR processing contexts, including:

- `moi-incoming`
- `moi-ivr`
- `ivr-reception`
- `ivr-finance`
- `ivr-dvc`
- `ivr-security`
- `ivr-ict`
- `ivr-schools`
- `ivr-accommodation`

Internal SIP endpoints are referenced from these call-processing contexts.

This demonstrates application-level SIP call-routing logic within Asterisk.

Telephone numbers and customer-specific routing information are intentionally omitted from this public documentation.

---

## 11. RTP Media Configuration

Asterisk RTP settings were verified from the running server.

### RTP port range

Start:

`10000`

End:

`65535`

Additional settings observed include:

- Strict RTP: enabled
- RTP checksums: enabled
- ICE support: enabled
- STUN address: not configured

The RTP range is also defined in:

`/etc/asterisk/rtp.conf`

### Media Path

Both the internal and provider-facing SIP peers have:

`DirectMedia: No`

This configuration is consistent with Asterisk being kept in the RTP media path rather than instructing the remote endpoints to exchange media directly.

Actual RTP packet exchange for a specific historical call has not been independently captured during this evidence review.

---

## 12. Separate Provider Media Address

The provider media destination:

`100.64.0.21`

is present in the Linux static routing configuration.

A search of the inspected Asterisk configuration did not find this address explicitly hard-coded under `/etc/asterisk`.

This is consistent with an architecture in which the RTP destination may be supplied dynamically through SDP during SIP call negotiation.

However, this evidence review did not capture historical SDP packets proving that behaviour for a specific call.

---

## 13. Call Detail Record Evidence

The retained Asterisk server contains:

`/var/log/asterisk/cdr-csv/Master.csv`

The file was parsed using Python's CSV parser to account correctly for quoted CSV fields.

### Verified CDR statistics

**Total valid CDR records:** 2,321,693

**First retained CDR:** 28 April 2026 04:10:58

**Last retained CDR:** 16 June 2026 10:21:32

### Disposition counts

| Disposition | Records |
|-------------|--------:|
| ANSWERED | 400,837 |
| BUSY | 987,616 |
| FAILED | 7,147 |
| NO ANSWER | 926,093 |
| **Total** | **2,321,693** |

These figures represent CDR records rather than necessarily unique telephone calls.

The CDR data demonstrates substantial recorded telecommunications activity on the retained Asterisk environment during the stated 2026 period.

It does not independently establish that all records relate to the original client project or that the same volume existed during the original 2025 R&D period.

---

## 14. Verified Architecture Summary

The server-side evidence supports the following architecture:

```text
VOS3000 Softswitch
10.10.10.10
        |
        | SIP / RTP
        |
        v
Asterisk 16.23.0
ens18: 10.10.10.11
ens19: 100.64.78.194
        |
        +---------------- SIP ----------------+
        |                                     |
        |                             Provider SBC
        |                             100.64.0.20
        |
        +--------------- RTP -----------------+
                                              |
                                      Provider media route
                                      100.64.0.21
```

Asterisk provides application-level telecommunications interworking between the internal Softswitch environment and the external provider-facing network.

---

## 15. Evidence Boundaries

The September 2026 server inspection directly verifies:

- the retained virtualised infrastructure
- operating systems
- VOS3000-associated Softswitch processes
- Asterisk 16.23.0
- dual network interfaces
- provider-facing static routes
- SIP peer configuration
- Asterisk dialplan configuration
- RTP configuration
- historical SIP log entries
- retained CDR records

The inspection does not independently establish:

- the original project development date
- the identity of the original client
- who personally performed every configuration change
- the exact VOS3000 software version
- successful provider connectivity at the September 2026 inspection
- historical RTP packet flows for individual calls
- the number of unique calls represented by the CDR records

Those matters require separate supporting evidence where relevant.

---

## 16. Historical Project Evidence

The engineering project is documented separately as a 2025 research and development implementation undertaken on behalf of CRTLHost for The Goal, Kolkata, India.

The historical project background should be supported by independent documentary evidence such as:

- CRTLHost confirmation
- client correspondence
- customer evidence letters
- contemporaneous project records where available

The current server inspection should be treated as technical verification of the retained implementation rather than as proof of the historical project date.

---

## 17. Evidence Handling

Screenshots obtained during the server inspection may contain:

- management IP addresses
- telephone numbers
- usernames
- provider identifiers
- customer information
- infrastructure details

Only appropriately redacted evidence should be published publicly.

Original unredacted material should be retained privately where necessary for evidential integrity.

---

**Author:** Mohammad Sorower Jahan

**Evidence inspection:** September 2026
