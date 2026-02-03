# Web Application Firewall (WAF) Home Lab

## Overview
This project demonstrates the design and implementation of a **Web Application Firewall (WAF) home lab** to simulate real-world web application attacks and evaluate defensive controls.  
The lab uses a vulnerable web application as the backend and a WAF deployed as a **reverse proxy with TLS termination**, allowing controlled attack simulation and traffic inspection.

The primary goal of this lab is to gain hands-on experience with:
- Reverse proxy architectures
- TLS/SSL termination
- Web attack patterns
- WAF detection and mitigation
- Network segmentation in virtualized environments

---

## Architecture
<img width="890" height="406" alt="pk" src="https://github.com/user-attachments/assets/ed784d3c-c624-4aea-83fd-df57358a2c88" />


### Key Design Choices
- **TLS termination at the WAF layer** to inspect decrypted traffic
- **Backend service isolation** by running DVWA on a non-public port (8080)
- **All traffic forced through the WAF**, preventing direct backend access
- **Isolated virtual network** to avoid exposure to the host or external networks

---

## Technologies Used

- Kali Linux (Attack simulation)
- Ubuntu Server (DVWA backend)
- SafeLine WAF (Reverse proxy & inspection)
- Apache (LAMP stack)
- OpenSSL (Self-signed TLS certificates)
- VMware Workstation
- Damn Vulnerable Web Application (DVWA)

---

## Implementation Summary

- Deployed DVWA on an Ubuntu server using a LAMP stack
- Configured Apache to serve DVWA on **port 8080** (backend-only access)
- Generated and deployed a **self-signed TLS certificate** for HTTPS
- Configured SafeLine WAF as a **reverse proxy on port 443**
- Onboarded the DVWA backend into the WAF configuration
- Enforced traffic flow: **Client → WAF → Backend**
- Verified correct routing and inspection via access and security logs

---

## Security Testing & Attack Simulation

The following tests were performed from the attacker machine (Kali Linux):

- SQL Injection attempts against DVWA
- HTTP flood / request burst testing
- Custom deny rule blocking attacker IP
- Validation of WAF blocking and logging behavior

All malicious requests were observed and analyzed through WAF logs.

---

## Results

- WAF successfully detected and blocked SQL injection payloads
- HTTPS traffic was terminated at the WAF and forwarded internally over HTTP
- Backend application remained inaccessible when bypassing the WAF
- Logs provided clear visibility into attack attempts and mitigation actions

---

## Key Learnings

- Reverse proxy and WAF placement in web architectures
- TLS termination design and certificate handling
- Common web attack patterns and defenses
- Importance of network segmentation and backend isolation
- Practical experience with WAF rule configuration and logging

---

## Limitations & Notes

- Self-signed certificates were used (not suitable for production)
- Signature-based detection may lead to false positives
- Lab environment does not fully replicate production traffic volume

---

## Future Improvements

- Integrate ModSecurity + OWASP CRS for comparison
- Centralize logs into a SIEM platform
- Add rate-limiting and anomaly-based detection
- Replace self-signed certificates with a trusted CA (e.g., Let's Encrypt)

---

## Documentation

A detailed technical PDF is included in this repository, covering:
- Network configuration
- SSL/TLS certificate generation
- Reverse proxy setup
- WAF onboarding and rule configuration
- Attack execution and analysis
> [View Document]

---

## Disclaimer

This lab was built strictly for **educational and defensive security research purposes** within an isolated environment.


