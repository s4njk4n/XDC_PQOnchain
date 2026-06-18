# XDC PQOnchain: Post-Quantum Onchain Communication

[![GitHub stars](https://img.shields.io/github/stars/s4njk4n/XDC_PQOnchain?style=social)](https://github.com/s4njk4n/XDC_PQOnchain/stargazers)
[![GitHub forks](https://img.shields.io/github/forks/s4njk4n/XDC_PQOnchain?style=social)](https://github.com/s4njk4n/XDC_PQOnchain/network/members)
[![GitHub issues](https://img.shields.io/github/issues/s4njk4n/XDC_PQOnchain)](https://github.com/s4njk4n/XDC_PQOnchain/issues)

Post-quantum encrypted messaging on the XDC blockchain. All encryption and decryption happens client-side. Uses ML-KEM-768 for key encapsulation and AES-256-GCM for message encryption. Messages are stored as transaction data onchain.

Live demo: https://s4njk4n.github.io/XDC_PQOnchain/

<img src="XDC_PQOnchain.jpg" alt="XDC PQOnchain Banner" style="max-width: 100%; height: auto; display: block; margin: 0 auto;">

## What it does

XDC PQOnchain lets you generate post-quantum (PQ) encryption keypairs, encrypt messages using a recipient's PQ encryption public key, and send them as data in XDC transactions. You can also use it to decrypt your received messages from transaction hashes using your PQ encryption private key. It's designed for secure, onchain communication that's resistant to quantum attacks.

## How it works

- **Key generation**: Creates an ML-KEM-768 encryption keypair (encryption public and private keys in hex).
- **Encryption**: Uses the recipient's encryption public key to encapsulate a shared secret, then encrypts the message with AES-GCM using that secret. The ciphertext, IV, and encapsulated key are concatenated and sent as transaction data.
- **Sending**: Connects to MetaMask on the XDC network (chain ID 50). Sends to a specified address. Optional XDC amount to transfer.  
  **Note**: MetaMask restricts sending transactions containing data to other addresses within the same wallet extension.
- **Decryption**: Fetches transaction data via RPC, extracts components, decapsulates the shared secret with your encryption private key, and decrypts the message.
- All ops are client-side; no server involvement.

Built with HTML/JS, Ethers.js for blockchain interaction, mlkem library for ML-KEM, and Web Crypto API for AES.

## How to use

1. **Generate keypair**:
   - Click "Generate Keypair".
   - Copy the encryption public and private keys (hex). Store the encryption private key securely offline.

2. **Encrypt and send message**:
   - Enter "To Address" (xdc... or 0x...).
   - Paste recipient's ML-KEM public key (hex).
   - Enter message.
   - Set XDC amount (default 0).
   - Set RPC endpoint (default: https://rpc.ankr.com/xdc).
   - Click "Connect MetaMask" (switch to XDC network if needed).
   - Click "Send Message". Confirm in MetaMask.
   - Copy the transaction hash from the status.

3. **Decrypt message**:
   - Enter transaction hash.
   - Paste your ML-KEM private key (hex).
   - Set RPC endpoint.
   - Click "Decrypt Message".
   - View decrypted message.

Note: Use MetaMask with XDC network added. If not, it prompts to add it.


## License

MIT
