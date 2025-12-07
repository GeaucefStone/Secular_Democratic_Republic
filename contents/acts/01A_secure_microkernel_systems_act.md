# THE SECURE SYSTEMS ACT

**Act Number:** ACT-0001  
**Sponsoring Department:** Department of Digital Integrity & Infrastructure  
**Date of Introduction:** [Date]

## PREAMBLE

**WHEREAS** the integrity of the state's digital infrastructure is foundational to national security, the protection of fundamental rights, and the delivery of essential services;

**WHEREAS** software vulnerabilities in critical systems, including medical devices, represent a clear and present danger to the constitutional order and the right to bodily autonomy;

**WHEREAS** microkernel architectures, which minimize code running in privileged kernel space, provide a superior security foundation over monolithic designs;

**WHEREAS** the SPARK programming language, through its use of formal verification and the elimination of undefined behavior, provides a technological means to achieve a level of assurance unattainable by conventional methods;

**WHEREAS** the Runit init system demonstrates a philosophy of simplicity, reliability, and deterministic service supervision that is ideal for high-assurance systems;

**WHEREAS** an exokernel architecture provides the most secure foundation for physical resource management and hardware multiplexing;

**BE IT ENACTED** by the Legislative Congress of the Secular Democratic Republic as follows:

---

## Section 1: Short Title

This Act may be cited as the "Secure Microkernel Systems Act."

## Section 2: Establishment of the Secure Microkernel Project (SMP)

 - There is hereby established the **Secure Microkernel Project (SMP)**, a public research and development initiative under the joint administration of the Department of Digital Integrity and the Scientific Branch.

 - The primary mandate of the SMP is to design, implement, and formally verify a new, minimal operating system based on a hybrid exokernel-microkernel architecture for use in state and critical infrastructure.

 - This microkernel shall be modeled after seL4. 

## Section 3: Core Architectural Mandate

1. **Hybrid Architecture:** The system shall employ a hybrid architecture consisting of two distinct layers:

 - **Exokernel Foundation Layer:** A minimal exokernel responsible for secure physical resource multiplexing of CPU cores, memory, and hardware interrupts.

 - **Microkernel Service Layer:** A privileged guest microkernel providing structured OS abstractions and user-space service management.

2. **Exokernel Foundation Mandate:**

 - The exokernel shall be written exclusively in SPARK and shall be formally verified in its entirety.

 - Its sole responsibility shall be secure hardware multiplexing:
  * Physical CPU core allocation and scheduling
  * Physical memory partitioning and protection
  * Hardware interrupt routing and isolation
  * Secure resource binding and revocation

 - The exokernel shall expose only low-level, hardware-like interfaces and shall impose no abstractions.

3. **Microkernel Service Layer:**

 - The microkernel shall run as a privileged guest on the exokernel foundation, modeled after the principles of seL4 and Redox OS.

 - Its responsibility shall be strictly limited to:
  * Inter-Process Communication (IPC)
  * Virtual Memory Management within its allocation
  * Task Scheduling on its allocated CPU cores
  * Capability-based security within its domain

4. **User-Space Services:** All other system components, including device drivers, file systems, and network stacks, shall run as isolated, mutually distrustful processes in user space, communicating via the microkernel's IPC mechanism.

5. **Service Management with a Runit-Modeled Init:**

 - The system shall include a primary init and service supervisor **written from the ground up in SPARK/Ada**.

 - Its design shall be **modeled after the Runit philosophy**, implementing its core principles of staged initialization, reliable service supervision, and clean process state management.

6. **Key implemented features must include:**

 - A linear, deterministic boot process divided into distinct stages.

 - A supervision tree where the init process automatically restarts failed critical services.

 - Simple service definitions based on executable directories and run scripts.

 - Clear and reliable logging of service state and termination signals.

7. **Primary Programming Language:** The exokernel, microkernel, the init system, and all system-level services shall be written predominantly in the SPARK programming language to the maximum extent technically feasible.

8. **Formal Verification:** The SMP shall prioritize the formal verification of both the exokernel's resource multiplexing and the microkernel's IPC and capability systems. The state machine of the init system shall also be a target for formal verification.

9. **Use of Ada:** Where the use of pure SPARK is impractical due to low-level hardware interaction or performance requirements validated by the Scientific Branch, the Ada programming language may be used. All such Ada code must adhere to the highest safety and security subsets of the language.

## Section 4: The "OpenBSD" Assurance Standard

The SMP shall adopt and exceed the assurance practices of the OpenBSD project through the following mandatory procedures:

 - **Rigorous Code Audit:** Every line of code committed to the SMP repository must be reviewed and approved by a minimum of two senior developers, one of whom must be a certified expert in formal methods.

 - **Proactive Vulnerability Hunting:** The project shall maintain a dedicated "Bug Bounty & Audit Team" tasked with continuous, proactive penetration testing and static analysis of the codebase.

 - **Minimalist and Clean Design:** The system shall be designed with a philosophy of minimalism, rejecting feature bloat and ensuring that every component is simple, auditable, and justifiable.

## Section 5: The Developer Catalyst Program

 - **Establishment:** The SMP shall include a **Developer Catalyst Program (DCP)** to incentivize and support the development of specialized applications on the secure base OS.

 - **Priority Domains:** The DCP shall prioritize and provide grants for projects in the following critical domains:
  * **Medical Devices:** Infusion pumps, patient monitors, diagnostic equipment.
  * **Industrial Control Systems:** SCADA, power grid management.
  * **Avionics and Transportation:** Certified software for critical vehicle systems.
  * **Financial Infrastructure:** Secure transaction processing.

 - **Support Mechanisms:** The DCP shall provide:
  * **Verified Toolchains:** Pre-certified SPARK/Ada compilers and development environments.
  * **Hardware Certification Kits:** Documentation and test suites for getting common medical and industrial hardware certified on the OS.
  * **Bounty System:** Financial bounties for the first formally verified driver or application for a piece of critical hardware.
  * **Developer Partnerships:** Direct technical support from the core SMP team for high-impact projects.

## Section 6: The On-Demand Package & Firmware Manager

 - **Development Mandate:** The SMP shall develop a package manager, named `spark-get`, whose primary design goal is **minimalism and security through on-demand provisioning.**

 - **Hardware Detection & Firmware Provisioning:**
  * Upon connecting a new device, `spark-get` shall query the hardware for its identification and required firmware checksums.
  * It shall then connect to a **Cryptographically-Signed State Software Repository** to fetch *only* the necessary, verified firmware or driver.
  * All drivers shall be implemented as user-space services, in accordance with Section 3(2).

 - **Service Integration:** Packages installed via `spark-get` that define system services shall automatically integrate with the Runit-modeled init system, creating the necessary service directories and dependencies.

 - **Anti-Bloat Principle:** The base OS installation shall contain *zero* non-essential drivers or firmware. All hardware support is acquired on-demand, ensuring a minimal initial footprint and eliminating attack surfaces for unused components.

 - **Verification and Sandboxing:** All packages installed via `spark-get` shall be:
  * Cryptographically verified against the signed repository.
  * Installed as supervised services under the init system where applicable.
  * Confined by the microkernel's capability system, limiting system access to only the resources explicitly granted.

## Section 7: Authorization for Recruitment and Training

 - The Department of Digital Integrity is hereby authorized and funded to initiate an immediate global recruitment drive to hire a minimum of fifty (50) proficient SPARK/Ada developers and formal methods experts.

 - A state-funded scholarship and training program shall be established in partnership with national universities to certify an additional two hundred (200) developers in SPARK and formal verification within three (3) years, creating a sovereign talent pipeline.

## Section 8: Phased Implementation and Deliverables

The SMP shall operate according to the following phased timeline, with reports submitted to the Scientific Branch for validation at each stage:

 - **Phase 1 (12 Months):** Completion of the formally verified exokernel foundation and a minimal microkernel capable of booting on the RISC-V and aarch64 architectures.

 - **Phase 2 (18 Months):** Development of the core Runit-modeled init/supervisor written in SPARK, the `spark-get` package manager, and a minimal set of core user-space services. Publication of the DCP guidelines and hardware certification kits.

 - **Phase 3 (24 Months):** A fully functional, self-hosting base system suitable for deployment on non-classified government web servers and network infrastructure, accompanied by a full public report on its verification status and the first wave of DCP-sponsored applications.

## Section 9: Open Source and Public Scrutiny

 - The entire codebase of the SMP, the `spark-get` manager, and all DCP-funded projects shall be released under a Copyleft license, ensuring they remain public goods and benefit from global peer review.

 - All audit reports, verification proofs, and design documents shall be published openly to maintain transparency and build international confidence in the system's security.

## Section 10: Funding

Funds necessary to carry out this Act are hereby authorized to be appropriated from the National Digital Sovereignty Fund, as established in the annual budget.

---

## JUSTIFICATION FOR CONSTITUTIONAL COMPLIANCE

 - **Basis in Article XI (National Security):** This Act directly fulfills the mandate of Article XI by creating a digitally sovereign, verifiably secure foundation for government systems, leveraging the inherent security advantages of a hybrid exokernel-microkernel architecture that provides hardware-enforced isolation.

 - **Basis in Article I, Section 6 (Bodily Autonomy):** By creating a verifiably secure platform for medical hardware using an exokernel that provides absolute hardware isolation and a microkernel that ensures continuous operation, this Act provides a technical enforcement mechanism for the right to bodily autonomy.

 - **Basis in Article IV, Section 8 (Scientific Branch):** The Act integrates the Scientific Branch into the validation process at every phase, ensuring the technical decisions—especially the hybrid architecture choice—are evidence-based and empirically sound.

 - **Methodology:** This Act follows the law-making pipeline outlined in `01G_law_making_process.md`. It originates from departmental experts, will be subjected to Scientific Branch impact assessment, and is designed to produce a technically competent, legally sound, and democratically legitimate outcome.