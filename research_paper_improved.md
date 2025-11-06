# Data Privacy in Wearable Health Devices: Evolution of Security Architectures for Real-Time Monitoring

**Kanishka Verma**
Computer Architecture and Systems D794
RPN1 Evolution Evaluation Research Paper

## Abstract

Wearable health devices like fitness bands, smart rings, and ECG patches are becoming increasingly common in healthcare. However, these devices collect highly sensitive personal health data, raising important questions about privacy and security. This paper examines how security measures in wearable health devices have evolved over the past decade.

The research shows that privacy protections have transformed from basic afterthoughts into core design principles. Modern wearable systems now implement security at every stage: from the wireless connection between device and phone, to data processing on the device itself, to cloud-based analysis. Drawing on recent research from 2023 to 2025, this paper explains the major security threats, describes current protection methods, and discusses ethical considerations. It concludes by exploring future developments, including advanced privacy-preserving machine learning and preparations for new cryptographic standards.

## 1. Introduction

### 1.1 Topic and Scope

This paper focuses on the security and privacy architecture of wearable health devices, a subset of the Internet of Medical Things (IoMT). IoMT refers to the network of medical devices and applications that connect to healthcare systems through the internet.

The typical data flow in these systems looks like this:
**Sensor → Wireless connection → Phone/Gateway → Secure processing → Cloud storage**

Understanding how data is protected at each step is crucial, as wearable devices collect intimate health information including heart rate, sleep patterns, activity levels, and even ECG readings. This topic connects directly to computer architecture and systems design, cybersecurity principles, and the growing field of healthcare technology.

### 1.2 Why Privacy Matters in Wearable Health Devices

Unlike most consumer electronics, wearable health devices collect continuous, highly personal data about our bodies. This data can reveal medical conditions and health status, daily routines and location patterns, stress levels and emotional states, and sleep quality and habits. If this data is stolen, leaked, or misused, it can lead to discrimination (e.g., by insurers or employers), identity theft, or serious privacy violations. Therefore, these devices require stronger security than typical consumer gadgets.

## 2. Understanding the Threats: What Can Go Wrong?

To design effective security, we must first understand the potential threats. Security researchers categorize attackers into several types based on their capabilities:

### 2.1 Types of Attackers

**Passive Eavesdropper:** This threat involves someone with basic radio equipment who can listen to wireless signals. Such attackers can intercept Bluetooth Low Energy (BLE) communications between your device and phone. This matters because even if they can't change anything, they might see your health data being transmitted.

**Active Network Attacker (Man-in-the-Middle or MITM):** A more sophisticated attacker who can intercept and modify wireless communications presents a more serious threat. These attackers can trick your device into using weak encryption, replay old commands, or inject false data. This is concerning because they could manipulate your health readings or gain control of device functions.

**Compromised Device Owner:** When malware or malicious software gains control of your wearable or smartphone, it can access all data stored on the device, extract encryption keys, and monitor everything. This represents complete local compromise, highlighting the need for hardware-level protections.

**Malicious Researcher (Model Poisoning):** A bad actor participating in collaborative machine learning research poses unique risks by corrupting the shared AI models through submitting manipulated training data. This threat is particularly relevant for newer systems that use federated learning (explained later).

**Manufacturer Insider or Supply Chain Attacker:** Someone who tampers with devices before they reach customers can install backdoors in the firmware or weaken security measures. This demonstrates that even trusted brands can be compromised at the manufacturing stage.

### 2.2 System Assumptions

This analysis assumes devices range from simple sensors with minimal computing power to sophisticated processors. Some devices include Trusted Execution Environments (TEE), special secure zones in the processor that protect sensitive operations even if the main system is compromised. Additionally, cloud servers are assumed to be "honest-but-curious", meaning they follow protocols correctly but might try to peek at user data if it isn't properly encrypted.

## 3. Security Solutions: How Protection Has Evolved

### 3.1 On-Device Processing (Edge Computing)

**What it is:** Instead of sending raw health data directly to the cloud, modern wearables process data locally on the device first.

**How it helps:** This approach ensures your raw heart rate data stays on your wrist, with only processed insights (like "your average heart rate was 72 bpm") getting transmitted. Less data traveling over the network means fewer opportunities for interception, and the system provides faster responses for time-sensitive health alerts. For example, a smart ring might analyze your sleep patterns locally and only upload a summary report, rather than transmitting every heartbeat throughout the night.

Edge computing has transformed healthcare by enabling real-time data processing at the device level, reducing latency and improving privacy. However, it also introduces challenges including limited computational resources on small devices and the need for efficient algorithms that can run on constrained hardware (Rancea et al., 2024).

### 3.2 Hardware Security Features

**Trusted Execution Environments (TEE):** A secure area inside the device's processor that's isolated from the main operating system provides critical protection. Even if malware infects your device, the TEE keeps encryption keys and sensitive health data protected. In real-world use, the TEE securely stores your health data and processes sensitive calculations without exposing them to potentially compromised apps.

**Hardware Root of Trust:** Security built into the device's hardware that can't be modified by software ensures the device boots up safely and hasn't been tampered with. This verifies that only authentic, unmodified software runs on your health device.

### 3.3 Privacy-Preserving Machine Learning

Modern health devices use artificial intelligence to detect patterns and provide insights. However, traditional AI requires collecting everyone's data in one place (a privacy nightmare). New techniques address this challenge.

**Federated Learning:** Instead of sending your data to a central server, the AI model comes to your device. The process works as follows: your device trains the AI model using only your local data, then only the updated model (not your data) is sent back to the server. The server combines updates from many users to improve the overall model, and your raw health data never leaves your device. This provides a significant privacy benefit, as the cloud never sees your actual health measurements, only mathematical model updates.

**Differential Privacy:** This mathematical technique adds carefully calculated "noise" to data. Even if someone sees the AI model updates, they can't reverse-engineer individual users' health data. However, there is a trade-off: too much noise makes the AI less accurate, while too little exposes privacy. Designers must find the right balance.

**Secure Aggregation:** A cryptographic method allows combining data from multiple users without any single party (including the server) seeing individual contributions. The server receives only the combined result, never individual updates. This enables population-level health insights without exposing anyone's personal data.

### 3.4 Wireless Communication Security

Wearable devices typically use Bluetooth Low Energy (BLE) to communicate with smartphones. BLE security has improved significantly over time.

**Early problems:** Initial implementations suffered from unencrypted data transmissions that anyone nearby could intercept, predictable pairing processes that attackers could exploit, and device identifiers that allowed long-term tracking of individuals.

**Modern protections:** Contemporary systems implement BLE Secure Connections with strong encryption, regularly changing device identifiers to prevent tracking, and authenticated pairing to prevent man-in-the-middle attacks.

**Remaining challenges:** Despite these improvements, research published in 2024 still finds vulnerabilities in how some devices rotate identifiers, potentially allowing tracking even with encryption enabled (Wu et al., 2024).

## 4. Evolution Timeline: How We Got Here

The security of wearable health devices has evolved through distinct phases:

### Phase 1: Cloud-Centric Era (~2010 to 2016)
- **Approach:** Send all raw sensor data to the cloud for processing
- **Security:** Basic HTTPS encryption and app permissions
- **Limitations:** No protection for wireless links; potential for mass data breaches; privacy concerns

### Phase 2: Link-Layer Hardening (~2016 to 2020)
- **Approach:** Strengthen Bluetooth connections with better encryption
- **Security:** BLE Secure Connections, improved pairing protocols
- **Limitations:** Still sending most data to cloud; limited local processing

### Phase 3: Edge Analytics and Secure Enclaves (~2020 to 2022)
- **Approach:** Process more data on the device itself using Trusted Execution Environments
- **Security:** On-device AI, hardware-protected encryption keys, device attestation
- **Advancement:** Significantly reduced data transmission; protection even if device OS is compromised

### Phase 4: Privacy-Preserving Collaborative Learning (~2022 to 2024)
- **Approach:** Federated learning with differential privacy and secure aggregation
- **Security:** AI training without sharing raw data; mathematical privacy guarantees
- **Advancement:** Population-level insights without centralized data collection (Abbas et al., 2024)

### Phase 5: Post-Quantum and Auditable Systems (~2023 to 2025)
- **Approach:** Prepare for future cryptographic threats; implement transparent consent and auditing
- **Security:** Testing post-quantum cryptography (PQC); blockchain-inspired audit trails; formal verification of protocols
- **Advancement:** Long-term security for devices with decade-long lifespans; user-controllable privacy settings (Wu et al., 2024; Paju et al., 2023; Baciu et al., 2025)

**Key insight:** Privacy has shifted from an add-on feature to a fundamental architectural requirement (Zhang et al., 2025).

## 5. Current Challenges and Vulnerabilities

Despite significant progress, real-world security issues persist:

### 5.1 Bluetooth Low Energy Weaknesses

Recent security audits reveal ongoing problems across several dimensions. Some devices still transmit data without encryption, while weak identifier rotation allows tracking of individuals across time and location. Exposed diagnostic interfaces provide attack vectors that adversaries can exploit, and pairing vulnerabilities enable man-in-the-middle attacks. Research published in 2024 demonstrated practical attacks against popular health devices, including the ability to track users and drain device batteries remotely (Cook et al., 2024; Wu et al., 2024).

### 5.2 Federated Learning Vulnerabilities

While privacy-preserving in principle, federated learning systems face several significant risks. Model inversion attacks allow sophisticated attackers to potentially extract information about training data from model updates. Model poisoning enables malicious participants to corrupt the AI model by submitting bad updates. Furthermore, weak validation in systems that don't properly verify update integrity makes these attacks easier to execute.

### 5.3 Device Management at Scale

Managing thousands or millions of devices creates several challenges. Organizations must ensure secure boot and safe software updates across diverse hardware platforms, distribute and rotate encryption keys efficiently, and balance centralized control with individual privacy requirements.

## 6. Practical Considerations

### 6.1 Energy and Sustainability

Battery life is critical for wearables, and security features must be energy-efficient to maintain usability. Several factors contribute to energy drain, including constant wireless transmission, computationally expensive encryption, and frequent cloud synchronization. To address these challenges, developers can adopt energy-efficient approaches such as processing data locally and sending only summaries, batching uploads instead of continuous streaming, using lightweight cryptography designed for low-power devices, and implementing adaptive sampling to collect detailed data only when needed. Recent studies show that poorly designed health apps can drain smartphone batteries significantly, highlighting the need for efficient privacy-preserving designs (Almasri et al., 2024).

### 6.2 Reliability and Updates

Wearable health devices must remain functional and secure throughout their lifespan, which requires several key capabilities. Signed updates ensure that only software verified by the manufacturer is installed. Rollback protection prevents downgrading to versions with known vulnerabilities. Dual partition systems keep a backup copy of working software in case updates fail. Watchdog mechanisms automatically recover if the device freezes or crashes. Secure firmware updates and device management are critical for maintaining long-term security in wearable health devices, as vulnerabilities discovered post-deployment must be patched without compromising device integrity (Zhang et al., 2025).

## 7. Future Directions

### 7.1 Federated Learning by Default

Future systems will likely adopt privacy-preserving machine learning as the standard approach. This includes configurable privacy budgets that allow users to choose their privacy/utility trade-off, automatic secure aggregation for all collaborative learning, and privacy guarantees built into the architecture from day one.

### 7.2 Post-Quantum Cryptography

Current encryption might be vulnerable to future quantum computers, requiring proactive preparation. Hybrid cryptography uses both current and post-quantum algorithms during the transition period. Careful migration paths ensure old and new devices can communicate securely. Long-term planning is particularly important for medical devices used for many years. Research is already testing post-quantum algorithms for medical IoT systems (Ravisankar & Maheswar, 2025; Sabrina et al., 2024).

### 7.3 Enhanced Attestation

Future systems will verify more than just device identity. They will confirm the firmware version and security patch level, validate the AI model version before accepting health data, perform continuous runtime integrity checks, and only accept data from verifiably secure devices.

## 8. Ethical Considerations

Technical security alone doesn't address all ethical concerns surrounding wearable health devices:

### 8.1 Access and Equity

Vulnerable populations may lack access to secure devices or the knowledge to use privacy features effectively. The cost of more secure devices may create a "privacy divide" between wealthy and poor communities. Language and literacy barriers may prevent understanding of privacy settings, further exacerbating inequalities.

### 8.2 Autonomy and Consent

Users must have meaningful control over their health data. Consent should be granular, allowing control over different types of data separately. Systems should provide easy-to-understand explanations of how data is used and a simple ability to revoke consent and delete data.

### 8.3 Surveillance and Freedom

Employer or insurance-mandated wearables may feel coercive, creating pressure to participate in health monitoring programs. Constant health monitoring could reduce personal autonomy and freedom. Data aggregation might enable discrimination even if individual records are kept private.

Recent research emphasizes that technical solutions must be paired with strong governance, transparent policies, and user-centered design to address these ethical dimensions (Capulli et al., 2025; Sun et al., 2024; Sui et al., 2023).

## 9. Implementation Recommendations

For researchers and developers building wearable health systems, this checklist provides practical guidance:

### 9.1 Core Security Practices

First, developers should implement secure boot and signed updates. This involves verifying software authenticity before execution, protecting against rollback to vulnerable versions, and establishing hardware root of trust where possible. Second, use remote attestation to verify device integrity before accepting health data, log attestation events for audit purposes, and reject data from devices that fail verification. Third, prefer on-device processing by extracting features and preprocessing data locally, uploading only processed insights rather than raw biosignals, and implementing batched encrypted uploads to reduce transmission overhead. Fourth, adopt energy-aware security that balances cryptographic strength with battery constraints, uses adaptive sampling to reduce unnecessary data collection, and optimizes for both privacy and sustainability. Fifth, enable key rotation and management by regularly updating encryption keys, using hardware-protected key storage when available, and planning for secure key distribution at scale.

### 9.2 Research and Reproducibility

To support scientific validation and reproducibility, researchers should document and share datasets (or create synthetic equivalents that preserve privacy), publish training scripts and model architectures for federated learning systems, and conduct small-scale experiments to validate privacy/utility trade-offs before deployment.

### 9.3 Suggested Experiments

Future work could include several practical tests. BLE linkability measurement would test consumer devices to quantify tracking risks under real-world conditions. TEE performance benchmarks would measure the overhead (memory, latency, energy) of using secure enclaves for on-device health AI. A federated learning pilot could simulate a collaborative learning system with real biosignal data to test privacy parameter tuning and resistance to poisoning attacks.

## 10. Conclusion

The security and privacy architecture of wearable health devices has undergone a remarkable transformation over the past decade. What began as an afterthought (basic cloud security for centralized data) has evolved into sophisticated multi-layered protection spanning hardware, wireless links, on-device processing, and privacy-preserving machine learning.

Modern systems implement security as a fundamental architectural property. Trusted execution environments protect sensitive data even on compromised devices. Federated learning enables population-level health insights without centralized data collection. Advanced cryptographic techniques provide mathematical privacy guarantees while maintaining clinical utility.

Yet significant challenges remain. Bluetooth vulnerabilities still enable tracking and attacks. Federated learning systems face risks from model inversion and poisoning. Energy constraints limit cryptographic options. And ethical concerns about access, consent, and surveillance require solutions beyond technology alone.

Looking forward, the field is moving toward federated-by-default architectures, post-quantum cryptographic readiness, and enhanced attestation mechanisms. These advances, combined with strong governance and user-centered design, will be essential as wearable health monitoring becomes increasingly integrated into healthcare delivery.

The evolution is far from complete. As devices become more capable and health monitoring more pervasive, the security architecture must continue to adapt, always prioritizing patient privacy alongside clinical benefit.

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
