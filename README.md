# fail2ban custom rules
## A collection of custom rules for fail2ban

To use it, just merge filter.d with your existing filter.d rules
and append content of jail.conf with your existing jail.conf

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
