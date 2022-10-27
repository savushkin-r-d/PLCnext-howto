# How to logging #

## 1. **PLCnext** diagnostic log file ##

PLCnext messages are located here: *"/var/log/messages"* and *"/var/log/error"*. To view the file content use one of this command:

```sh
cat /var/log/messages
cat /var/log/error
```

To constantly monitor the file content use this:

```sh
tail -F /var/log/messages
```

![tail -F /opt/plcnext/logs/Output.log](images/tail_F.gif)

The parameter **-F** is important - it makes possible to see changes after file recreation (because of log rotation).

Next example makes it easier to catch error messages by using colors:

```sh
tail -F /var/log/messages /var/log/error | awk '
  /\/var\/log\/messages/ {print "\033[32m" $0 "\033[39m"; current_color="\033[32m"; next}
  /\/var\/log\/error/ {print "\033[31m" $0 "\033[39m"; current_color="\033[31m"; next}
  /WARN/ {print "\033[33m" $0 "\033[39m"; next}
  /DEBUG/ {print "\033[37m" $0 "\033[39m"; next}
  1 {print current_color $0 "\033[39m"}
  '
```

![colored tail -F](images/colored_tail_F.gif)

## 2. System diagnostic log file ##

System log file is located here: *"/var/log/messages"* and *"/var/log/error"*. You can view this files content to monitor system wide events.
If it is required to find some certain events (for example, **Arp.System**) - it is possible to use *awk*:

```sh
tail -F /var/log/messages /var/log/error | awk '
  /\/var\/log\/messages/ {print "\033[32m" $0 "\033[39m"; current_color="\033[32m"; next}
  /\/var\/log\/error/ {print "\033[31m" $0 "\033[39m"; current_color="\033[31m"; next}
  /WARN/ && /Arp.System/ {print "\033[33m" $0 "\033[39m"; next}
  /DEBUG/ && /Arp.System/ {print "\033[37m" $0 "\033[39m"; next}
  /Arp.System/ {print current_color $0 "\033[39m"}
  '
```

## 3. Using **syslog** ##

You can also use **syslog** and save messages to system diagnostic log file:

```cpp
#include <syslog.h>
//...
openlog ("my_prog", LOG_CONS | LOG_PID | LOG_NDELAY, LOG_USER);

syslog (LOG_NOTICE, "Program started by User %d", getuid ());
syslog (LOG_INFO, "Test info message.");

closelog ();
//...
```
