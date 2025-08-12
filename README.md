# Penetration-testing-portfil
My ethical hacking and penetration testing projects"
#!/usr/bin/env python3

import os
import sys
import subprocess
from datetime import datetime

if len(sys.argv) != 2:
    print(f"Usage: python3 {sys.argv[0]} <target>")
    sys.exit(1)

target = sys.argv[1]
timestamp = datetime.now().strftime("%Y%m%d-%H%M%S")

output_dir = f"scan_results_{timestamp}"
os.makedirs(output_dir, exist_ok=True)

print(f"[+] Target: {target}")
print(f"[+] Results will be saved in: {output_dir}\n")

# Step 1: Nmap scan
print("[*] Running Nmap scan...")
with open(os.path.join(output_dir, "nmap.txt"), "w") as f:
    subprocess.run(["nmap", "-sC", "-sV", "-p-", target], stdout=f)

# Step 2: Nikto scan
print("[*] Running Nikto scan...")
with open(os.path.join(output_dir, "nikto.txt"), "w") as f:
    subprocess.run(["nikto", "-h", target], stdout=f)

# Step 3: Dirb scan
print("[*] Running Dirb scan...")
with open(os.path.join(output_dir, "dirb.txt"), "w") as f:
    subprocess.run(["dirb", f"http://{target}"], stdout=f)

print("\n[+] All scans completed!")
print(f"[+] Check '{output_dir}' folder for results.")
