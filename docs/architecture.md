# Aether Architecture Overview

Aether is a distributed, metadata-minimized communication protocol designed for hostile environments.

## System Components

### 1. Aether Core
Runs locally and handles:
- Encryption / decryption
- Noise-based key exchange
- Zero-knowledge validation
- Metadata scrubbing

### 2. Aether Node (P2P Mesh)
Responsible for:
- Peer discovery
- Routing (libp2p Kademlia)
- Multi-hop anonymity
- Obfuscation layers (QUIC, WebRTC, Tor)

### 3. Aether Conduit (ZK Relay)
A blind forwarding service:
- Cannot decrypt messages
- Stores zero data
- Helps restricted users reach the mesh

## Data Flow

