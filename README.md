<div align="center">

# 🔐 Crypter

### AES-256 File Encryption Utility

A lightweight, pure-Python tool for encrypting any file with **AES-256 (CBC mode)**,
using a cryptographically secure random key and IV.

![Python](https://img.shields.io/badge/Python-3.6+-3776AB?logo=python&logoColor=white)
![AES](https://img.shields.io/badge/AES-256--CBC-C72C41)
![Dependency](https://img.shields.io/badge/cryptography-lib-4B8BBE)
![Status](https://img.shields.io/badge/status-educational-orange)

</div>

---

## ✨ Features

- 🔒 **AES-256 encryption** in CBC mode with PKCS7 padding
- 🎲 **Secure randomness** — key and IV generated with Python's `secrets` module
- 📦 **Chunked I/O** — processes files in 64 KB blocks, so large files won't exhaust memory
- 🗝️ **Automatic key management** — the key is saved to a `.key` file next to the output
- 🧾 **Run report** — prints SHA-256 hashes and size overhead after each encryption
- 🧪 **Built-in self-test** mode

---

## 📋 Requirements

- Python **3.6+**
- The [`cryptography`](https://pypi.org/project/cryptography/) library

```bash
pip install cryptography
```

---

## 🚀 Usage

**Encrypt a file**
```bash
python3 crypter.py <input_file> <output_file>
```

**Example**
```bash
python3 crypter.py document.pdf document.enc
```

**Use a specific 256-bit key** (64 hex characters)
```bash
python3 crypter.py document.pdf document.enc --key <HEX_KEY>
```

**Run the built-in test**
```bash
python3 crypter.py --test
```

---

## 🧠 How It Works

| Step | Detail |
|------|--------|
| **1 · Key** | A 256-bit key is generated with `secrets.token_bytes(32)`, or supplied via `--key`. |
| **2 · IV** | A fresh 16-byte initialization vector is generated per run and written to the start of the output. |
| **3 · Cipher** | `AES-256-CBC` from the `cryptography` library encrypts the data stream. |
| **4 · Padding** | `PKCS7(128)` pads the final block to the AES block size. |
| **5 · Output** | The output is `[ 16-byte IV ][ ciphertext ]`; the key is written alongside as `<output>.key`. |

After encryption, the tool reports both file sizes, the byte overhead, and truncated SHA-256 hashes of the input and output.

---

## 📂 Output Files

| File | Contents |
|------|----------|
| `<output>` | IV followed by the encrypted data |
| `<output>.key` | Hex-encoded 256-bit key — **keep it safe; it is required for decryption** |

---

## ⚠️ Disclaimer

This project is for **educational and personal use** — a hands-on way to see how
symmetric encryption, initialization vectors, padding, and chunked file I/O fit
together. Store your key files securely: if a key is lost, the encrypted data
cannot be recovered. This is a learning project, not a substitute for a reviewed,
production-grade encryption tool.

---

<div align="center">
<sub>Built with Python 🐍 — for learning, not production use</sub>
</div>
