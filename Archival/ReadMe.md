# Machine Submission: Archival

## Machine Details
- **Name**: Archival
- **Difficulty**: Easy
- **OS**: Ubuntu 22.04 LTS
- **Hostname**: archival.htb
- **Author**: [USER] / Antigravity

## Credentials
| User | Password | Role |
| --- | --- | --- |
| root | - | Administrative |
| archivist | Archivist2026! | Service User / Lateral Pivot |
| www-data | - | Web Service User |

## Services
| Port | Service | Description |
| --- | --- | --- |
| 80/tcp | Apache/2.4 | Library Archive Portal (PHP/Tesseract) |
| 22/tcp | OpenSSH | SSH Access (for archivist) |

## Exploitation Summary

### 1. Foothold
The "Digital Archive Portal" allows users to upload images for OCR processing. The backend script `process.php` passes the filename directly to the `tesseract` binary via a shell command without sanitization. If the `debug=1` parameter is appended to the URL, the full command is revealed. Attackers can inject commands by naming uploaded files with special characters (e.g., `; sleep 5 ;.jpg`).

### 2. Lateral Movement
Enumeration of the web directory reveals a `.env` file containing clear-text credentials for the `archivist` user. This user has SSH access.

### 3. Privilege Escalation
The `archivist` user can run a custom backup script `/usr/local/bin/backup.sh` as root via `sudo`. This script performs a `tar` command with a wildcard (`*`) in a world-writable directory (`/home/archivist/backups`). This allows for a classic `tar` wildcard argument injection attack.

## Automation & Stability
- **Concurrency**: Each web upload is handled in a unique subdirectory (`uploads/session_...`) to ensure multiple players do not interfere with each other's files.
- **Cleanup**: A cron job running every 5 minutes clears the `uploads` and `backups` directories to prevent spoilers and ensure disk space.
- **Repeatability**: The vulnerabilities are logical and do not depend on volatile exploits that could crash the machine.
- **History**: Bash history is symlinked to `/dev/null` for privacy and to prevent spoilers.
