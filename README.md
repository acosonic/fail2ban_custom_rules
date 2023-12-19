# fail2ban custom rules
## A collection of custom rules for fail2ban

To use it, just merge filter.d with your existing filter.d rules
and append content of jail.conf with your existing jail.conf

***A littlebit of theory:***
Fail2ban is supposed to read log files (it can read log files of your custom software as well), 
and then when criteria matches like 2 failed login atempts within 10 minutes, it triggers some
action, it can be something simple like blocking that IP address for 1hr, or more complex and
custom, it depends upon your configuration.

One of things that fail2ban can also do is, send email to abuse contact, unfortunateley most 
of developers and admins don't actually know how internet works.
Each IP address is assigned by RIPE, an international internet controlling legal entity...
And each IP address has it's owner, which must have abuse email.
Usually those emails are monitored and actions are taken, because if they don't respond, and you
have log files of attempted hacking attempts, you can email abuse at RIPE, and they will block 
theri IP addresses...   

You can individually download (github raw) files and place it in your /etc/fail2ban 
appropriate folders.

Sample **jail.local** with enabled sshd, postfix-sasl, postfix and dovecot rules:

```
[sshd]
enabled = false

[postfix-sasl]
enabled  = true
port     = smtp,ssmtp,submission,imap2,imap3,imaps,pop3,pop3s
action   = iptables-multiport[name=postfix-sasl, port="smtp,ssmtp,465,submission,imap,imaps,pop3,pop3s"]
filter   = postfix-sasl
logpath  = /var/log/mail.log
maxretry = 2
findtime = 10800
bantime  = -1

[postfix]
enabled = true

[dovecot]
enabled = true
```

**note:** This rules can be heavy on your server's CPU, and if you
are lacking it, think of some other solution...

**note2:** theese rules should be constantly updated, and can be significantly improved,
feel free to work on them and request PR's ...


To confirm that script is working:
```
root@host:/etc/fail2ban# fail2ban-client status apache-script-hackbots
Status for the jail: apache-script-hackbots
|- Filter
|  |- Currently failed:	0
|  |- Total failed:	264
|  `- File list:	/var/log/virtualmin/example.com_access_log
`- Actions
   |- Currently banned:	9
   |- Total banned:	10
   `- Banned IP list:	209.95.51.11 109.70.100.20 134.175.26.138 178.17.170.196 14.63.75.46 78.148.23.203 185.222.202.12 120.27.133.197 185.220.101.12
```

TODO:
- create complain rule to send abuse reports to RIPE administrative contact
- integrate with various BAD IP lists
(please do above if you have time...)
