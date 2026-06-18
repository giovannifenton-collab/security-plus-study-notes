# Security-Plus-Study-Notes
Security + Notes 

# 1.0 General Security Concepts

## PKI (Public Key Infrastructure)

- **Symmetric Encryption:** Uses the same key for both encryption and decryption (Shared Secret)
- **Asymmetric Encryption:** Uses a public and private key pair
- **Key Escrow:** Manages and stores large private keys in a central location until needed
- **Key Exchange:**
  - *Out-of-band:* Key is delivered outside the network (telephone, courier, in-person)
  - *In-band:* Key is delivered over the network, protected with additional encryption (e.g., using asymmetric encryption to deliver a symmetric key)
  - *Key Exchange Algorithm:* Combines known public keys with your own private key to mathematically derive a shared symmetric key

## Encryption Technologies

- **TPM (Trusted Platform Module):** Standardized hardware that provides cryptographic functions for a single computer. Generates random numbers for keys, stores keys securely, and is resistant to brute-force and dictionary attacks
- **HSM (Hardware Security Module):** Functions like a TPM but at a larger scale, serving multiple devices
- **Key Management System:** A centralized service that keeps keys separate from data and manages certificate authorities and key types
- **Secure Enclave:** A dedicated hardware processor built into a system to protect the privacy of data. Performs AES encryption and keeps data isolated from the rest of the system

## Obfuscation

The process of making information unclear or hiding it in plain sight.

- **Steganography:** Hiding information inside an image or media file. The data can only be recovered if you know how it was originally stored
- **Types of Steganography:** Network-based, embedded messages, images, invisible watermarks (machine identification codes on printers), audio and video, tokenization, and data masking

## Hashing and Digital Signatures

- **MD5:** Do not use. Has known collision vulnerabilities
- **Digital Signatures:** Used for non-repudiation, integrity, and authentication
- **Salting:** Random data added to a password before hashing to prevent pre-computed attacks
- **Key Stretching:** A technique that makes weak passwords more resistant to brute-force attacks by increasing the computational effort required to derive the key
- **Algorithms:**
  - *PBKDF2:* Key derivation function
  - *bcrypt:* Suited for high-security environments
  - *scrypt:* Memory-hard design that reduces brute-force effectiveness
  - *SHA-256:* Not ideal for password storage due to speed
  - *Argon2:* The strongest and most modern password hashing function, designed to consume memory

## HMAC (Hash-Based Message Authentication Code)

A construction that combines a cryptographic hash function with a secret key. Used to verify both data integrity and message authenticity. Commonly used in internet protocols and cryptographic applications.

## Blockchain Technology

A distributed ledger technology used to track transactions. Every participant in the blockchain has access to the ledger, and it automatically updates across all nodes when changes are made.

## Certificates

- **Root of Trust:** A foundational security characteristic where a third party vouches for the authenticity of a connection
- **Certificate Authority (CA):** Digitally signs a website's certificate, establishing trust for the browser
- **CSR (Certificate Signing Request):** A request submitted to a CA to obtain a new certificate
- **SAN (Subject Alternative Name):** Allows a certificate to cover multiple domain names
- **CRL (Certificate Revocation List):** Maintained by the CA and contains a list of revoked certificates
- **OCSP (Online Certificate Status Protocol):** Provides real-time certificate validity status when connecting to a web server
- **Certificate Pinning:** An application is hardcoded to trust only a specific certificate or key, even if another valid CA-signed certificate exists
- **Wildcard Certificate:** Covers all subdomains under a single domain, not limited to one FQDN
- **Single Domain Certificate:** Secures one specific fully qualified domain name (FQDN)

## Authentication and Authorization Protocols

- **OIDC (OpenID Connect):** Adds authentication on top of OAuth 2.0 using ID tokens
- **OAuth 2.0:** Handles authorization only, not authentication
- **SAML 2.0:** Used with SSO. Relies on XML assertions between the Identity Provider (IdP) and Service Provider (SP)
- **Kerberos:** Ticket-based authentication protocol used in Windows Active Directory environments. Authenticates the user once at login and issues a Ticket Granting Ticket (TGT). Subsequent resource requests use service tickets derived from the TGT. The password never travels across the network after initial login
- **RADIUS:** A server that provides authentication to the network through a Network Access Server (NAS). The NAS forwards credentials to the RADIUS server and opens or denies access based on the response
- **Identity Federation:** A security framework that links a user's digital identity across multiple separate identity management systems, allowing access to applications in different domains using a single set of credentials

## Key Concepts

- **Ephemeral Credentials:** Temporary, short-lived authentication tokens that automatically expire after a set period or task completion
- **Just-In-Time (JIT) Permissions:** A security model where access is granted only when needed, for a specific duration, with the minimum privileges required
- **Privilege Creep:** When a user accumulates access rights beyond what their role requires over time. Prevented through periodic access reviews
- **Data Sovereignty:** The concept that data is subject to the laws and regulations of the country where it is physically stored or collected

- # 2.0 Threats, Vulnerabilities, and Mitigations

## Memory Injection

Everything running on a computer passes through memory, including malware. To inject malware, an attacker must insert code between the starting and ending address of a running memory process such as Dynamic Link Libraries (DLLs), threads, buffers, and memory management functions. Malware can also run as its own independent process in memory.

- **DLL (Dynamic Link Library):** A Windows library containing shared code and data. One of the most common targets for memory injection attacks

## Buffer Overflow

Writing more data than an area of memory is designed to hold, causing it to overflow into adjacent memory regions. Each memory area should only hold its designated amount (e.g., 8 bits).

## Race Conditions

Occurs when two events happen simultaneously within an application and the application cannot handle both.

- **TOCTOU (Time of Check to Time of Use):** A specific type of race condition where the state of a resource changes between when it is checked and when it is used

## Malicious Updates

Software updates should be applied as soon as possible. Before updating, maintain a backup so you can revert to the last known good configuration in case an update itself contains malicious code from a compromised vendor.

## Operating System Vulnerabilities

- **Patch Tuesday:** Microsoft releases security patches on the second Tuesday of each month
- The more code an OS contains, the more potential vulnerabilities exist. Always keep systems updated

## SQL Injection (SQLi)

A code injection attack where an attacker inserts malicious SQL statements into an input field that interacts with a database. SQL (Structured Query Language) is the most common method for applications to communicate with databases. SQLi is not difficult to exploit and can reveal significant amounts of data. A common indicator is input like `("1" = 1)`.

## Cross-Site Scripting (XSS)

A browser vulnerability where malicious scripts from one site can be executed in the context of another. One of the most common web vulnerabilities. Exploits JavaScript.

- **Non-Persistent (Reflected) XSS:** The website allows scripts to run in user input fields and reflects the attack back to the user
- **Persistent (Stored) XSS:** Malicious script is stored on a third-party site (e.g., a forum or social media platform), attacking every visitor to that page
- **Prevention:** Do not click untrusted links. Keep applications updated

## Cross-Site Request Forgery (CSRF)

An attack that tricks a user's browser into submitting an unauthorized request to a website where the user is already authenticated, resulting in unintended actions being performed on their behalf.

## Injection Attacks

An attack that injects malicious code or commands into an input field, tricking the system into treating the code as a legitimate command instead of data.

## Hardware Vulnerabilities

- **Firmware:** The software embedded inside hardware devices
- **EOL (End of Life):** A manufacturer notice indicating a device is no longer being sold
- **EOSL (End of Service Life):** A manufacturer notice indicating a device will no longer receive updates or support
- **IoT Devices:** Devices connected to the network that often have limited security controls and introduce risk

## Virtualization Security

- **VM Escape:** An attack where a threat actor gains access to one hypervisor and then pivots to another, breaking out of the virtual environment
- **Resource Reuse:** The risk of sensitive data being shared between multiple virtual machines through shared resources

## Cloud-Specific Vulnerabilities

- **DoS / DDoS:** Denial of Service and Distributed Denial of Service attacks
- **Directory Traversal:** Exploiting misconfigurations to access files and directories outside the intended scope on a server. The attacker uses the website as a catalyst to reach resources on the underlying server
- **CVSS (Common Vulnerability Scoring System):** A standardized scale used to assess the severity of vulnerabilities
- **Out-of-Bounds Write:** Writing data to unauthorized memory areas outside the intended buffer

## Supply Chain Vulnerabilities

- Audit vendors frequently and ensure they are trusted sources
- Treat all new vendor devices as potentially compromised and apply security best practices during implementation

## Misconfiguration Vulnerabilities

- **Open Permissions:** Leaving data or resources exposed without proper access controls

## Mobile Device Vulnerabilities

- **Jailbreaking (iOS) / Rooting (Android):** Replacing the device OS with a third-party version to bypass built-in security controls
- **MDM (Mobile Device Manager):** Software used by organizations to monitor, manage, and secure employee mobile devices
- **Sideloading:** Installing applications from outside the official app store, bypassing vendor security vetting
- **COPE (Corporate Owned, Personally Enabled):** A model where a corporation issues devices to employees and allows personal use while retaining management and control over the device

## Zero-Day Vulnerabilities

Unidentified vulnerabilities that have no available patches at the time of discovery.

- **CVE (Common Vulnerabilities and Exposures):** A standardized identifier system for publicly known vulnerabilities

## Wireless Attacks

- **Deauthentication Attack:** Forces a device to disconnect from a wireless network
- **RF Jamming:** Decreasing the signal-to-noise ratio at the receiving device, drowning out the legitimate signal and disrupting communication

## On-Path Attacks (Man-in-the-Middle)

An attacker positions themselves between two communicating parties and potentially intercepts or alters messages.

- **ARP Spoofing / Poisoning:** A common on-path attack exploiting the ARP protocol, which lacks encryption
- **Man-in-the-Browser:** The attack runs directly on the victim's device, within the browser

## Replay Attacks

An attacker captures legitimate data and replays it to the destination to impersonate the original sender.

- **Pass the Hash:** Capturing a hashed password and using it to authenticate without knowing the actual plaintext password. Mitigated by salting
- **Session Hijacking:** Stealing a session ID after authentication to gain unauthorized access to a web session. Mitigated by encrypting all traffic with HTTPS

## Malicious Code Types

Executables, scripts, macro viruses, worms, and Trojan horses.

- **Trojan:** Appears legitimate but contains malicious functionality. Indicators include high outbound traffic and high CPU usage
- **Rootkit:** Malware that gains and maintains privileged access to a system while hiding its presence
- **Worm:** Self-replicating malware that spreads across systems and networks without user interaction
- **Prevention:** Anti-malware, firewalls, and regular patching

## Application Attacks

- **Horizontal Privilege Escalation:** An attacker gains access to another user's privileges at the same level (e.g., moving from User A to User B) without elevating to admin
- **Insecure Deserialization:** An attack where untrusted data is converted from a stored format (XML, binary) back into usable objects, allowing an attacker to execute arbitrary code
- **Open Redirect:** An attacker manipulates a legitimate website's redirect function to send users to a malicious destination. The goal is to deceive the user, not attack the server directly
- **BOLA (Broken Object Level Authorization):** An API vulnerability where an endpoint allows access to an object without verifying that the requesting user is authorized to access that specific data

## Attack Vectors Summary

| Attack | Description |
|---|---|
| SQL Injection | Malicious SQL inserted into input fields |
| XSS | Malicious scripts injected into web pages |
| CSRF | Unauthorized requests submitted via authenticated browser |
| Pass the Hash | Hashed credentials used to authenticate |
| Session Hijacking | Stolen session ID used to access authenticated sessions |
| Buffer Overflow | Memory overflow into adjacent regions |
| Directory Traversal | File path manipulation to access restricted server files |


# 3.0 Security Architecture

## Network Segmentation

Dividing a network into smaller segments to limit the scope of a security event such as a breach. Segmentation is also used to isolate high-bandwidth applications and improve overall network performance.

## Infrastructure Concepts

- **On-Premises:** All storage and systems are managed and maintained internally. Higher cost but provides full control. Creates a centralized computing model which introduces a single point of failure risk
- **Virtualization:** Each virtual machine requires its own operating system, even when running the same OS across multiple VMs
- **Application Containerization:** Multiple applications run simultaneously on the same hardware, each isolated within its own container. Encapsulates an application and its dependencies, protecting it from other applications on the same server
- **Embedded System:** A self-contained device built for a single purpose (e.g., traffic lights)
- **RTOS (Real-Time Operating System):**
  - *Deterministic:* A specific function takes priority over all others (e.g., a car's anti-lock braking system prioritizing braking functions)
  - *Non-Deterministic:* No single function takes priority over another

## Infrastructure Considerations

- **Availability:** The importance of maintaining uptime for critical systems
- **Resilience:** How quickly a system recovers after downtime
- **MTTR (Mean Time to Repair):** The average time required to restore a system after failure
- **Responsiveness:** How quickly a service delivers requested information
- **Cost:** The financial consideration of maintaining availability and redundancy

## Data Protection by State

| Data State | Protection Method |
|---|---|
| Data at Rest | Tokenization |
| Data in Transit | TLS |
| Data in Use | Memory Encryption |
| Data in Use | Secure Enclaves |

## Encryption Approaches

- **Record-Level Encryption:** Fine-grained control, encrypting individual records within a dataset
- **Partition Encryption:** Encrypts entire partitions or volumes of data
- **EFS (Encrypted File System):** Built into Windows, encrypts selected files and folders
- **FDE (Full Disk Encryption):** Encrypts everything on the drive

## Cloud and Network Security Tools

- **CASB (Cloud Access Security Broker):** Provides visibility into cloud service usage, assesses risk associated with cloud services, and enforces security policies. Specifically designed to detect and manage shadow IT and control SaaS application usage
- **SASE (Secure Access Service Edge):** Merges network and security services with WAN capabilities into a single cloud-native platform. Designed for distributed workforces requiring secure and scalable access to cloud resources
- **Secure Web Gateway:** Sits between the user and the internet to inspect outbound web traffic in real time
- **PAM (Privileged Access Management):** Controls and monitors high-privilege accounts

## DNS Tunneling

An attack method that routes non-DNS traffic through DNS port 53 to bypass network security controls.

## STIX and TAXII

- **STIX (Structured Threat Information eXpression):** A standardized language used to describe and share cyber threat intelligence in a format any system can understand
- **TAXII (Trusted Automated eXchange of Indicator Information):** The transport protocol used to securely share STIX data between systems
- # 4.0 Security Operations

## Technical Change Management

The process by which a technician implements updates, upgrades, and configuration changes. Changes are typically scheduled during downtime or within a designated change control window. Legacy applications often cannot be modified and present ongoing risk.

## System Hardening

- **OS Patching:** Always apply security patches as soon as they are available
- **Password Policy:** Enforce complexity and minimum length requirements
- **Role-Based Access (RBA):** Limit access to only the parts of the network a user needs for their role
- **Encryption:** Use EFS for file-level encryption and FDE for full disk encryption
- **EDR (Endpoint Detection and Response):** Uses behavioral analysis and machine learning to detect threats. Can take autonomous action such as isolating a system, rolling back changes, or quarantining affected components

## Mitigation Techniques

- **Patching:** Install software updates as soon as they become available
- **Encryption:** Limits the usability of data if intercepted by an attacker
- **Monitoring:** Deploy sensors, IDS, IPS, and firewalls to detect and respond to threats
- **Least Privilege:** Grant only the minimum rights and permissions required to perform a job function
- **Configuration Enforcement:** Ensure all system settings align with security baselines and remain current
- **Decommissioning:** Securely remove sensitive data from equipment before removing it from production

## Logging and Monitoring

- **Out-of-Cycle Log:** Log entries that appear at a time when they should not, which may indicate a compromise. Common in firewall logs
- **Log Tampering:** Attackers often delete logs to remove evidence. Implement detection controls to alert on unexpected log modifications
- **SIEM (Security Information and Event Management):** Collects and analyzes security logs from across an environment in real time

## Malicious Code Mitigation

Use anti-malware software, firewalls, and regular patching to defend against executables, scripts, macro viruses, worms, and Trojan horses.

## Operational Security (OPSEC)

The process of identifying and protecting information that could negatively affect business operations if disclosed to adversaries.

## UDP (User Datagram Protocol)

A connectionless network protocol that prioritizes speed over reliability. Lightweight and fast but does not guarantee delivery or order of packets.
# 5.0 Security Program Management and Oversight

## Compliance and Regulations

- **PCI DSS (Payment Card Industry Data Security Standard):** Requirements that apply to any organization that stores, processes, or transmits cardholder data
- **GDPR (General Data Protection Regulation):** Applies to any organization that interacts with European Union citizens' personal data regardless of where the organization is located
- **Data Sovereignty:** The concept that data is subject to the laws and regulations of the country where it is physically stored or collected

## Risk Management

- **SLE (Single Loss Expectancy):** The expected monetary loss from a single occurrence of a threat against an asset
- **ARO (Annualized Rate of Occurrence):** Estimates how frequently a specific threat is expected to occur within a year
- **ALE (Annualized Loss Expectancy):** The expected monetary loss per year. Calculated as: ALE = SLE x ARO

## Frameworks and Standards

| Framework | Focus |
|---|---|
| NIST CSF | Develops and measures cybersecurity standards and guidelines |
| ITIL | Best practices for IT service management |
| COBIT | Governance and controls for IT, not operational aspects |
| ISO 27001 | Creating and maintaining an information security management system |
| CIS Controls | Prioritized security best practices for cyber defense |
| OWASP | Tools, information, and guidelines specifically for web application security |

## Organizations and Groups

- **CERT (Computer Emergency Response Team):** Handles security incidents and vulnerabilities
- **W3C (World Wide Web Consortium):** Creates and maintains web standards and guidelines

## Identity and Access Management

- **SAML (Security Assertion Markup Language):** The most appropriate protocol for implementing SSO in enterprise environments. Enables employees to use one set of credentials to access multiple cloud-based applications
- **IDP (Identity Provider):** A system that authenticates users and provides identity verification to service providers
- **Identity Federation:** Links a user's digital identity across multiple separate identity management systems, allowing access to applications in different domains with a single set of credentials
- **Privilege Creep:** The gradual accumulation of access rights beyond what a user's role requires. Prevented through periodic access reviews and recertification
- **Just-In-Time (JIT) Permissions:** Access is granted only when needed, for a specific duration, with the minimum required privileges
- **Ephemeral Credentials:** Temporary, short-lived authentication tokens that automatically expire after a set period or task completion

## Threat Intelligence Sharing

- **STIX (Structured Threat Information eXpression):** A standardized language for describing cyber threat intelligence in a machine-readable format
- **TAXII (Trusted Automated eXchange of Indicator Information):** The transport protocol used to securely exchange STIX data between organizations and systems
