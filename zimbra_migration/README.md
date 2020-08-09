ZIMBRA MIGRATION STEPS:

https://syslint.com/blog/tutorial/zimbra-server-migration-and-zimbra-account-transfer-the-perfect-method/


1. Clone old zimbra (ADD EXTRA STORAGE IF IT NECESSARY)
2. Create a new machine with ubuntu 18.04 and install new zimbra
3. Change old zimbra network configuration (put zimbra to same network as new server)
4. SSH from new to old ( first create user into old one, add sudo privilege, and allow ssh. Allow root ssh. Also send ssh-key to a new one using second ip of a new)
5. Give the same hostname on both machines
6. Create migration dir and change permission
 - STOP ANTISPAM
 - CHANGE zmlocalconfig zmdisklog_critical_threshold TO 99@
 - Certs!!!
 - Forwarding mail will not be migrated
 - Mail will be duplicated if they use POP3!!!
 - Outlook calendar will be migrated but must be config from outlook (this is Ivelin part)
7. Export all inside
- REMOVE ALL DOMAINS AND SUBDOMAINS from admins.txt RELATED WITH THE MAIN HOSTNAME BECAUSE IT WAS ALREADY CREATED IN A NEW SERVER
- remove all the email accounts from the file /backups/zmigrate/emails.txt with starting words like spam, virus, ham, galsync 

8. Copy ssh-key from old to a new location:
9. Rsync
  rsync -avp -e 'ssh -p 22' /backups/zmigrate/ root@172.20.5.32:/backups/zmigrate
10. Extract all
11. Change IP addresses
12. Send test e-mail

Config DIskSPace warning mails from 10 minutes to 24 hours:
 TO CHECK:
zmlocalconfig zmstat_disk_interval
 TO CHANGE:
zmlocalconfig -e zmstat_disk_interval=86400
 TO APPLY IT:
zmcontrol restart

Install and conf fail2ban !!!
