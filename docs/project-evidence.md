# Project Evidence and Engineering Contribution

## NAT-Traversing Multi-Network VoIP Routing & SIP Media Interworking Platform

**Author:** Mohammad Sorower Jahan

**Project Year:** 2025

**Engineering Organisation:** CRTLHost

**Client:** The Goal, Kolkata, India

**Project Type:** Research and Development

**Engineering Field:** Telecommunications Infrastructure, VoIP, SIP/RTP Interworking and Multi-Network Connectivity

---

## 1. Project Background

This document records the engineering work undertaken in connection with the development of a multi-network VoIP routing and SIP media interworking platform.

The project was undertaken in 2025 for The Goal, an India-based company, on behalf of CRTLHost.

The work involved researching, designing and implementing a telecommunications infrastructure solution intended to enable communication between otherwise isolated network environments.

The project was developed as a research and development implementation for a new telecommunications service.

It combined a VOS3000 Softswitch, Asterisk, Linux virtualisation and telecommunications network routing.

The implementation supported the processing of inbound and outbound telecommunications calls through an intermediate Asterisk server.

---

## 2. Engineering Objective

The principal objective was to develop a telecommunications platform capable of establishing communication between an internal Softswitch environment and an external telecommunications provider.

The two environments operated across different network interfaces and addressing arrangements.

The external telecommunications provider also used separate network endpoints for SIP signalling and RTP media.

The engineering implementation sought to establish appropriate SIP signalling, media negotiation, routing and bidirectional RTP connectivity between these environments.

---

## 3. Original Infrastructure

The research and development implementation used one physical server running Proxmox VE.

Two virtual machines were configured within the Proxmox environment.

### Virtual Machine 1

**Application:** VOS3000 Softswitch

**Operating System:** CentOS 6.2, 64-bit Minimal

**Internal IP Address:** 10.10.10.10

The VOS3000 Softswitch provided the internal telecommunications environment and communicated with Asterisk through a registration-based SIP gateway arrangement.

### Virtual Machine 2

**Application:** Asterisk

**Operating System:** CentOS 7, 64-bit Minimal

**Internal Interface:** ens18

**Internal IP Address:** 10.10.10.11

**External Interface:** ens19

The Asterisk server provided telecommunications interworking between the internal Softswitch and the external provider's SIP trunk network.

Both SIP signalling and RTP media passed through Asterisk.

The implementation incorporated static routing to establish connectivity with the provider's separate SBC signalling and RTP media endpoints.

Asterisk did not perform IP-level NAT between its internal and external interfaces.

---

## 4. Engineering Contribution

Mohammad Sorower Jahan undertook the engineering work associated with developing the multi-network telecommunications infrastructure.

The project involved:

- Designing the virtualised telecommunications infrastructure.
- Deploying the Linux-based virtual server environment.
- Integrating the VOS3000 Softswitch with Asterisk.
- Configuring the Asterisk server's internal and provider-facing network interfaces.
- Establishing connectivity between the internal Softswitch and the external telecommunications provider.
- Configuring SIP gateway integration.
- Implementing inbound and outbound telecommunications call routing.
- Configuring network connectivity to the provider's signalling and media infrastructure.
- Investigating SIP signalling, SDP negotiation and RTP media connectivity.
- Developing and testing the telecommunications interworking implementation.

The engineering approach used Asterisk as an application-level intermediary between the internal and external telecommunications environments.

---

## 5. Research and Development Scope

The project was developed as a research and development implementation for a new telecommunications service.

The technical work focused on establishing telecommunications connectivity between otherwise isolated network environments.

The implementation incorporated bidirectional call routing and RTP media interworking through Asterisk.

The work addressed the interaction between telecommunications application configuration, network interfaces, IP routing, SIP signalling and RTP media communication.

This repository documents the engineering architecture and implementation approach.

It does not represent the project as a commercially deployed production service.

---

## 6. Technical Implementation

The platform incorporated two principal telecommunications environments.

The internal environment contained the VOS3000 Softswitch.

The external environment provided access to the telecommunications provider's SIP trunk infrastructure.

The Asterisk server connected to both environments through separate network interfaces.

SIP signalling and RTP media were handled through Asterisk.

The internal Softswitch and external provider did not require direct end-to-end IP connectivity for the documented call path.

Static routing provided Asterisk with connectivity to the provider's separate signalling and media endpoints.

The implementation supported both inbound and outbound telecommunications call processing.

Further information is available in the repository's technical architecture, network routing and SIP gateway documentation.

---

## 7. Historical Implementation and Present-Day Evidence

The original project was undertaken in 2025.

The original server remains available, with its configuration retained according to the project engineer.

Historical screenshots from the original development period are not currently available.

Current screenshots and technical records may be captured from the original server to document its configuration and architecture.

Any new screenshots will be identified using their actual capture dates.

Current evidence will not be represented as having been created during the original development period.

The current GitHub documentation was prepared retrospectively to describe the original engineering implementation.

Its publication date is not evidence of the original project implementation date.

---

## 8. Infrastructure Evidence

The original infrastructure provides an opportunity to obtain technical evidence of the implementation.

Relevant evidence may include:

- Proxmox virtual machine configuration.
- VOS3000 virtual machine information.
- Asterisk virtual machine information.
- Linux operating-system information.
- Asterisk network interface configuration.
- SIP gateway configuration.
- Static routing configuration.
- Asterisk SIP and dialplan configuration.
- SIP signalling and RTP media troubleshooting records.

Any collected evidence should be dated and reviewed to remove confidential information before publication.

The presence of the original configuration can help demonstrate the technical architecture.

It does not independently establish the original development date, commercial deployment status or historical performance.

---

## 9. Performance and Capacity

The platform's simultaneous-call capacity depends on factors including:

- Available processor resources.
- System memory.
- Network bandwidth.
- Codec selection.
- RTP media processing requirements.
- Asterisk configuration.
- Softswitch and telecommunications infrastructure capacity.

A verified simultaneous-call capacity has not been established in this documentation.

No specific call-capacity or performance benchmark is claimed.

Any future performance results should identify the testing date, infrastructure configuration, test methodology and measured results.

---

## 10. Independent Supporting Evidence

The project may be supported by independent confirmation from the engineering organisation and the client.

### CRTLHost

CRTLHost was the engineering organisation on whose behalf the project was undertaken.

Its CEO can provide confirmation of the project's background, engineering responsibilities, development period and nature of the implementation.

### The Goal

The Goal was the client for whom the R&D project was developed.

A customer evidence letter has been received and may provide independent confirmation of relevant aspects of the project.

The precise contents and evidential scope of the supporting letters should be reviewed separately.

Confidential correspondence and personal contact details are not reproduced in this public repository.

---

## 11. Evidence Limitations

The technical documentation in this repository is a retrospective account of the original engineering work.

The repository does not contain recovered historical source code or complete original production configuration files.

The available original server may provide current technical evidence of the retained implementation.

Current screenshots and demonstrations will be distinguished from historical records.

The project is described as a research and development implementation rather than a commercially deployed production service.

No unverified performance figures, implementation dates or historical technical results are claimed.

---

## 12. Related Documentation

The following documents provide further details about the engineering implementation:

- [Technical Architecture](architecture.md)
- [Network Routing and SIP/RTP Interworking](network-routing.md)
- [SIP Gateway Configuration and Call Processing](sip-gateway-configuration.md)

---

## 13. Author

**Mohammad Sorower Jahan**

Digital Technology & Telecommunications Infrastructure Engineer

**GitHub:** [Core-daemon](https://github.com/Core-daemon)

**Professional Website:** [www.msjahan.com](https://www.msjahan.com)

---

*This document provides a retrospective technical record of an engineering research and development project undertaken in 2025. Supporting evidence must be evaluated according to its original source, date and independently verifiable content.*
