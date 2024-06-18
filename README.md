### ADE

This repository contains a Python script to automate the process of exploiting digital certificates using various tools. The script performs tasks such as setting up a relay with Certipy, coercing authentication with PetitPotam, acquiring certificates, and dumping user hashes.

#### Prerequisites

- Python 3.x
- Certipy
- PetitPotam
- Mimikatz
- Impacket

#### Installation

1. **Clone the repository:**
    ```bash
    git clone https://github.com/yourusername/certificate-exploitation-automation.git
    cd certificate-exploitation-automation
    ```

2. **Install required tools:**
    - **Certipy:** [Certipy Installation Guide](https://github.com/ly4k/Certipy)
    - **PetitPotam:** [PetitPotam Installation Guide](https://github.com/topotam/PetitPotam)
    - **Mimikatz:** [Mimikatz Installation Guide](https://github.com/gentilkiwi/mimikatz)
    - **Impacket:** [Impacket Installation Guide](https://github.com/SecureAuthCorp/impacket)

3. **Install Python dependencies:**
    ```bash
    pip install -r requirements.txt
    ```

#### Usage

1. **Run the script:**
    ```bash
    python exploit.py
    ```

2. **Follow the prompts to enter the required information:**
    - Domain Controller IP
    - CA Server Name
    - Listener IP
    - Target IP
    - Username
    - Password
    - Domain
    - Path to Certificate
    - Hash

#### Script Functionality

The script performs the following tasks:
1. **Setup Certipy Relay:**
    - Sets up a relay using Certipy to intercept and relay authentication requests.
2. **Coerce Authentication:**
    - Uses PetitPotam to coerce the domain controller into authenticating against the attacker's server.
3. **Acquire Certificate:**
    - Uses Certipy to obtain the certificate of the domain controller's machine account.
4. **Dump User Hashes:**
    - Utilizes Impacket's secretsdump tool to dump user hashes from the domain controller.

#### Security Warning

This script is intended for educational purposes and authorized penetration testing only. Unauthorized use of this script may be illegal and unethical. Use responsibly.

#### Contribution

Contributions are welcome! Please fork the repository and submit a pull request with your changes.

#### License

This project is licensed under the MIT License. See the LICENSE file for details.

---

By following the instructions provided, you can automate the process of exploiting digital certificates within a network environment for educational or authorized testing purposes.
