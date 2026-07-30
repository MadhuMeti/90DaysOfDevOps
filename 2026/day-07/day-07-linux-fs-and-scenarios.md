**Core Directories (Must Know):**
- `/` (root) - The starting point of everything
- `/home` - User home directories
- `/root` - Root user's home directory
- `/etc` - Configuration files
- `/var/log` - Log files (very important for DevOps!)
- `/tmp` - Temporary files

**Additional Directories (Good to Know):**  
- `/bin` - Essential command binaries
- `/usr/bin` - User command binaries
- `/opt` - Optional/third-party applications

**the largest log file in /var/log**
~$   du -sh /var/log/* 2>/dev/null | sort -h | tail -5
252K    /var/log/syslog.4.gz
260K    /var/log/syslog.2.gz
29M     /var/log/syslog
124M    /var/log/syslog.1
366M    /var/log/journal


**list all services**
systemctl list-units --type=service

**Check service status** 
~$ systemctl status cron
● cron.service - Regular background program processing daemon
     Loaded: loaded (/usr/lib/systemd/system/cron.service; enabled; preset: enabled)
     Active: active (running) since Tue 2026-07-28 05:33:41 UTC; 6h ago
       Docs: man:cron(8)
   Main PID: 197 (cron)
      Tasks: 1 (limit: 9363)
     Memory: 2.5M (peak: 4.8M)
        CPU: 319ms
     CGroup: /system.slice/cron.service
             └─197 /usr/sbin/cron -f -P


**Check if service is enabled on boot** 
```bash
systemctl is-enabled nginx

