# OHSNAP-Documentation

Internal documentation for the OHSNAP project.

https://www.noisebridge.net/wiki/OHSNAP

## General research

### PF reading

- https://www.openbsd.org/faq/pf/
- https://home.nuug.no/~peter/pftutorial/#1
- https://www.tumfatig.net/2019/protect-the-esxi-virtual-machines-with-openbsd/
  - mentions relayd to publish LAN services to Internet, ntpd etc
- https://nostarch.com/pf3
  - https://nostarch.com/download/pf3_ch3.pdf

### VPN

- Wireguard
  - https://www.tumfatig.net/2020/a-mesh-vpn-using-openbsd-and-wireguard/
- OpenVPN
- [tinc](https://www.tinc-vpn.org/)
- Use built-in IKEv2 ?

### Observability

- Need a security scanner for package vulnerabilities?
- [ntopng](https://www.ntop.org/products/traffic-analysis/ntop/)
  - See https://github.com/ntop/ntopng/blob/dev/doc/README.OpenBSD
- [ndpi](https://www.ntop.org/products/deep-packet-inspection/ndpi/) for deep
  packet inspection and Silk?
- tripwire
- snort
- [fwsnort](http://cipherdyne.org/fwsnort/) (IPTables, does it have a BSD/pf?)
- some
  [phishing filter](https://gitlab.com/curben/phishing-filter#phishing-url-blocklist)
  rules (see also uBlock Origin rules?):
- Suricata
- pflog graphing?
  - [PF logging](https://www.openbsd.org/faq/pf/logging.html)
  - https://prefetch.net/articles/monitoringpf.html
  - [pfstat](https://www.benzedrine.ch/pfstat.html)
- opentelemetry.io?
- rootkit detection
- [RITA](https://www.activecountermeasures.com/free-tools/rita/) Active
  Countermeasures
  - this can detect DNS tunneling?
- [OpenWIPS-ng](http://www.openwips-ng.org/) - Deprecated, but can we build on
  this interesting idea for wireless IPS?
- kibana/splunk for alerting admin machines
- file/system integrity
  - tripwire
  - [accton](https://man.openbsd.org/accton.8)
  - [acct](https://man.openbsd.org/acct.2)
- [FlowBAT](http://www.flowbat.com/)
- netflows
  - https://prefetch.net/articles/monitoringpf.html
  - https://en.wikipedia.org/wiki/SFlow
  - https://en.wikipedia.org/wiki/NetFlow
  - https://support.solarwinds.com/SuccessCenter/s/article/J-Flow-and-sFlow-configuration-examples-for-Juniper-devices?language=en_US
- SNMP
- syslog
- [SiLK](https://tools.netsa.cert.org/silk/)
- https://www.ntop.org/products/netflow/nprobe/
- [ttyd](https://tsl0922.github.io/ttyd/) - bundled in OpenWRT
- grafana
  - https://www.tumfatig.net/2018/monitoring-unbound8-using-net-snmp-telegraf-influxdb-and-elasticsearch/
- https://www.tumfatig.net/2011/running-monit-v5-on-openbsd/
  - lightweight, can restart processes
  - https://mmonit.com/monit/

### Messaging/communication

- https://github.com/victronenergy/dbus-mqtt
- Other MQTT
  - https://medium.com/@shantanoodesai/live-iot-data-subscription-with-apollo-graphql-and-mqtt-60b7c5a86cde
- Matrix (self-hosted)
  - https://matrix.org/docs/guides/installing-synapse
  - Also, self-hosted map tiling for location sharing, etc
    (https://matrix.org/docs/guides/map-tile-server)
- https://www.tumfatig.net/2020/status-page-using-collectd-influxdb-and-grafana/
  (has examples for sending emails and SMS alerts)
- https://github.com/maqp/tfc (tinfoil chat)
  - Needs to go through Tor, so might not be good for messaging, but
    architecture is of interest
- https://www.dnsstuff.com/free-siem-tools
  - [Wuzah](https://documentation.wazuh.com/current/quickstart.html)
    (on-premise, but 4CPU, 8G RAM, 50G storage)
  - https://mozdef.readthedocs.io/en/latest/overview.html
  - https://metron.apache.org/
- https://luca.ntop.org/n2n.pdf - "a novel layer-two over layer-three P2P
  virtual private network (VPN)"
- XMPP?
  - https://xmpp.org/uses/internet-of-things/
  - https://www.xmpp-iot.org/basics/being-friends/
  - https://www.xmpp-iot.org/basics/
  - https://stackoverflow.com/questions/38838199/how-to-implement-end-to-end-encryption-using-xmpp-configured-to-archive-the-mess
- https://stackoverflow.com/questions/62394557/python-lan-messenger-notification

### Services

- DNSSec using unbound with SSL or dnscrypt
- Also look at uBlock Origin lists
- SSH only public key auth, no root, not WAN interface
- Enhance pf config (create ncurses menus?)
  - https://tldp.org/HOWTO/NCURSES-Programming-HOWTO/intro.html
  - https://man.openbsd.org/ncurses
- web admin?
- Squid to control site access?
  - https://www.udemy.com/course/squid-proxy-server/
- Bitwarden password manger
  - https://www.tumfatig.net/2020/from-1password-on-icloud-to-bitwarden-on-openbsd/
- Support Tor and I2P?

### Content filtering

- https://www.ntop.org/products/traffic-analysis/ntopng-edge/
- https://www.sunnyvalley.io/sensei
- https://www.tumfatig.net/2019/blocking-ads-using-unbound8-on-openbsd/
  - https://www.tumfatig.net/2019/storing-unbound8-logs-into-influxdb/

### Existing solutions

- https://calomel.org/pfstat.html
  - https://calomel.org/rrdtool.html
- https://github.com/sonertari/PFFW (PHP-based, actively maintained)
- https://github.com/ntop/ntopng/blob/dev/doc/README.OpenBSD
- https://github.com/nahun/pfweb
  - Seems not maintained, but using
    [py-pf](http://www.kernel-panic.it/software/py-pf/) under the hood. Might be
    some useful code/ideas there!
  - NOTE: the warning about web app having access to pf which gives kernel
    access.Maybe the web app can just be for reading and any config needs to be
    done using ncurses on CLI. Or, do some cool CLI graphing and only allow CLI
    access. What about ttyd above?
- https://openwisp.org/whatis.html
- Other OS
  - [Pi-Hole](https://pi-hole.net/)
  - https://opnsense.org/
  - http://nfsen.sourceforge.net/
  - IPFire
  - Smoothwall
  - SecurityOnion
  - Endian Firewall
  - https://www.untangle.com/untangle-ng-firewall/
  - https://www.securepoint.de/produkte/utm-firewalls/black-dwarf-firewall/
  - https://duckduckgo.com/?sites=distrowatch.com&k7=%23fdffe3&k1=-1&q=firewall&sa=Go

### Misc reading

- http://roscidus.com/blog/blog/2016/01/01/a-unikernel-firewall-for-qubesos/
- https://www.freebsd.org/cgi/man.cgi?apropos=0&manpath=NetBSD%206.0&query=rump&sektion=3
