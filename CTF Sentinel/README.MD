# CTF Sentinel 🐉

**AI-Enhanced OSINT Tool for Kali Linux**

[![Python 3.10+](https://img.shields.io/badge/python-3.10+-blue.svg)](https://www.python.org/downloads/)
[![Kali Linux](https://img.shields.io/badge/Kali%20Linux-Optimized-blueviolet.svg)](https://www.kali.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

> 🎯 **Built for Kali Linux** - Leverages all pre-installed OSINT tools for maximum CTF power!

## 🎯 Overview

CTF Sentinel is a powerful, AI-enhanced OSINT tool designed specifically for CTF competitions on Kali Linux. It automates intelligence collection from external OSINT tools (most pre-installed on Kali!), applies AI/NLP for entity recognition, and intelligently correlates findings to uncover flags and hidden clues.

### Key Features

- **🚀 Speed**: Automated execution of multiple OSINT tools in parallel
- **🤖 AI-Powered**: Advanced NER using spaCy with custom CTF-specific patterns
- **🔗 Correlation**: Intelligent linking of disparate facts across sources
- **🎯 Flag Detection**: Custom patterns for CTF flags, API keys, and credentials
- **📊 Rich Reports**: Beautiful, color-coded terminal output using Rich
- **🔍 Multi-Target**: Supports domains, IPs, usernames, emails, hashes, and files
- **� Kali-Optimized**: Uses Kali's pre-installed tools (Nmap, Whois, dig, ExifTool)

## 🚀 Quick Installation

### One-Line Install (Recommended)

```bash
chmod +x kali-setup.sh && ./kali-setup.sh
```

This automated script will:

- Install all Python dependencies
- Download spaCy AI model
- Install external OSINT tools (Amass, Sherlock, etc.)
- Verify everything works
- Create bash alias (optional)

### Manual Installation

```bash
# 1. Update system
sudo apt update && sudo apt upgrade -y

# 2. Install Python dependencies
pip3 install -r requirements.txt
python3 -m spacy download en_core_web_sm

# 3. Install external OSINT tools
sudo apt install -y amass sublist3r nmap whois dnsutils libimage-exiftool-perl
pip3 install sherlock-project

# 4. Verify installation
python3 demo.py
```

## 🎯 Usage

### Basic Scans

```bash
# Domain reconnaissance
python3 main.py --target-type domain --value ctfchallenge.com

# Username OSINT  
python3 main.py --target-type alias --value hacker_ctf

# IP investigation (may need sudo for Nmap)
sudo python3 main.py --target-type ip --value 192.168.1.1

# Email analysis
python3 main.py --target-type email --value admin@target.com

# Hash lookup
python3 main.py --target-type hash --value 5d41402abc4b2a76b9719d911017c592

# File metadata extraction
python3 main.py --target-type filename --value /path/to/image.jpg
```

### Advanced Options

```bash
# Save results to JSON
python3 main.py --target-type domain --value target.com --output ~/results.json

# Verbose mode (see all tool output)
python3 main.py --target-type domain --value target.com --verbose

# Skip AI analysis (faster, less intelligent)
python3 main.py --target-type domain --value target.com --skip-ai
```

### Create Bash Alias

```bash
echo "alias ctf-sentinel='python3 $(pwd)/main.py'" >> ~/.bashrc
source ~/.bashrc

# Now use:
ctf-sentinel --target-type domain --value example.com
```

## 📊 Example Output

```
╔═══════════════════════════════════════════════════════════╗
║              🔍 CTF SENTINEL 🔍                           ║
║         AI-Enhanced OSINT for CTF Competitions            ║
╚═══════════════════════════════════════════════════════════╝

Target Type: DOMAIN
Target Value: ctfchallenge.com

═══ Phase 1: Data Collection ═══
  → Running Amass subdomain enumeration...
  → Querying DNS records...
  → Running WHOIS lookup...
✓ Collected 5 data sources

═══ Phase 2: AI/NER Analysis ═══
✓ Extracted 142 entities using AI/NER

═══ Phase 3: Correlation & Analysis ═══
✓ Identified 23 linked entities

═══ Phase 4: Intelligence Report ═══

🚩 HIGH-VALUE TARGETS (AI-DETECTED)
╔══════════════════════════════════╗
║ CTF Flags                        ║
╠══════════════════════════════════╣
║ CTF{found_in_subdomain}          ║
║ flag{hidden_in_js_code}          ║
╚══════════════════════════════════╝

🔑 API Keys & Tokens
╔══════════════════════════════════╗
║ AKIAIOSFODNN7EXAMPLE             ║
║ ghp_abc123def456...              ║
╚══════════════════════════════════╝
```

## 🎓 How It Works

### 1. Data Collection (collection_engine.py)

Executes Kali's OSINT tools based on target type:

- **Domains**: Amass/Sublist3r, DNS (dig), WHOIS
- **IPs**: Reverse DNS, WHOIS, Nmap port scan
- **Aliases**: Sherlock, GitHub API, Pastebin
- **Emails**: Domain analysis, GitHub commit search
- **Hashes**: Public database searches
- **Files**: ExifTool metadata extraction

### 2. AI/NLP Analysis (ai_parser.py)

Uses spaCy NER with custom patterns for:

- **CTF Flags**: `CTF{...}`, `flag{...}`, `FLAG{...}`
- **API Keys**: AWS keys, GitHub tokens, generic API keys
- **File Paths**: `/etc/passwd`, `~/.ssh/`, sensitive directories
- **Credentials**: username:password patterns
- **Standard Entities**: emails, IPs, URLs, hashes

### 3. Correlation (correlation_report.py)

Builds a knowledge graph:

- Links entities across multiple sources
- Identifies co-occurring entities
- Calculates importance scores
- Detects relationships

### 4. Reporting

Generates rich terminal output:

- Executive summary with statistics
- High-value targets (flags, keys, credentials) in red/bold
- Entity breakdown by type
- Relationship visualization
- JSON export capability

## 🔧 Customization

### Add Custom Flag Patterns

Edit `ai_parser.py`:

```python
def _setup_custom_patterns(self):
    custom_flag = [
        [{"TEXT": {"REGEX": r"MYCTF\{[^}]+\}"}}]
    ]
    self.matcher.add("CUSTOM_FLAG", custom_flag)
```

### Add New Target Types

Extend `collection_engine.py`:

```python
def collect_new_type(self, value: str, progress_callback=None):
    # Your collection logic
    return results
```

## � Docker Option

Run in a container:

```bash
# Build image
docker build -t ctf-sentinel .

# Run scan
docker run --rm ctf-sentinel --target-type domain --value example.com

# With output file
docker run --rm -v $(pwd)/output:/output ctf-sentinel \
  --target-type domain --value example.com --output /output/report.json
```

## 🧪 Testing

```bash
# Run all tests
pytest

# With coverage
pytest --cov=. --cov-report=html

# View coverage
firefox htmlcov/index.html
```

## 🔥 Advanced Kali Workflows

### Automated Recon Script

```bash
#!/bin/bash
TARGET=$1
OUTPUT_DIR="./recon_$(date +%Y%m%d_%H%M%S)"
mkdir -p $OUTPUT_DIR

echo "[*] Running CTF Sentinel"
python3 main.py --target-type domain --value $TARGET --output $OUTPUT_DIR/sentinel.json

echo "[*] Running Amass"
amass enum -d $TARGET -o $OUTPUT_DIR/amass.txt

echo "[*] Complete! Results in $OUTPUT_DIR"
```

### Batch Scanning

```bash
# Create targets.txt with one domain per line
for target in $(cat targets.txt); do
  python3 main.py --target-type domain --value $target \
    --output "results/${target}_$(date +%s).json"
done
```

### With VPN (OpensVPN)

```bash
# Start VPN
sudo openvpn ~/vpn/config.ovpn

# In another terminal
python3 main.py --target-type domain --value target.com
```

## 📚 Documentation

- **Installation Guide**: [`KALI_INSTALL.md`](KALI_INSTALL.md) - Detailed setup instructions
- **Usage Examples**: [`USAGE_EXAMPLES.md`](USAGE_EXAMPLES.md) - CTF-specific scenarios
- **Project Summary**: [`PROJECT_SUMMARY.md`](PROJECT_SUMMARY.md) - Complete overview
- **Configuration**: [`config.py`](config.py) - Customize settings

## 🏗️ Project Structure

```
ctf-sentinel/
├── main.py                    # CLI entry point
├── collection_engine.py       # External tool execution
├── ai_parser.py              # AI/NLP processing with spaCy
├── correlation_report.py     # Correlation & rich reporting
├── config.py                 # Configuration & constants
├── requirements.txt          # Python dependencies
├── kali-setup.sh            # Automated setup script
├── Dockerfile               # Container deployment
├── docker-compose.yml       # Docker orchestration
├── test_ai_parser.py        # AI/NER unit tests
├── test_correlation.py      # Correlation unit tests
├── demo.py                  # Installation verification
├── README.md                # This file
├── KALI_INSTALL.md          # Detailed installation guide
└── USAGE_EXAMPLES.md        # CTF usage scenarios
```

## 🛡️ Best Practices

### Use VPN for Anonymity

```bash
sudo openvpn ~/vpn/config.ovpn
```

### Rate Limiting

Be mindful of aggressive scans - use on authorized targets only.

### Save Everything

```bash
python3 main.py --target-type domain --value target.com \
  --output "scan_$(date +%Y%m%d_%H%M%S).json"
```

## 🐛 Troubleshooting

### "Permission denied" for Nmap

```bash
sudo python3 main.py --target-type ip --value 192.168.1.1
```

### "Module not found"

```bash
pip3 install -r requirements.txt
python3 -m spacy download en_core_web_sm
```

### "Tool not found" warnings

```bash
sudo apt install <tool-name>
# Or run kali-setup.sh again
```

### Virtual environment issues

```bash
python3 -m venv venv
source venv/bin/activate
pip3 install -r requirements.txt
```

## 📄 License

This project is licensed under the MIT License.

## ⚠️ Disclaimer

This tool is intended for **educational purposes and authorized security research only**. Always obtain proper authorization before conducting reconnaissance on systems you do not own

.

## 🙏 Acknowledgments

- OWASP Amass team
- Kali Linux project
- spaCy development team
- CTF community
- All OSINT tool creators

---

**🐉 Made for Kali Linux | Happy Hunting! 🔍**
