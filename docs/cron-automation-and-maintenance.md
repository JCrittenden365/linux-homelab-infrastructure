
# Cron Automation and Maintenance

## Overview

Cron is used to automate routine system tasks in Linux.

In this lab environment cron is used to practice **scheduled system maintenance and automated logging**.

---

# What is Cron

Cron is a built-in Linux service that runs commands or scripts automatically at scheduled times.

Administrators commonly use cron for:

* backups
* log cleanup
* system monitoring
* maintenance scripts

---

# Cron Script Creation

A maintenance script was created to demonstrate automation and logging.

Example script location:

```
/usr/local/bin/system-maintenance.sh
```

The script records when it starts and finishes executing.

Example logging behavior:

```
maintenance started
maintenance completed
```

---

# Logging

The script writes information to a log file so activity can be reviewed later.

Example log file:

```
/var/log/cron-maintenance.log
```

This allows administrators to confirm that the scheduled task executed successfully.

---

# Error Logging

Error output is redirected to a separate file.

Example:

```
/var/log/cron-maintenance-error.log
```

Separating normal logs from error logs makes troubleshooting easier.

---

# Cron Scheduling

The script is executed automatically using a cron job.

Example schedule:

```
0 * * * * /usr/local/bin/system-maintenance.sh
```

This runs the script **once every hour**.

---

# Maintenance Tasks

Current tasks include:

* recording execution times
* testing log output
* verifying cron scheduling

Future maintenance tasks may include:

* automated log cleanup
* disk usage monitoring
* system health checks

---

# Purpose of This Lab

This exercise demonstrates how Linux administrators automate routine system tasks.

Automation improves reliability and reduces the need for manual maintenance on production systems.
