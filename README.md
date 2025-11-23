# Linux Administration & Automation Scripts 🐧

[![Shell Script](https://img.shields.io/badge/shell_script-%23121011.svg?style=flat&logo=gnu-bash&logoColor=white)]()
[![Python](https://img.shields.io/badge/python-3670A0?style=flat&logo=python&logoColor=ffdd54)]()
[![Linux](https://img.shields.io/badge/Linux-FCC624?style=flat&logo=linux&logoColor=black)]()

> Collection of Bash and Python scripts for automating Linux system administration tasks

## 📋 Table of Contents
- [Overview](#overview)
- [Scripts Included](#scripts-included)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Usage Examples](#usage-examples)
- [Script Details](#script-details)
- [Scheduling with Cron](#scheduling-with-cron)
- [What I Learned](#what-i-learned)
- [Best Practices](#best-practices)
- [Troubleshooting](#troubleshooting)

## 🎯 Overview

This repository contains practical system administration scripts that automate common Linux tasks. These scripts demonstrate:
- System monitoring and health checks
- Log management and rotation
- User account provisioning
- Backup automation
- Security auditing
- Performance monitoring

**Purpose:** Learn Linux administration fundamentals and automation scripting while building reusable tools for system management.

## 📦 Scripts Included

### System Monitoring
- `system_health_check.sh` - Comprehensive system health monitoring
- `disk_usage_monitor.sh` - Monitor disk space and alert on thresholds
- `service_monitor.sh` - Check if critical services are running
- `memory_monitor.py` - Track memory usage over time

### Log Management
- `log_rotation.sh` - Rotate and compress old log files
- `log_cleanup.sh` - Delete logs older than specified days
- `log_analyzer.py` - Parse and analyze system logs

### User Management
- `user_creation.sh` - Bulk create users from CSV file
- `password_expiry_check.sh` - Check and report password expiration
- `inactive_user_report.sh` - Find users who haven't logged in recently

### Backup & Recovery
- `backup_script.sh` - Automated backup with compression
- `database_backup.sh` - MySQL/PostgreSQL backup automation
- `config_backup.sh` - Backup important configuration files

### Security & Auditing
- `security_audit.sh` - Basic security checks and hardening
- `port_scanner.sh` - Check for open ports
- `failed_login_monitor.sh` - Monitor failed SSH login attempts

### System Maintenance
- `system_update.sh` - Automated package updates
- `cleanup_temp.sh` - Remove temporary files safely
- `service_restart.sh` - Graceful service restart with checks

## 🔧 Prerequisites

### System Requirements
```bash
# Tested on:
- Ubuntu 20.04 LTS / 22.04 LTS
- CentOS 7 / 8
- Debian 10 / 11

# Required packages
sudo apt update
sudo apt install -y \
  bash \
  coreutils \
  python3 \
  python3-pip \
  curl \
  wget
```

### Permissions
Most scripts require root or sudo access:
```bash
# Option 1: Run with sudo
sudo ./script_name.sh

# Option 2: Run as root
su -
./script_name.sh
```

## 💻 Installation

### Step 1: Clone Repository
```bash
git clone https://github.com/rahul-thangavel/Linux-bash-automation.git
cd Linux-bash-automation
```

### Step 2: Make Scripts Executable
```bash
# Make all scripts executable
chmod +x *.sh

# Or individually
chmod +x system_health_check.sh
```

### Step 3: Install Python Dependencies (if needed)
```bash
# For Python scripts
pip3 install -r requirements.txt
```

### Step 4: Configure Scripts (Optional)
```bash
# Copy example config and customize
cp config.example config.sh
nano config.sh

# Set your email for alerts, log paths, etc.
```

## 🚀 Usage Examples

### System Health Check
```bash
# Run comprehensive health check
sudo ./system_health_check.sh

# Output example:
# ========================================
# System Health Check Report
# Date: 2024-11-23 14:30:00
# ========================================
# 
# CPU Usage: 15%
# Memory Usage: 2.3GB / 8GB (28%)
# Disk Usage: 45GB / 100GB (45%)
# Load Average: 0.52, 0.48, 0.45
# 
# Services Status:
# ✓ nginx - Running
# ✓ mysql - Running
# ✓ ssh - Running
# 
# System Health: GOOD
```

### Disk Usage Monitor
```bash
# Monitor disk usage with 80% threshold
sudo ./disk_usage_monitor.sh 80

# Send email alert if threshold exceeded
sudo ./disk_usage_monitor.sh 80 --email admin@example.com
```

### Log Rotation
```bash
# Rotate logs older than 7 days
sudo ./log_rotation.sh /var/log/application 7

# With compression
sudo ./log_rotation.sh /var/log/application 7 --compress
```

### Bulk User Creation
```bash
# Create users from CSV file
# CSV format: username,full_name,department,shell
sudo ./user_creation.sh users.csv

# Example CSV:
# jdoe,John Doe,Engineering,/bin/bash
# jsmith,Jane Smith,Marketing,/bin/bash
```

### Automated Backup
```bash
# Backup directory with compression
sudo ./backup_script.sh /var/www/html /backup/web

# With retention (keep 7 days)
sudo ./backup_script.sh /var/www/html /backup/web --retention 7
```

## 📝 Script Details

### system_health_check.sh

**Purpose:** Comprehensive system health monitoring

**What it checks:**
- CPU usage and load average
- Memory utilization (RAM and swap)
- Disk space usage (all mounted filesystems)
- Critical services status
- Network connectivity
- System uptime

**Usage:**
```bash
# Basic usage
sudo ./system_health_check.sh

# Save report to file
sudo ./system_health_check.sh > health_report.txt

# Email report
sudo ./system_health_check.sh | mail -s "Health Report" admin@example.com
```

**Output format:**
- Plain text report
- Color-coded status (green/yellow/red)
- Timestamp and hostname

---

### disk_usage_monitor.sh

**Purpose:** Monitor disk space and alert when threshold exceeded

**Features:**
- Checks all mounted filesystems
- Customizable threshold percentage
- Email alerts
- Log file generation

**Usage:**
```bash
# Monitor with 80% threshold
sudo ./disk_usage_monitor.sh 80

# With email alert
sudo ./disk_usage_monitor.sh 80 admin@example.com

# Check specific mount point
sudo ./disk_usage_monitor.sh 80 admin@example.com /var
```

**Alert example:**
```
DISK SPACE ALERT!
Filesystem: /dev/sda1
Mount point: /
Usage: 85% (85GB used, 15GB free)
Threshold: 80%
Action required: Clean up old files or expand disk
```

---

### log_rotation.sh

**Purpose:** Rotate and compress old log files

**Features:**
- Age-based rotation
- Compression (gzip)
- Preserves file permissions
- Maintains log directory structure

**Usage:**
```bash
# Rotate logs older than 7 days
sudo ./log_rotation.sh /var/log/app 7

# With compression
sudo ./log_rotation.sh /var/log/app 7 --compress

# Keep only 30 days of compressed logs
sudo ./log_rotation.sh /var/log/app 7 --compress --keep 30
```

**What it does:**
1. Finds logs older than specified days
2. Compresses them with gzip
3. Renames with timestamp
4. Optionally deletes very old compressed logs

---

### user_creation.sh

**Purpose:** Bulk create Linux user accounts

**Features:**
- CSV input file support
- Automatic home directory creation
- Password generation
- Group assignment
- Shell configuration

**CSV Format:**
```csv
username,full_name,group,shell
jdoe,John Doe,developers,/bin/bash
jsmith,Jane Smith,marketing,/bin/bash
```

**Usage:**
```bash
# Create users from CSV
sudo ./user_creation.sh users.csv

# Generate password file
sudo ./user_creation.sh users.csv --passwords passwords.txt

# Force password change on first login
sudo ./user_creation.sh users.csv --force-change
```

**Output:**
```
Creating user: jdoe
✓ User jdoe created successfully
✓ Home directory: /home/jdoe
✓ Default password: Temp123!
✓ Added to group: developers

Creating user: jsmith
✓ User jsmith created successfully
...
```

---

### backup_script.sh

**Purpose:** Automated file and directory backups

**Features:**
- Full and incremental backups
- Compression (tar.gz)
- Retention policy
- Verification after backup
- Email notifications

**Usage:**
```bash
# Full backup
sudo ./backup_script.sh /var/www /backup/www

# With retention (keep 7 days)
sudo ./backup_script.sh /var/www /backup/www --retention 7

# Incremental backup
sudo ./backup_script.sh /var/www /backup/www --incremental

# Email notification on completion
sudo ./backup_script.sh /var/www /backup/www --email admin@example.com
```

**Backup naming:**
```
backup_www_2024-11-23_143000.tar.gz
backup_www_2024-11-24_143000.tar.gz
backup_www_2024-11-25_143000.tar.gz
```

## ⏰ Scheduling with Cron

### Setup Cron Jobs

```bash
# Edit crontab
crontab -e

# Daily health check at 2 AM
0 2 * * * /path/to/system_health_check.sh > /var/log/health_$(date +\%Y\%m\%d).log 2>&1

# Check disk usage every 6 hours
0 */6 * * * /path/to/disk_usage_monitor.sh 80 admin@example.com

# Rotate logs daily at midnight
0 0 * * * /path/to/log_rotation.sh /var/log/app 7 --compress

# Weekly backup every Sunday at 3 AM
0 3 * * 0 /path/to/backup_script.sh /var/www /backup/www --retention 7

# Monitor failed logins hourly
0 * * * * /path/to/failed_login_monitor.sh
```

### Cron Syntax Quick Reference
```
* * * * * command
│ │ │ │ │
│ │ │ │ └─── Day of week (0-7, Sunday = 0 or 7)
│ │ │ └──────── Month (1-12)
│ │ └───────────── Day of month (1-31)
│ └────────────────── Hour (0-23)
└─────────────────────── Minute (0-59)
```

## 🧠 What I Learned

### Bash Scripting Skills
- **Control Structures**: if/else, loops (for, while), case statements
- **Functions**: Reusable code blocks with parameters
- **Error Handling**: Exit codes, trap commands, error logging
- **Input Validation**: Checking arguments and user input
- **File Operations**: Reading, writing, permissions, existence checks

### System Administration
- **Process Management**: ps, top, systemctl, service commands
- **Disk Management**: df, du, mount, fdisk concepts
- **User Management**: useradd, usermod, passwd, group operations
- **Log Management**: Understanding /var/log, syslog, journalctl
- **Cron Jobs**: Scheduling automated tasks

### Best Practices Learned
- Always check if running as root when needed
- Log script execution with timestamps
- Use meaningful variable names
- Comment code for future maintenance
- Test scripts in safe environments first
- Handle edge cases and errors gracefully

### Troubleshooting Skills
- **Issue**: Script fails silently
  - **Solution**: Added error checking after each command with `set -e`
  
- **Issue**: Cron job doesn't run
  - **Solution**: Use absolute paths, check cron logs in /var/log/syslog

- **Issue**: Permission denied errors
  - **Solution**: Proper use of sudo, file permissions (chmod)

## ✅ Best Practices

### Script Development
```bash
# Use bash strict mode
set -euo pipefail

# Check if running as root
if [[ $EUID -ne 0 ]]; then
   echo "This script must be run as root"
   exit 1
fi

# Use meaningful variable names
LOG_DIR="/var/log/myapp"
RETENTION_DAYS=7
ALERT_EMAIL="admin@example.com"

# Function for logging
log() {
    echo "[$(date +'%Y-%m-%d %H:%M:%S')] $*" | tee -a "$LOG_FILE"
}

# Clean up on exit
trap cleanup EXIT
```

### Security Considerations
- Store sensitive data in separate config files
- Use proper file permissions (600 for configs with passwords)
- Don't hardcode passwords in scripts
- Validate and sanitize user input
- Use sudo instead of running entire script as root when possible

### Code Organization
- One script, one purpose
- Use functions for reusable code
- Document with comments
- Include usage/help messages
- Version your scripts with Git

## 🔧 Troubleshooting

### Common Issues

**Script won't execute:**
```bash
# Check permissions
ls -l script.sh

# Make executable
chmod +x script.sh

# Check shebang line
head -1 script.sh
# Should be: #!/bin/bash
```

**Permission denied:**
```bash
# Run with sudo
sudo ./script.sh

# Or change ownership
sudo chown root:root script.sh
```

**Command not found:**
```bash
# Install missing command
sudo apt install package-name

# Or check if in PATH
which command_name
```

**Cron job not working:**
```bash
# Check cron is running
sudo systemctl status cron

# View cron logs
sudo grep CRON /var/log/syslog

# Use absolute paths in crontab
/usr/local/bin/script.sh instead of script.sh
```

## 🚀 Future Improvements

- [ ] Add more comprehensive error handling
- [ ] Implement centralized logging
- [ ] Create web dashboard for monitoring
- [ ] Add Ansible playbooks for deployment
- [ ] Implement notification via Slack/Discord
- [ ] Add unit tests for scripts
- [ ] Create Docker containers for testing
- [ ] Add support for more Linux distributions

## 📚 Resources

- [Bash Guide for Beginners](https://tldp.org/LDP/Bash-Beginners-Guide/html/)
- [Advanced Bash-Scripting Guide](https://tldp.org/LDP/abs/html/)
- [Linux System Administration](https://www.linuxfoundation.org/)

## 🤝 Contributing

Improvements and new scripts welcome! Please:
- Follow existing code style
- Test scripts before submitting
- Document your changes
- Add usage examples

## 📄 License

This project is open source and available under the [MIT License](LICENSE).

## 📫 Contact

**Rahul Thangavel**
- 💼 LinkedIn: [linkedin.com/in/rahul-thangavel](https://linkedin.com/in/rahul-thangavel)
- 📧 Email: rahult30112002@gmail.com
- 🐙 GitHub: [@rahul-thangavel](https://github.com/rahul-thangavel)

---

⭐ **If these scripts helped you, please star this repo!**

## ⚠️ Disclaimer

These scripts are for educational purposes. Always test in a safe environment before using in production. The author is not responsible for any system issues or data loss.
