# Aether Threat Model

Aether is designed for users facing state-level adversaries, censorship systems, and network monitoring.

## Adversaries

- Global passive surveillance
- Traffic correlation attackers
- MITM active adversaries
- Compromised infrastructure nodes
- Metadata collectors

## User Assumptions

- Devices may be confiscated
- Networks may be blocked
- Traffic may be fingerprinted
- Physical safety may depend on secrecy

## Threat Mitigations

### Metadata Minimization
- No accounts
- No phone numbers
- No logs or history
- Ephemeral keys

### Network-Level Protections
- Multi-hop routing
- Packet padding and timing noise
- Domain fronting / Tor bridges

### Cryptographic Protections
- Noise-based key exchange
- ChaCha20-Poly1305 AEAD
- ZK proofs for non-identifying validation

### Failure Containment
Compromise of one node does not:
- Reveal past communications
- Reveal user identity
- Expose routing tables

Aether assumes the network is hostile and designs accordingly.
