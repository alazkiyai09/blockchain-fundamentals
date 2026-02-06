# Blockchain Fundamentals - Usage Guide

## How to Use

### Prerequisites

1. Install required dependencies:
```bash
pip install -r requirements.txt
```

2. Ensure Python 3.7+ is installed

### Running the Application

Start the blockchain application:

```bash
python blockchain.py
```

### Menu Options

#### 1. Create New Blockchain
- Initializes a new blockchain with a genesis block
- **Warning**: This will replace any existing `Blockchain.csv` file
- The genesis block has index 0 with "Genesis" as data

#### 2. Add New Block or Data
- Prompts for input data to add to the blockchain
- Mines a new block using proof-of-work
- Displays the time taken to mine the block
- Appends the new block to the chain

#### 3. View Block
- Displays all blocks in the current blockchain
- Shows index, data, timestamp, previous hash, current hash, and nonce

#### 4. Validate Block
- Verifies the integrity of the entire blockchain
- Checks if each block's hash is correctly computed
- Checks if each block's previous hash matches the actual previous block's hash
- Returns "Safe" if valid, "Danger" if tampering is detected

#### 5. Exit
- Closes the application

### Data Storage

The blockchain data is stored in `Blockchain.csv` with the following format:

| Index | Data | Time | Previous Hash | Nonce | Hash |
|-------|------|------|---------------|-------|------|
| 0 | Genesis | 2024-01-01 12:00:00 | 0 | 0 | 0 |
| 1 | Your data here | 2024-01-01 12:01:00 | 0 | 123456789 | 00ff01abc... |
| ... | ... | ... | ... | ... | ... |

### Testing Tamper Detection

To test the validation feature:

1. Create a blockchain
2. Add some blocks
3. Manually edit `Blockchain.csv` (change some data in a block)
4. Run "Validate Block" - it should detect the tampering and return "Danger"

### Mining Difficulty

The current difficulty target is `00ff00`, meaning the hash must start with these 6 hexadecimal characters. This provides:
- Quick mining for demonstration purposes
- Still requires computational work
- Easy to modify for different difficulty levels

To change difficulty, modify line 66 in `blockchain.py`:
```python
if Hash[0:6] == '00ff00':  # Change this pattern
```

More leading zeros = higher difficulty (longer mining time).
