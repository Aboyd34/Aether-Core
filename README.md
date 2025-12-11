# Aether – Communication Without Witnesses

Aether is a next-generation, privacy-first communication protocol designed for environments where surveillance, metadata collection, and network interference are the norm.

Instead of relying on centralized servers and account systems, Aether uses:

- **Peer-to-peer networking**
- **End-to-end encryption**
- **Zero-knowledge verification**
- **Ephemeral communication (no logs, no history)**

Aether is built as a public good for journalists, activists, human rights defenders, and anyone who needs to communicate without being watched.

---

## Project Status

> **Status:** Early development / MVP planning  
> **Grant:** Submitted to Open Technology Fund – Internet Freedom Fund  
> **Code:** This repository will track the reference implementation of Aether Core, Aether Nodes, and Aether Conduit.

This repository currently focuses on documentation, architecture, and initial implementation scaffolding. As the MVP matures, code, tests, and specs will be added here.

---

## Core Ideas

Aether is designed around four principles:

1. **No Witnesses**  
   No central server, no persistent identity, no readable metadata. Intermediaries route encrypted blobs without seeing who is talking or what is being said.

2. **Censorship Resistance**  
   Traffic is routed over a distributed mesh using multiple transports (TCP, QUIC, WebRTC, Tor, etc.) with optional obfuscation layers to make blocking difficult and expensive.

3. **Zero-Knowledge Security**  
   Access, permissions, and authenticity are validated using cryptographic proofs, not stored user accounts. Verification without exposure.

4. **Open and Auditable**  
   Aether is built as free and open-source software so that anyone can inspect, verify, and improve the security model.

---

## High-Level Architecture

Aether is composed of three major components:

### 1. Aether Core

Runs on the user’s device and handles:

- Session setup and key exchange  
- End-to-end encryption / decryption  
- Zero-knowledge challenge / response  
- Local metadata minimization (no contact list upload, no history storage)

**Planned cryptographic stack:**

- `Ed25519` – signatures  
- `X25519` – key exchange  
- `ChaCha20-Poly1305` – AEAD encryption  
- `Noise`-based handshakes (XX / X3DH-style patterns)  
- Zero-knowledge proof primitives for access / ownership checks

### 2. Aether Nodes (P2P Layer)

A mesh of lightweight nodes responsible for:

- Peer discovery and routing (libp2p-style Kademlia)  
- Multi-hop forwarding for anonymity  
- Pluggable transports:
  - TCP / QUIC  
  - WebRTC (where applicable)  
  - Tor / bridge-like relays in hostile networks  

Nodes never see plaintext messages and do not retain logs.

### 3. Aether Conduit (ZK Relay)

An optional, blind relay service:

- Forwards encrypted blobs between peers  
- Runs on a minimal surface (e.g. port `8088`)  
- Stores nothing and exposes no user identifiers  
- Designed so that compromise yields no usable data

Conduits exist to help users in heavily restricted or NAT-locked environments join the network without sacrificing privacy.

---

## Threat Model (Summary)

Aether is being designed to reduce risk against:

- **State-level surveillance** and centralized logging  
- **Global passive adversaries** monitoring traffic patterns  
- **Active adversaries** attempting man-in-the-middle attacks  
- **Server compromise** and mass-data exfiltration  
- **Account-based unmasking** of users

No system is perfect, but Aether’s architecture aims to remove as many structural weaknesses as possible:

- No central database to seize  
- No accounts to subpoena  
- No message history to review  

---

## Repository Structure (Planned)

```text
aether-core/
├─ cmd/
│  ├─ aether-node/       # CLI for running a node
│  ├─ aether-conduit/    # CLI for running a conduit relay
│  └─ aether-client/     # Experimental client interface
├─ internal/
│  ├─ crypto/            # Key management, Noise handshakes, ZK helpers
│  ├─ net/               # libp2p wrappers, routing, transports
│  ├─ storage/           # Ephemeral in-memory buffers (no long-term logs)
│  └─ config/            # Safe defaults, config parsing
├─ docs/
│  ├─ architecture.md
│  ├─ threat-model.md
│  └─ roadmap.md
├─ tests/
│  ├─ integration/
│  └─ fuzz/
└─ LICENSE
