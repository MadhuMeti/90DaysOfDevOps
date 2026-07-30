- Process checks
-----------------------------------
-----------------------------------
~$ ps
    PID TTY          TIME CMD
    288 pts/0    00:00:00 bash
 249672 pts/0    00:00:00 ps
-----------------------------------
:~$ top
top - 08:52:25 up 2 days, 11:47,  1 user,  load average: 0.01, 0.22, 0.21
Tasks:  22 total,   1 running,  21 sleeping,   0 stopped,   0 zombie
%Cpu(s):  0.0 us,  0.2 sy,  0.0 ni, 99.7 id,  0.0 wa,  0.0 hi,  0.0 si,  0.0 st
MiB Mem :   7813.6 total,   6638.6 free,    901.2 used,    470.2 buff/cache
MiB Swap:   2048.0 total,   2048.0 free,      0.0 used.   6912.4 avail Mem

    PID USER      PR  NI    VIRT    RES    SHR S  %CPU  %MEM     TIME+ COMMAND
      1 root      20   0   22216  13708   9852 S   0.3   0.2   4:34.95 systemd
  66426 syslog    20   0  222516   6172   4460 S   0.3   0.1   0:14.91 rsyslogd
      2 root      20   0    3180   2144   2016 S   0.0   0.0   0:00.01 init-systemd(Ub
      7 root      20   0    3196   2124   2008 S   0.0   0.0   0:00.00 init
     59 root      19  -1   66968  16120  14772 S   0.0   0.2   7:10.79 systemd-journal
    107 root      20   0   25548   6928   5216 S   0.0   0.1   0:19.70 systemd-udevd
    156 systemd+  20   0   21344  13268  11144 S   0.0   0.2   0:03.62 systemd-resolve
    161 systemd+  20   0   91036   8044   7076 S   0.0   0.1   0:09.26 systemd-timesyn
    173 root      20   0    4244   2748   2496 S   0.0   0.0   0:00.16 cron
    174 message+  20   0    9788   5736   4780 S   0.0   0.1   0:45.38 dbus-daemon
-----------------------------------
- Service checks
-----------------------------------
-----------------------------------
:~$ systemctl status
● ACPLGGN-Lap-238
    State: running
    Units: 376 loaded (incl. loaded aliases)
     Jobs: 0 queued
   Failed: 0 units
    Since: Thu 2026-07-23 10:19:05 UTC; 3 days ago
  systemd: 255.4-1ubuntu8.16
-----------------------------------
~$ systemctl list-units
  UNIT                                                                                                       >
  sys-devices-LNXSYSTM:00-LNXSYBUS:00-ACPI0004:00-VMBUS:00-04cf8762\x2d6106\x2d4086\x2da9ca\x2dc06e91dfb42c-p>
  sys-devices-LNXSYSTM:00-LNXSYBUS:00-ACPI0004:00-VMBUS:00-04cf8762\x2d6106\x2d4086\x2da9ca\x2dc06e91dfb42c-p>
  sys-devices-LNXSYSTM:00-LNXSYBUS:00-ACPI0004:00-VMBUS:00-04cf8762\x2d6106\x2d4086\x2da9ca\x2dc06e91dfb42c-p>
-----------------------------------
- Log checks
-----------------------------------
-----------------------------------
~$ journalctl
Jul 27 08:55:31 ACPLGGN-Lap-238 systemd-resolved[156]: Clock change detected. Flushing caches.
Jul 27 08:55:31 ACPLGGN-Lap-238 systemd-journald[59]: Time jumped backwards, rotating. (Dropped 11 similar message(s))
Jul 27 08:55:32 ACPLGGN-Lap-238 systemd[1]: wsl-pro.service: Scheduled restart job, restart counter is at 19870.
Jul 27 08:55:32 ACPLGGN-Lap-238 systemd[1]: Starting wsl-pro.service - Bridge to Ubuntu Pro agent on Windows...
Jul 27 08:55:32 ACPLGGN-Lap-238 wsl-pro-service[251020]: INFO Starting WSL Pro Service version v0.1.4
-----------------------------------
