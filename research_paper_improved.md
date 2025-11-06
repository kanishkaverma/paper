# Data Privacy in Wearable Health Devices: Evolution of Security Architectures for Real-Time Monitoring

**Kanishka Verma**
Computer Architecture and Systems D794
RPN1 Evolution Evaluation Research Paper

## Abstract

Wearable health devices collect highly sensitive personal health data, raising critical privacy and security concerns. This paper examines how security architectures in wearable health devices have evolved over the past decade, transforming from basic afterthoughts into core design principles. Modern systems implement multi-layered security: wireless encryption, on-device processing, and privacy-preserving machine learning. Drawing on recent research from 2023 to 2025, this paper analyzes security threats, current protection methods, vulnerabilities, sustainability challenges, and ethical considerations, concluding with future developments including post-quantum cryptography and enhanced attestation mechanisms.

## 1. Introduction

### 1.1 Topic and Scope

This paper examines the security and privacy architecture of wearable health devices within the Internet of Medical Things (IoMT). The typical data flow follows: **Sensor → Wireless connection → Phone/Gateway → Secure processing → Cloud storage**. Understanding protection at each step is crucial, as these devices collect intimate health information including heart rate, sleep patterns, activity levels, and ECG readings.

### 1.2 Why Privacy Matters

Wearable health devices collect continuous, highly personal data revealing medical conditions, daily routines, stress levels, and sleep patterns. Data breaches can lead to discrimination by insurers or employers, identity theft, and privacy violations, requiring stronger security than typical consumer electronics.

## 2. Understanding the Threats: What Can Go Wrong?

Security researchers categorize threats based on attacker capabilities:

### 2.1 Types of Attackers

**Passive Eavesdropper:** Attackers with basic radio equipment can intercept Bluetooth Low Energy (BLE) communications between device and phone, potentially viewing transmitted health data.

**Active Network Attacker (MITM):** Sophisticated attackers can intercept and modify wireless communications, trick devices into using weak encryption, replay commands, or inject false data to manipulate health readings.

**Compromised Device Owner:** Malware can access all device data, extract encryption keys, and monitor activities, representing complete local compromise and highlighting the need for hardware-level protections.

**Malicious Researcher:** Bad actors in collaborative machine learning can corrupt shared AI models by submitting manipulated training data, particularly threatening federated learning systems.

**Supply Chain Attacker:** Device tampering before customer delivery can install firmware backdoors or weaken security measures.

### 2.2 System Assumptions

Devices range from simple sensors to sophisticated processors. Some include Trusted Execution Environments (TEE), secure processor zones protecting sensitive operations even when the main system is compromised. Cloud servers are assumed "honest-but-curious," following protocols correctly while potentially attempting to access unencrypted user data.

## 3. Security Solutions: How Protection Has Evolved

### 3.1 On-Device Processing (Edge Computing)

Modern wearables process data locally before cloud transmission. Raw health data remains on the device, with only processed insights transmitted. This reduces interception opportunities and enables faster responses for time-sensitive alerts. Edge computing enables real-time processing, reducing latency and improving privacy, but faces challenges including limited computational resources and the need for efficient algorithms on constrained hardware (Rancea et al., 2024).

### 3.2 Hardware Security Features

**Trusted Execution Environments (TEE):** Secure processor areas isolated from the main operating system protect encryption keys and sensitive health data even when malware infects the device. TEEs securely store and process sensitive calculations without exposure to potentially compromised applications.

**Hardware Root of Trust:** Hardware-based security ensures safe device boot-up and tamper detection, verifying that only authentic, unmodified software runs on health devices.

### 3.3 Privacy-Preserving Machine Learning

Traditional AI requires centralized data collection, creating privacy risks. New techniques address this:

**Federated Learning:** AI models train on local device data, sending only model updates (not raw data) to servers. Servers combine updates from multiple users to improve overall models while raw health data never leaves devices.

**Differential Privacy:** Mathematical techniques add calibrated "noise" to data, preventing reverse-engineering of individual health data from model updates. The trade-off requires balancing privacy protection with AI accuracy.

**Secure Aggregation:** Cryptographic methods combine data from multiple users without any party seeing individual contributions, enabling population-level health insights without exposing personal data.

### 3.4 Wireless Communication Security

Wearable devices use Bluetooth Low Energy (BLE) for smartphone communication. BLE security has evolved from early problems (unencrypted transmissions, predictable pairing, trackable identifiers) to modern protections (BLE Secure Connections with strong encryption, rotating device identifiers, authenticated pairing). However, 2024 research still finds vulnerabilities in identifier rotation, potentially enabling tracking despite encryption (Wu et al., 2024).

## 4. Evolution Timeline: How We Got Here

Wearable health device security has evolved through five distinct phases:

**Phase 1: Cloud-Centric Era (~2010-2016)** - Raw sensor data sent to cloud with basic HTTPS encryption; lacked wireless link protection and risked mass data breaches.

**Phase 2: Link-Layer Hardening (~2016-2020)** - Strengthened Bluetooth with BLE Secure Connections and improved pairing; still relied on cloud processing.

**Phase 3: Edge Analytics and Secure Enclaves (~2020-2022)** - On-device processing using TEEs with hardware-protected keys and device attestation; significantly reduced data transmission and protected against OS compromise.

**Phase 4: Privacy-Preserving Collaborative Learning (~2022-2024)** - Federated learning with differential privacy and secure aggregation enabled AI training without sharing raw data, providing mathematical privacy guarantees for population-level insights (Abbas et al., 2024).

**Phase 5: Post-Quantum and Auditable Systems (~2023-2025)** - Testing post-quantum cryptography, blockchain-inspired audit trails, and formal protocol verification for long-term security with user-controllable privacy settings (Wu et al., 2024; Paju et al., 2023; Baciu et al., 2025).

Privacy has shifted from an add-on feature to a fundamental architectural requirement (Zhang et al., 2025).

## 5. Current Challenges and Vulnerabilities

Despite progress, real-world security issues persist:

### 5.1 Bluetooth Low Energy Weaknesses

Security audits reveal ongoing problems: unencrypted transmissions, weak identifier rotation enabling user tracking, exposed diagnostic interfaces, and pairing vulnerabilities allowing man-in-the-middle attacks. 2024 research demonstrated practical attacks including user tracking and remote battery drainage (Cook et al., 2024; Wu et al., 2024).

### 5.2 Federated Learning Vulnerabilities

While privacy-preserving in principle, federated learning faces risks: model inversion attacks can extract training data information from updates, model poisoning corrupts AI models through malicious updates, and weak validation enables easier exploitation.

### 5.3 Device Management at Scale

Managing large device deployments requires secure boot and updates across diverse hardware, efficient key distribution and rotation, and balancing centralized control with individual privacy.

## 6. Practical Considerations

### 6.1 Energy and Sustainability

Battery life is critical for wearables; security features must be energy-efficient. Energy drains from constant wireless transmission, encryption, and cloud synchronization can be addressed through local data processing with summary-only transmission, batched uploads, lightweight cryptography, and adaptive sampling. Poorly designed health apps significantly drain batteries, highlighting the need for efficient privacy-preserving designs (Almasri et al., 2024).

### 6.2 Reliability and Updates

Wearable devices require signed updates for manufacturer verification, rollback protection against vulnerable versions, dual partition systems for update failure recovery, and watchdog mechanisms for automatic crash recovery. Secure firmware updates are critical for patching post-deployment vulnerabilities without compromising device integrity (Zhang et al., 2025).

### 6.3 Computing Systems Performance

Wearable health devices present unique computing systems challenges due to their heterogeneous, distributed architectures. Advantages include distributed processing that enables workload sharing between wearable devices, smartphones, and cloud servers; scalability through tiered computing architectures that can accommodate growing user bases; and flexible resource allocation that adapts to varying computational demands. However, significant challenges arise from severe resource constraints on wearable processors, including limited memory (often under 256KB RAM), restricted processing power, and minimal storage capacity. System complexity increases as security mechanisms must operate across multiple computing tiers with different trust levels and capabilities. Furthermore, real-time processing requirements for health monitoring conflict with energy efficiency needs, creating difficult optimization trade-offs. The heterogeneous nature of IoMT deployments, where devices range from simple sensors to sophisticated processors, complicates system design and management at scale (Rancea et al., 2024; Zhang et al., 2025).

## 7. Future Directions

### 7.1 Federated Learning by Default

Future systems will adopt privacy-preserving machine learning as standard, including configurable privacy budgets for user-controlled privacy/utility trade-offs, automatic secure aggregation, and architectural privacy guarantees.

### 7.2 Post-Quantum Cryptography

Current encryption may be vulnerable to quantum computers, requiring proactive preparation. Hybrid cryptography combines current and post-quantum algorithms during transition, with careful migration paths ensuring secure communication between old and new devices. Long-term planning is critical for multi-year medical device lifespans. Research is testing post-quantum algorithms for medical IoT systems (Ravisankar & Maheswar, 2025; Sabrina et al., 2024).

### 7.3 Enhanced Attestation

Future systems will verify firmware versions, security patch levels, AI model versions, and perform continuous runtime integrity checks, accepting data only from verifiably secure devices.

## 8. Ethical Considerations

Technical security alone doesn't address all ethical concerns:

### 8.1 Access and Equity

Vulnerable populations may lack access to secure devices or knowledge to use privacy features. More secure devices may create a "privacy divide" between wealthy and poor communities, with language and literacy barriers preventing understanding of privacy settings.

### 8.2 Autonomy and Consent

Users require meaningful control over health data through granular consent for different data types, easy-to-understand usage explanations, and simple consent revocation and data deletion.

### 8.3 Surveillance and Freedom

Employer or insurance-mandated wearables create coercive pressure for health monitoring participation. Constant monitoring may reduce personal autonomy, and data aggregation enables discrimination despite individual record privacy.

Technical solutions require strong governance, transparent policies, and user-centered design to address these ethical dimensions (Capulli et al., 2025; Sun et al., 2024; Sui et al., 2023).

## 9. Conclusion

Wearable health device security has transformed from basic cloud security into sophisticated multi-layered protection spanning hardware, wireless links, on-device processing, and privacy-preserving machine learning. Modern systems implement security as fundamental architecture: TEEs protect data on compromised devices, federated learning enables population insights without centralized collection, and advanced cryptography provides mathematical privacy guarantees.

Significant challenges remain: Bluetooth vulnerabilities enable tracking, federated learning faces model inversion and poisoning risks, energy constraints limit cryptographic options, and ethical concerns about access, consent, and surveillance require non-technical solutions.

The field is moving toward federated-by-default architectures, post-quantum cryptographic readiness, and enhanced attestation. Combined with strong governance and user-centered design, these advances will be essential as wearable health monitoring integrates into healthcare delivery. As devices become more capable and monitoring more pervasive, security architecture must continue adapting, prioritizing patient privacy alongside clinical benefit.

---

## References

Abbas, S. R., Abbas, Z., Zahir, A., & Lee, S. W. (2024). Federated learning in smart healthcare: A comprehensive review on privacy, security, and predictive analytics with IoT integration. *Healthcare, 12*(24), 2587. https://doi.org/10.3390/healthcare12242587

Almasri, A., Rios, J., Dallas, J., Kramer, K., & Karpinski, A. C. (2024). Evaluating the energy efficiency of popular US smartphone healthcare apps: A comparative analysis study toward sustainable health and nutrition app practices. *JMIR Human Factors, 11*, e58311. https://doi.org/10.2196/58311

Baciu, V.-E., Braeken, A., Segers, L., & da Silva, B. (2025). Secure Tiny Machine Learning on edge devices: A lightweight dual attestation mechanism for machine learning. *Future Internet, 17*(2), 85. https://doi.org/10.3390/fi17020085

Capulli, E., Druda, Y., Palmese, F., Butt, A. H., Domenicali, M., Macchiarelli, A. G., Silvani, A., Bedogni, G., & Ingravallo, F. (2025). Ethical and legal implications of health monitoring wearable devices: A scoping review. *Social Science & Medicine, 370*, 117685. https://doi.org/10.1016/j.socscimed.2025.117685

Cook, S., Mehrnezhad, M., & Toreini, E. (2024). Bluetooth security analysis of general and intimate health IoT devices and apps: The Case of FemTech. *International Journal of Information Security, 23*(6), 3547–3567. https://doi.org/10.1007/s10207-024-00883-3

Paju, A., Javed, M. O., Nurmi, J., Savimäki, J., McGillion, B. B., & Brumley, B. B. (2023). SoK: A systematic review of TEE usage for developing trusted applications. In *Proceedings of the 18th International Conference on Availability, Reliability and Security* (ARES'23). https://doi.org/10.1145/3600160.3600169

Rancea, A., Anghel, I., & Cioara, T. (2024). Edge computing in healthcare: Innovations, opportunities, and challenges. *Future Internet, 16*(9), 329. https://doi.org/10.3390/fi16090329

Ravisankar, S., & Maheswar, R. (2025). SecureEdge-MedChain: A post-quantum blockchain and federated learning framework for real-time predictive diagnostics in IoMT. *Sensors, 25*(19), 5988. https://doi.org/10.3390/s25195988

Sabrina, F., Sohail, S., & Tariq, U. U. (2024). A review of post-quantum privacy preservation for IoMT using blockchain. *Electronics, 13*(15), 2962. https://doi.org/10.3390/electronics13152962

Sun, L., Yang, B., Kindt, E., & Chu, J. (2024). Privacy barriers in health monitoring: Scoping review. *JMIR Nursing, 7*, e53592. https://doi.org/10.2196/53592

Sui, A., Sui, W., Liu, S., & Rhodes, R. E. (2023). Ethical considerations for the use of consumer wearables in health research. *Digital Health, 9*, 20552076231153740. https://doi.org/10.1177/20552076231153740

Wu, J., Traynor, P., Xu, D., Tian, D. J., & Bianchi, A. (2024). Finding traceability attacks in the Bluetooth Low Energy specification and its implementations. In *Proceedings of the 33rd USENIX Security Symposium*. https://www.usenix.org/conference/usenixsecurity24/presentation/wu-jianliang

Zhang, B., Chen, C., Lee, I., Lee, K., & Ong, K.-L. (2025). A survey on security and privacy issues in wearable health monitoring devices. *Computers & Security, 155*, 104453. https://doi.org/10.1016/j.cose.2025.104453
