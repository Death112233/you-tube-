# 🔍 Ultimate Subdomain Enumeration Toolkit
# Complete subdomain reconnaissance workflow for bug bounty and penetration testing.

## 📦 Tools Used
- **Passive**: Subfinder, Amass, Findomain, AssetFinder, crt.sh, GitHub Subdomains
- **Brute Force**: GoBuster, FFuf, Feroxbuster

## 🚀 Installation
```bash
# Install main tools
go install -v github.com/projectdiscovery/subfinder/v2/cmd/subfinder@latest
go install -v github.com/OWASP/Amass/v3/...@master
go install -v github.com/projectdiscovery/assetfinder@latest
```

---

## 💻 COMMANDS

### 🔹 Passive Enumeration
```bash
# Subfinder
subfinder -d target.com -silent -all -recursive -o subfinder_subs.txt

# Amass Passive
amass enum -passive -d target.com -o amass_passive_subs.txt

# crt.sh Certificates
curl -s "https://crt.sh/?q=%25.target.com&output=json" | jq -r '.[].name_value' | sed 's/\*\.//g' | anew crtsh_subs.txt

# GitHub Subdomains
github-subdomains -d target.com -t YOUR_GITHUB_TOKEN -o github_subs.txt

# AssetFinder
assetfinder --subs-only target.com > assetfinder.txt

# Findomain
findomain -t target.com | tee findomain_subs.txt

# Amass Alternative
amass enum -passive -d target.com | cut -d']' -f 2 | awk '{print $1}' | sort -u > amass_subs.txt

# RapidDNS
curl -s "https://rapiddns.io/subdomain/target.com?full=1" \
| grep -Eo '[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}' \
| sort -u | awk -F. '{if (NF>2) print $0}' > rapiddns_subs.txt
```

### 🔹 Brute Force Attacks
```bash
# GoBuster DNS
gobuster dns --domain target.com -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt -t 50 -o gobuster-dns.txt

# Feroxbuster
feroxbuster -u https://found.target.com -w /usr/share/wordlists/dirb/common.txt -x php,html,txt -o ferox.json

# FFuf VHost Fuzzing
ffuf -u "https://FUZZ.target.com" -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt -mc 200,301,302 -o subdomains.json
```

### 🔹 Combine Results
```bash
cat *.txt | sort -u > all_subdomains.txt
```

---

## ⚠️ Disclaimer
For educational and authorized testing only. Always get proper permission before scanning.

---

**📝 Note:** Replace `target.com` with your target domain and `YOUR_GITHUB_TOKEN` with actual token.

---
# subscribe youtube channel 
https://youtu.be/FxwGwx9WgG4?si=vcteaVRfEUqOU9Oz
