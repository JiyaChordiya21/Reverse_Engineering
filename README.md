🐀 Reverse TCP Remote Access Trojan (RAT) in Rust
📄 Project Summary
This project involves the development and analysis of a Reverse TCP Remote Access Trojan (RAT) written in Rust. The goal was to explore stealthy malware behavior, understand detection evasion techniques, and study command-and-control (C2) operations in a safe, academic environment.

Disclaimer:
This project is for educational and research purposes only. Any misuse of this knowledge is strongly discouraged.
TLP:WHITE – This information can be shared freely.

👩‍💻 Authors
Jiya Chordiya

Swaraj Tandel

Tatsam Pandey 

📦 Artifacts
🐧 ELF 64-bit RAT Executable (unstripped)

🦀 Source Code in Rust

📡 PCAP Logs from Controlled Execution

💻 Bash/Python C2 Server Scripts

🔧 Capabilities
Shell command execution

System info gathering (CPU, memory, network)

Directory and file enumeration

File reading (/etc/passwd, etc.)

Shutdown/reboot commands (DoS)

🧠 Key Behaviors
Outbound reverse TCP connection (port 4444)

Plaintext C2 communication with retry beaconing every 5 seconds

Graceful termination via exit command

Persistent loop for continuous control

🧪 Dynamic Analysis Environment
Two Virtual Machines (VMs)

VM-1 (Victim): RAT host

VM-2 (Attacker): C2 server

Tools Used:

Wireshark (PCAP capture)

Netcat (nc) or custom C2 scripts

lsof, netstat, ps, top for process/network monitoring

🔍 Observations
Static Analysis:
Written in Rust (with debug symbols)

Linked with libc.so, optionally libssl.so

Network-related strings: connect, ConnectionRefused, etc.

Strings suggest outbound C2 communication attempts

Dynamic Analysis:
Successful reverse shell from victim to C2

Commands executed: whoami, cat /etc/passwd, etc.

Full response sent back over TCP

Session closed via exit command

⚠️ Limitations
Limitation	Suggested Fix
Unix-only shell usage	Add cross-platform support for Windows (e.g., cmd.exe)
No persistence	Use crontab/systemd or Windows Registry autorun
No encryption	Integrate rustls or native-tls
Static IP for C2	Use dynamic DNS or Tor
No obfuscation	Apply cargo-obfuscate, polymorphic techniques

🛡️ Detection & Defense
Host-Based:
Monitor for shell spawning from user directories

Use AppArmor/SELinux to restrict critical commands

Network-Based:
Block common reverse shell ports (4444, 1337)

Apply DPI to detect suspicious plain-text C2 traffic

Behavioral:
Alert on repeated TCP retries and unexpected shell commands

✅ Recommendations
Application Whitelisting

Endpoint Detection & Response (EDR)

User Awareness Training

Patch Management

MFA for sensitive access

Secure Backups

Use of Sandboxes for file testing

📈 Result
The RAT remained undetected by VirusTotal, showcasing how novel language usage (Rust) and lack of obfuscation can still bypass many static detection mechanisms. This emphasizes the importance of behavioral and heuristic analysis in malware defense.

