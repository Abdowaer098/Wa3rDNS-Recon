# wa3rdns 🌐

**wa3rdns** is an advanced and highly concurrent reconnaissance tool designed for deep DNS, network, and ASN enumeration. It automates the process of gathering intelligence on a target domain by consolidating information from various sources into a structured output directory.

-----

## ✨ Features

  - **Comprehensive DNS Recon:** Uses `dnsrecon`, `dig`, `host`, and `nslookup` for a wide range of DNS record lookups.
  - **Subdomain Brute-forcing:** Quickly checks a built-in list of common subdomains.
  - **SSL/TLS Certificate Analysis:** Extracts Subject Alternative Names (SANs) from SSL certificates to discover related domains.
  - **ASN & CIDR Enumeration:** Fetches ASN information for discovered IPs and collects all associated CIDR ranges.
  - **Reverse DNS Scanning:** Performs reverse DNS lookups on individual IPs or entire CIDR ranges.
  - **High-Speed Port Scanning:** Utilizes `masscan` for fast TCP port scanning on IPv4 and `nmap` for IPv6.
  - **Highly Concurrent:** Leverages threading to perform multiple lookups and scans in parallel for maximum speed.
  - **Structured Output:** Saves all findings in a timestamped directory with clearly labeled JSON and text files.

-----

## 🔧 Requirements

Before you can run `wa3rdns`, you must install the required command-line tools and Python libraries.

### Command-Line Tools

The script depends on several external tools. You can install them using your distribution's package manager.

**For Debian / Ubuntu:**

```bash
sudo apt update && sudo apt install -y dnsrecon dnsutils masscan nmap whois curl openssl
```

**For Fedora / CentOS / RHEL:**

```bash
sudo dnf install -y dnsrecon bind-utils masscan nmap whois curl openssl
```

**For Arch Linux:**

```bash
sudo pacman -Syu --noconfirm dnsrecon dnsutils masscan nmap whois curl openssl
```

### Python Libraries

The script requires one external Python library.

```
colorama
```

-----

## 🚀 Installation

Follow these steps to install and configure `wa3rdns` for easy use from anywhere in your terminal.

**1. Clone the Repository**

```bash
git clone https://github.com/your-username/wa3rdns.git
cd wa3rdns
```

**2. Install Python Dependencies**

```bash
pip3 install -r requirements.txt
```

**3. Make the Script Executable**

```bash
chmod +x wa3rdns.py
```

**4. Move to `/usr/local/bin`**

Move the script to a directory in your system's `PATH` to make it runnable as a global command. We'll also rename it to `wa3rdns` for convenience.

```bash
sudo mv wa3rdns.py /usr/local/bin/wa3rdns
```

You can now run the tool from any directory by simply typing `wa3rdns`.

-----

## 💻 Usage

The tool is straightforward to use. Point it at a target domain and select the desired actions using flags.

**Show the help menu:**

```bash
wa3rdns -h
```

### Examples

**Basic Reconnaissance (DNS, SSL, ASN):**

```bash
wa3rdns example.com
```

**Perform Reverse DNS Lookup on Discovered IPs:**

```bash
wa3rdns example.com --rev-dns
```

**Run a Port Scan on the Top 1000 Ports:**
*Note: Requires sudo privileges.*

```bash
sudo wa3rdns example.com --scan-ports
```

**Run a Full Port Scan (All 65535 Ports):**

```bash
sudo wa3rdns example.com --scan-ports --full-scan
```

**Scan All Discovered CIDR Ranges:**
This will first find all ASNs, collect their associated CIDR ranges, and then perform a reverse DNS lookup on every IP in those ranges. **Warning: This can be very time-consuming.**

```bash
wa3rdns example.com --scan-cidrs all
```

**Scan a Specific CIDR Range:**

```bash
wa3rdns example.com --scan-cidrs "192.0.2.0/24"
```

-----

## 📝 Output

All results are saved in a uniquely named directory, for example: `recon_results_example.com_20250722_040114/`. Inside you will find:

  - `ips.txt`: A clean list of all unique IP addresses found.
  - `asn_info.json`: ASN details for each IP.
  - `asn_cidrs.txt`: All CIDR ranges associated with the discovered ASNs.
  - `ssl_cert_domains.txt`: Domains found in the SSL certificate.
  - `reverse_dns.json`: Results from the reverse DNS lookup.
  - `masscan_open_ports.grep`: Greppable output from `masscan`.
  - `nmap_*.txt`: Output from `nmap` for each IPv6 address.
  - `reverse_dns_CIDR_HERE.json`: Reverse DNS results for scanned CIDR ranges.
