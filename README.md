# **Klogger - Advanced Cross-Platform Keylogger**  
*(For Research & Educational Purposes Only)*  
![Screenshot 2025-04-03 220809](https://github.com/user-attachments/assets/558369ab-cbed-4020-8c85-7a8b7a2a5c8b)

**Author:** [Caleb Elie](https://github.com/caleb-elie)  
**License:** *This tool is for legal security research only. Unauthorized use is prohibited.*  

---

## **📌 Overview**  
`Klogger` is a **stealthy, cross-platform keylogger** designed for **penetration testing and red teaming**. It features:  
✔ **Multi-platform** (Windows & Linux)  
✔ **Advanced evasion** (anti-VM, anti-debugging)  
✔ **Multiple persistence mechanisms**  
✔ **Encrypted exfiltration** (HTTPS, DNS, ICMP)  
✔ **Process injection** (explorer.exe / sshd)  

⚠ **Warning:** Use only in **authorized environments** with explicit permission.  

---

## **⚙ Installation & Setup**  

### **Prerequisites**  
- Python 3.8+  
- Required libraries:  
  ```bash
  pip install pynput requests pyfiglet colorama pycryptodome ctypes  
  ```  

### **Usage**  
1. **Run the keylogger:**  
   ```bash
   python klogger.py
   ```
2. **Logs are:**  
   - Encrypted (AES-256 + ChaCha20)  
   - Exfiltrated via HTTPS, DNS, or ICMP  
   - Stored in memory and flushed periodically  

---

## **🔍 Features Breakdown**  

### **1. Evasion & Anti-Analysis**  
- **Debugger detection** (Windows/Linux)  
- **VM detection** (checks for VMware/VirtualBox)  
- **Security tool checks** (Wireshark, ProcMon, Volatility)  
- **Randomized sleep** (avoids sandbox detection)  

### **2. Persistence Mechanisms**  
| **OS**       | **Persistence Method**                      |  
|--------------|--------------------------------------------|  
| **Windows**  | Registry Run Key + Startup VBS Script      |  
| **Linux**    | Systemd Service + Crontab + .bashrc        |  

### **3. Data Exfiltration**  
- **HTTPS (Cloudflare, Google APIs as cover)**  
- **DNS Tunneling** (Base64-encoded chunks)  
- **ICMP Covert Channel** (Ping-based data leak)  

### **4. Encryption**  
- **AES-256-CBC** (for initial encryption)  
- **ChaCha20** (second-layer obfuscation)  
- **Zlib compression** before exfiltration  

---

## **🛡 Defensive Countermeasures**  
### **Detection Tips (For Blue Teams)**  
- **YARA Rule:**  
  ```yara
  rule Klogger_Keylogger {
      strings:
          $a = "pynput" nocase
          $b = "Crypto.Cipher" nocase
          $c = "ShadowComms" nocase
      condition:
          any of them
  }
  ```
- **Network Indicators:**  
  - Unusual HTTPS requests to `cloudflare.com/cdn-cgi/trace`  
  - DNS queries with long Base64 subdomains  
  - Abnormal ICMP payload sizes  

- **Host-Based Detection:**  
  - Suspicious process injection (`explorer.exe` with RWX memory)  
  - Unusual persistence (`system-update.service`, `update.vbs`)  

---

## **⚠ Legal & Ethical Notice**  
This tool is **for authorized security research only**.  
- **Do not use** on systems without **explicit permission**.  
- **The developer is not responsible** for misuse.  

---

## **📜 License**  
This project is under **MIT License** but **must not** be used for illegal activities.  

🔗 **GitHub:** [https://github.com/caleb-elie/klogger](https://github.com/caleb-elie/klogger)  

---

### **📌 Final Notes**  
- **For malware analysts:** Study behavior in a **sandboxed VM**.  
- **For defenders:** Use the provided YARA rules and network signatures.  
- **For pentesters:** Only deploy in **legally authorized engagements**.  

**Use responsibly!** 🛡️
