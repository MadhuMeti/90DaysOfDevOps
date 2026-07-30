**Commands**
ps - report a snapshot of the current processes.
top - display Linux tasks
free - Display amount of free and used memory in the system
pgrep, pkill - look up or signal processes based on name and other
df -h : disk size
free -h : RAM storage
tail -f file.txt: prints the last 5 lines of a file currently being updated. (ex:log file)

**Process Types**
*User Process*: Initiated and run in user space. No special previleges to the processor.
*Deamon Process*: Background application runs a service. Starts at system boot and ends at shutdown. Managed by root user. Advised to run as user scoped to be pretected against attacks.
*Kernel Process*: Runs in kernel space. Similar to deamon processes.

*Kernel Vs Deamon Process*
- Full access to system kernel making it more powerful - Limited access
- Less flexible (Cannot chnage behaviour without recompiling the kernel) - Can change behaviour by chnaging the config files and reloading the service



