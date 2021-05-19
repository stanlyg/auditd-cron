# Primary Use
Contains a script to use when configuring auditd to use cron for rotating logs

Based on https://access.redhat.com/solutions/661603, and modified to work according to the requirements given to me.

For simple use, place the file cron.daily-auditd in /etc/cron.daily. 

Update the /etc/audit/auditd.conf file with max_log_file_action = ignore. (If you don't do this, then you'll end up with multiple daily files. Which is fine, if that's what you want.)

```
sed -i 's/max_log_file_action = ignore/max_log_file_action = ignore/' /etc/audit/auditd.conf
```
# Alternate Uses

You can also place the cron.daily-auditd file in another location, probably with a different name, and call it with cron, or manually, or however needed.

Old files are renamed according to their timestamp, and then compressed with gzip. The logic handles existing /var/log/audit/audit.log.N files by renaming and compressing them.

