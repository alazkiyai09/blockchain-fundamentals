# Blockchain Fundamentals

Blockchain implementation from scratch demonstrating cryptographic hashing, proof-of-work, and distributed consensus — foundational concepts for federated learning security research.

## Overview

This repository contains a from-scratch implementation of blockchain technology to understand the cryptographic foundations that underpin modern distributed systems. Understanding these fundamentals is essential for:

- Cryptographic security research
- Distributed consensus mechanisms
- Tamper-evident logging systems
- Federated learning security
- Digital signature verification

## Features

- **SHA-3-256 Cryptographic Hashing**: Secure one-way hash function
- **Proof-of-Work Mining**: Custom difficulty target implementation
- **Chain Validation**: Integrity verification across all blocks
- **PCG32 Random Number Generator**: High-quality PRNG for nonce generation
- **CSV-based Persistence**: Simple blockchain storage

## Why Learn Blockchain Fundamentals?

Blockchain combines several fundamental cryptographic concepts:

1. **Hash Functions**: One-way functions that secure data integrity
2. **Merkle Trees**: Efficient verification of large data structures
3. **Digital Signatures**: Authentication and non-repudiation (ECDSA in SignGuard)
4. **Consensus Mechanisms**: Distributed agreement protocols

These concepts are directly applicable to:
- **SignGuard**: ECDSA signatures use similar cryptographic primitives
- **Federated Learning**: Blockchain can secure model updates
- **Audit Trails**: Tamper-evident logging for security events

## Code Structure

### Block Structure

Each block contains:

```python
class Block:
    index: int        # Block position in chain
    data: str         # Transaction/payload data
    time: str         # Timestamp of creation
    prevHash: str     # Hash of previous block
    nonce: int        # Proof-of-work counter
    hash: str         # Block's cryptographic hash
```

### Hashing Algorithm

```python
def sha3(data):
    return hashlib.sha3_256(data.encode('utf-8')).hexdigest()

def hashValue(index, data, timestamp, prevHash, nonce):
    allData = str(index) + str(data) + str(timestamp) + str(prevHash) + str(nonce)
    return sha3(allData)
```

### Proof-of-Work Mining

The miner searches for a nonce that produces a hash starting with a specific pattern:

```python
def addBlockchain(newData):
    # ... setup code ...
    while True:
        nonce = nonce - 1
        Hash = hashValue(index, newData, timestamp, prevHash, nonce)
        if Hash[0:6] == '00ff00':  # Difficulty target
            # Block mined successfully
            break
```

**Difficulty Target**: `00ff00` means the hash must start with these 6 hexadecimal characters.

## Installation

```bash
# Clone the repository
git clone https://github.com/alazkiyai09/blockchain-fundamentals.git
cd blockchain-fundamentals

# Install dependencies
pip install -r requirements.txt
```

## Requirements

```
numpy>=1.21.0
pandas>=1.3.0
```

## Usage

### Running the Blockchain

```bash
python blockchain.py
```

### Menu Options

1. **Create New Blockchain**: Initialize a new chain with genesis block
2. **Add New Block**: Mine and append a new block with data
3. **View Block**: Display all blocks in the chain
4. **Validate Block**: Verify chain integrity
5. **Exit**: Close the application

### Example Session

```
Blockchain

1. Create New Blockchain (Previous File Will be Deleted)
2. Add New Block or Data
3. View Block
4. Validate Block
5. Exit
Write Number of Action: 1
Blockchain Successfully Created

Write Number of Action: 2
Input New Data: Transaction: Alice sends 2 BTC to Bob
Total Time in Mining: 12.453 s
New Data Successfully Added
```

## Key Concepts

### Cryptographic Hashing

SHA-3-256 (Keccak) is used because:
- **Deterministic**: Same input always produces same output
- **Avalanche effect**: Small input changes dramatically alter output
- **Preimage resistant**: Infeasible to reverse
- **Collision resistant**: Hard to find two inputs with same hash

### Proof-of-Work

Mining requires computational work to create new blocks:
- **Purpose**: Prevents spam and ensures commitment
- **Difficulty**: Adjusted by target hash prefix
- **Nonce**: Counter incremented until target is met

### Chain Validation

Each block contains the previous block's hash, creating an immutable chain:

```
[Genesis] -> [Block 1] -> [Block 2] -> [Block 3]
     hash(0)      hash(1)       hash(2)
```

To validate, we verify:
1. Each block's hash is correct
2. Each block's `prevHash` matches the actual previous hash

## PCG32 Random Number Generator

The implementation includes PCG32, a modern random number generator:

```python
def pcg32(param1, param2, param3):
    # Permuted Congruential Generator
    # Better statistical properties than LCG
    # Used for nonce generation in mining
```

## Connection to Cryptography in SignGuard

The cryptographic concepts in this blockchain directly relate to SignGuard:

| Blockchain Concept | SignGuard Application |
|-------------------|----------------------|
| SHA-3 Hashing | Message digest for signing |
| Immutable Chain | Audit log for signatures |
| Proof-of-Work | Anti-tampering mechanism |
| Consensus | Distributed verification |

ECDSA (used in SignGuard) and blockchain both rely on:
- **Trapdoor functions**: Easy to compute, hard to reverse
- **Digital signatures**: Authentication and integrity
- **Public-key cryptography**: Key pairs for signing/verification

## Data Storage

The blockchain is persisted to `Blockchain.csv` with columns:

| Column | Description |
|--------|-------------|
| Index | Block number |
| Data | Block content |
| Time | Creation timestamp |
| Previous Hash | Hash of prior block |
| Nonce | Mining solution |
| Hash | Block's cryptographic hash |

## Security Considerations

This is a **learning implementation**. For production use:

1. **Use established libraries**: `bitcoinlib`, `web3.py`
2. **Proper key management**: Hardware security modules
3. **Network security**: TLS, authentication
4. **Consensus protocols**: PBFT, PoS, etc.

## Key Learnings

| Concept | Understanding Gained |
|---------|---------------------|
| **Hash Functions** | One-way functions for data integrity |
| **Proof-of-Work** | Computational commitment schemes |
| **Chaining** | Tamper-evident data structures |
| **Mining** | Random search for partial hash collisions |
| **Validation** | Cryptographic verification of integrity |

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Contributing

This is an educational repository. Feel free to submit issues or PRs.

## Author

**Ahmad Whafa Azka Al Azkiyai**
- GitHub: [alazkiyai09](https://github.com/alazkiyai09)
- Email: [azka.alazkiyai@outlook.com](mailto:azka.alazkiyai@outlook.com)
- Specialization: Fraud Detection & AI Security

## References

- [SHA-3 Standard (FIPS 202)](https://nvlpubs.nist.gov/nistpubs/FIPS/NIST.FIPS.202.pdf)
- [Bitcoin: A Peer-to-Peer Electronic Cash System](https://bitcoin.org/bitcoin.pdf)
- [PCG Random Number Generation](https://www.pcg-random.org/)
- [Mastering Bitcoin](https://github.com/bitcoinbook/bitcoinbook) by Andreas Antonopoulos
