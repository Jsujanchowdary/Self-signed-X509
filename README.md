# Self-Signed X.509 Certificate Generator

This repository contains a Bash script to generate self-signed X.509 certificates. These certificates can be used for secure communication in various applications, such as testing, development, or non-critical production scenarios.

## Table of Contents
- [Overview](#overview)
- [Features](#features)
- [Prerequisites](#prerequisites)
- [How to Use](#how-to-use)
- [Explanation of the Script](#explanation-of-the-script)
- [When to Use Self-Signed Certificates](#when-to-use-self-signed-certificates)
- [Limitations](#limitations)


---

## Overview
An X.509 certificate is used in cryptographic protocols like SSL/TLS for authenticating servers and encrypting communications. Self-signed certificates are not issued by a trusted Certificate Authority (CA) but are instead signed with their own private key.

This script simplifies the creation of such certificates by automating the process using OpenSSL.

---

## Features
- Generates an RSA private key.
- Creates a Certificate Signing Request (CSR).
- Issues a self-signed X.509 certificate.
- Customizable certificate information and validity period.

---

## Prerequisites
- **Bash Shell**: This script is written for Linux or macOS systems with a Bash shell.
- **OpenSSL**: Ensure that OpenSSL is installed on your system. You can check by running:

  ```bash
  openssl version

  To install OpenSSL:
  - On Debian/Ubuntu-based systems:
    ```bash
    sudo apt update && sudo apt install openssl
    ```
  - On macOS:
    ```bash
    brew install openssl
    ```

---

## How to Use
1. **Clone the Repository:**
   ```bash
   git clone https://github.com/your-username/self-signed-cert-generator.git
   cd self-signed-cert-generator
   ```

2. **Customize the Script:**
   Open the script `generate_cert.sh` and edit the following variables to suit your requirements:
   - `COMMON_NAME`
   - `ORGANIZATION`
   - `COUNTRY`
   - `STATE`
   - `LOCALITY`
   - `ORGANIZATIONAL_UNIT`
   - `EMAIL`
   - `VALIDITY_DAYS`

3. **Make the Script Executable:**
   ```bash
   chmod +x generate_cert.sh
   ```

4. **Run the Script:**
   ```bash
   ./generate_cert.sh
   ```

5. **Output:**
   After successful execution, two files will be generated:
   - `private_key.pem`: The private key.
   - `certificate.pem`: The self-signed X.509 certificate.

---

## Explanation of the Script
### Key Steps:
1. **Generate Private Key:**
   The script generates a 2048-bit RSA private key using:
   ```bash
   openssl genpkey -algorithm RSA -out "private_key.pem"
   ```

2. **Create CSR:**
   A Certificate Signing Request (CSR) is generated using the private key:
   ```bash
   openssl req -new -key "private_key.pem" -out "certificate.csr" -subj "/CN=..."
   ```

3. **Self-Sign the Certificate:**
   The CSR is signed with the private key to produce a self-signed certificate:
   ```bash
   openssl x509 -req -days 365 -in "certificate.csr" -signkey "private_key.pem" -out "certificate.pem"
   ```

4. **Cleanup:**
   The temporary CSR file is deleted.

---

## When to Use Self-Signed Certificates
Self-signed certificates are suitable for:
- Internal testing and development environments.
- Non-critical applications where the trust chain is not a concern.
- Securing communications within closed systems.

---

## Limitations
- Self-signed certificates are not trusted by browsers or external systems.
- They are unsuitable for public-facing websites or applications requiring trusted communication.
