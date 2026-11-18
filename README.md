# AI-Assisted DFIR Log Triage & Post-Quantum Encryption Pipeline

**BSc (Hons) Computer Forensics & Security — Final Dissertation Project**  
*Canterbury Christ Church University (2026–2027)*

## Overview

Security Operations Centers (SOC) and DFIR analysts face severe alert fatigue while processing sensitive forensic artifacts that must remain confidential against long-term cryptographic threats (*Harvest Now, Decrypt Later*).

This research architecture implements an air-gapped hybrid pipeline:
1. **Local Automated Triage:** Deploys quantized Small Language Models (SLMs) locally to normalize and classify raw Sysmon, EVTX, and syslog events against the **MITRE ATT&CK** framework with zero external cloud telemetry leakage.
2. **Post-Quantum Chain of Custody:** Protects generated forensic reports and evidence bundles using a hybrid key-encapsulation scheme combining **NIST FIPS 203 (ML-KEM)** with AES-256-GCM.

## Pipeline Architecture

```mermaid
flowchart LR
    Logs["Raw Telemetry (EVTX / Sysmon / Syslog)"] --> Parser["Log Normalizer (Python)"]
    Parser --> SLM["Local Quantized SLM"]
    SLM --> MITRE["MITRE ATT&CK Classification"]
    MITRE --> PQC["Hybrid Encryption (NIST ML-KEM + AES-256-GCM)"]
    PQC --> Vault["Tamper-Evident Evidence Archive"]
