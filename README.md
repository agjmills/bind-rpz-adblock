# DNS-Level Ad-Blocking on LAN with BIND RPZ
BIND allows you to change the responses it serves for DNS queries, called Response Policy Zones (RPZ)

Utilising Steven Black's curated list of adware and malware domains, https://raw.githubusercontent.com/StevenBlack/hosts/master/hosts, we can generate a BIND-compatible zonefile, and therefore block adverts and malware at the DNS level. No browser extensions required.

Generate the zonefile:

```
python3 generate_blocklist.py > /etc/bind/zones/rpz-adblock.db
```

Modify named.conf:

```
options {
 // ...
 response-policy {
  zone "rpz-adblock";
 };
};

zone "rpz-adblock" {
 type master;
 file "/etc/bind/zones/rpz-adblock.db"
};
```

Restart BIND and you have an ad-free experienece.
