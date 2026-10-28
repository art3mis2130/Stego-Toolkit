#  StegoToolkit: Advanced Applied Cryptography Suite

**StegoToolkit** is a high-performance security application designed for hiding and detecting encrypted data within digital media. Utilizing **AES-256-CBC** encryption and **NumPy-optimized vectorized LSB** (Least Significant Bit) injection, it offers a robust platform for secure communication and forensic image analysis.



##  Key Features

* **Image Steganography:** Hide encrypted text inside PNG/BMP files using bit-plane manipulation.
* **AES-256 Security:** All payloads are encrypted using industry-standard AES-256-CBC with PKCS7 padding and PBKDF2 key derivation.
* **Forensic Anomaly Scanner:** A heuristic model that generates **Bit-Plane Heatmaps** to detect hidden data in suspicious images.
* **PDF Metadata Vault:** Inject secret strings into PDF document metadata fields.
* **Batch Processing:** Securely encode multiple images simultaneously and download them as a ZIP archive.
* **Real-time Capacity Analysis:** Dynamically calculates the available storage space in an image to prevent visual corruption.

---

##  Getting Started

### 1. Prerequisites
Ensure you have **Python 3.10+** installed on your system.

### 2. Installation
Clone the repository and install the required dependencies using the requirements file:

```bash
# Clone the repository
git clone https://github.com/art3mis2130/Stego-Toolkit.git
cd Stego-Toolkit

# Install dependencies
pip install -r requirements.txt
```

### Launching the application
```bash
python app.py
```
Navigate to the web address http://127.0.0.1:5000

## Project files

| File or folder | Purpose |
| --- | --- |
| `app.py` | Main Flask and Socket.IO application; serves the interface and handles image, PDF, text and live-message operations. Start this file to run the toolkit. |
| `aes.py` | Password-derived AES-CBC encryption and decryption, with an HMAC over the ciphertext. |
| `stego/lsb.py` | Image payload encoding/extraction, capacity estimates, anomaly heatmaps and visual differences. |
| `text_stego.py` | Encodes payload bits as invisible Unicode characters within cover text. |
| `pdf/pdf_crypto.py` | Stores and reads payload strings in a PDF's `/SecretKey` metadata field; encryption is handled by the caller. |
| `stego/detect_ml.py` | Auxiliary machine-learning detection code. |
| `train_model.py` | Training script for the optional detection model; review its expected training-data paths before running. |
| `templates/` | Homepage, local-toolkit and live-chat HTML interfaces. |
| `static/favicon.ico.png` | Image asset also used as the main application's default carrier. |
| `Socket_Handler.js` | Empty placeholder for separate socket-handler code; the live template currently contains the socket handlers. |
| `server.py` | Earlier alternate server implementation. It references a top-level `lsb` module and a carrier asset not present in this snapshot; use `app.py` instead. |
| `requirements.txt` | Pinned Python dependencies. |
| `__pycache__/` and nested cache folders | Included local Python 3.10 bytecode snapshots. Python normally regenerates these from source; they are not required for installation. |
| `crypto/__pycache__/` | Bytecode-only copies from a previous module layout; current editable encryption/text modules are at the repository root. |
| `.gitignore` | Rules for future untracked generated files. Explicitly committed cache files remain tracked despite these rules. |

## Local development notes

Run commands from the repository root so template, static and output paths resolve correctly. A virtual environment keeps the pinned dependencies separate from other Python projects:

```bash
python -m venv .venv
# Git Bash on Windows:
source .venv/Scripts/activate
# On Linux/macOS, use: source .venv/bin/activate
python -m pip install -r requirements.txt
python app.py
```

The app creates `uploads/` and `outputs/` when it starts. Those folders are runtime storage, not missing source directories. Keep encoded images in a lossless format and use the same bit depth during extraction. Text normalization can remove the invisible characters used by text steganography; PDF metadata tools can remove the embedded metadata field.

The supplied entry point enables Flask debug mode for local development. The live-message handlers receive passphrases on the server, so this implementation should not be described as end-to-end encryption. The anomaly scanner's results are indicators, not proof that an image contains a hidden message. No production security audit or runtime test is implied by this source upload.