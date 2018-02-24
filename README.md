# shhirose.chrony

[![Github](https://img.shields.io/badge/github-shhirose%2Fansible--chrony-brightgreen.svg)](https://github.com/shhirose/ansible-chrony)
[![Ansible galaxy](https://img.shields.io/badge/ansible--galaxy-chrony-brightgreen.svg)](https://galaxy.ansible.com/shhirose/chrony/)
[![Build Status](https://travis-ci.org/shhirose/ansible-chrony.svg?branch=master)](https://travis-ci.org/shhirose/ansible-chrony)
[![MIT License](http://img.shields.io/badge/license-MIT-blue.svg?style=flat)](LICENSE)

This is Ansible role for chrony install and setting for RedHat Enterprise Linux.

## Requirements

None

## Role Variables

```
shhirose_chrony_servers:
  - type: server
    name: time1.google.com
    options: iburst
  - type: server
    name: time2.google.com
    options: iburst
  - type: server
    name: time3.google.com
    options: iburst
# shhirose_chrony_initstepslew_threshold: 30
# shhirose_chrony_initstepslew_hosts:
#   - foo.example.net
shhirose_chrony_refclock: []
  # - driver: PPS
  #   options: '/dev/pps0 lock NMEA refid GPS'
# shhirose_chrony_dumpdir: /var/run/chrony
shhirose_chrony_manual: no
shhirose_chrony_stratumweight: 0
shhirose_chrony_driftfile: /var/lib/chrony/drift
shhirose_chrony_RTC: rtcsync
shhirose_chrony_makestep_threshold: 1.0
shhirose_chrony_makestep_limit: 3
# shhirose_chrony_hwtimestamp_interface: '*'
# shhirose_chrony_hwtimestamp_interface_params: ''
# shhirose_chrony_minsources: 2
shhirose_chrony_port: 123
# shhirose_chrony_bindaddress: 1.2.3.4
shhirose_chrony_client_access: []
  # - type: allow
  #   subnet: 1.2.3.4
shhirose_chrony_cmdport: 323
shhirose_chrony_cmdallow: []
  # - 127.0.0.1
  # - ::1
shhirose_chrony_cmddeny: []
  # - 1.2.3.4
shhirose_chrony_bindcmdaddress: []
  # - 127.0.0.1
  # - ::1
# shhirose_chrony_local_option: stratum
# shhirose_chrony_local_option_params: '10'
# shhirose_chrony_keyfile: /etc/chrony.keys
shhirose_chrony_noclientlog: yes
shhirose_chrony_logchange: 0.5
shhirose_chrony_logdir: /var/log/chrony
# shhirose_chrony_log: measurements statistics tracking
shhirose_chrony_extra_params: []
shhirose_chrony_logrotate_missingok: yes
shhirose_chrony_logrotate_nocreate: yes
shhirose_chrony_logrotate_sharedscripts: |
  postrotate
    /usr/libexec/chrony-helper command cyclelogs > /dev/null 2>&1 || true
shhirose_chrony_logrotate_extra_params: []
  # - monthly
  # - rotate 7
shhirose_chrony_similar_services:
  - ntpd
```

## Variable parameters

### shhirose_chrony

| key | required | default | type | values | notes |
| --- | --- | --- | --- | --- | --- |
| servers | no |  | array |  |  |
| servers[].type | no |  | string | server, pool or peer | This corresponds to the server, pool, and peer directive of Chrony. <br />[server directive](https://chrony.tuxfamily.org/doc/3.2/chrony.conf.html#server)<br />[pool directive](https://chrony.tuxfamily.org/doc/3.2/chrony.conf.html#pool)<br />[peer directive](https://chrony.tuxfamily.org/doc/3.2/chrony.conf.html#peer) |
| servers[].name | no |  | string |  | This corresponds to hostname argument of the server, pool, and peer directive. |
| servers[].options | no |  | string |  | This corresponds to option  argumentof the server, pool, and peer directive. |
| initstepslew_threshold | no | 30 | int |  | This corresponds to the initstepslew directive of Chrony. [initstepslew directive](https://chrony.tuxfamily.org/doc/3.2/chrony.conf.html#initstepslew) |
| initstepslew_hosts | no |  | array |  | This corresponds to the initstepslew directive of Chrony. [initstepslew directive](https://chrony.tuxfamily.org/doc/3.2/chrony.conf.html#initstepslew) |
| refclock | no |  | array |  | This corresponds to the refclock directive of Chrony. [refclock directive](https://chrony.tuxfamily.org/doc/3.2/chrony.conf.html#refclock) |
| refclock[].driver | no |  | string | PPS, SHM, SOCK, and PHC | This corresponds to driver argument of the refclock directive. |
| refclock[].options | no |  | string |  | This corresponds to parameter and option argument of the refclock directive. |
| dumpdir | no | /var/run/chrony | string |  | This corresponds to the dumpdir directive of Chrony. [dumpdir directive](https://chrony.tuxfamily.org/doc/3.2/chrony.conf.html#dumpdir) |
| manual | no | no | boolean |  | This corresponds to the manual directive of Chrony. [manual directive](https://chrony.tuxfamily.org/doc/3.2/chrony.conf.html#manual) |
| stratumweight | no | 0 | int |  | This corresponds to the stratumweight directive of Chrony. [stratumweight directive](https://chrony.tuxfamily.org/doc/3.2/chrony.conf.html#stratumweight) |
| driftfile | no | /var/lib/chrony/drift | string |  | This corresponds to the driftfile directive of Chrony. [driftfile directive](https://chrony.tuxfamily.org/doc/3.2/chrony.conf.html#driftfile) |
| RTC | no | rtcsync | string | hwclockfile, rtcautotrim, rtcdevice, rtcfile, rtcountc, and rtcsync | This corresponds to the Real-time clock (RTC) of Chrony. [Real-time clock (RTC)](https://chrony.tuxfamily.org/doc/3.2/chrony.conf.html#_real_time_clock_rtc)  |
| makestep_threshold | no | 1.0 | double |  | This corresponds to threshold argument of the makestep directive of Chrony. [makestep directive](https://chrony.tuxfamily.org/doc/3.2/chrony.conf.html#makestep) |
| makestep_limit | no | 3 | int |  | This corresponds to limit argument of the makestep directive of Chrony. [makestep directive](https://chrony.tuxfamily.org/doc/3.2/chrony.conf.html#makestep) |
| hwtimestamp_interface | no |  |  |  | This corresponds to interface argument of the hwtimestamp directive of Chrony. [hwtimestamp directive](https://chrony.tuxfamily.org/doc/3.2/chrony.conf.html#hwtimestamp) |
| hwtimestamp_interface_params | no |  |  |  | This corresponds to interface paramter argument of the hwtimestamp directive of Chrony. [hwtimestamp directive](https://chrony.tuxfamily.org/doc/3.2/chrony.conf.html#hwtimestamp) |
| minsources | no |  |  |  | This corresponds to the minsources directive of Chrony. [minsources directive](https://chrony.tuxfamily.org/doc/3.2/chrony.conf.html#minsources) |
| port | no | 123 | int |  | This corresponds to the port directive of Chrony. [port directive](https://chrony.tuxfamily.org/doc/3.2/chrony.conf.html#port) |
| bindaddress | no |  | string |  | This corresponds to the bindaddress directive of Chrony. [bindaddress directive](https://chrony.tuxfamily.org/doc/3.2/chrony.conf.html#bindaddress) |
| client_access | no |  | array |  |  |
| client_access[].type | no |  | string | allow or deny | This corresponds to the allow and deny directive of Chrony.<br />[allow directive](https://chrony.tuxfamily.org/doc/3.2/chrony.conf.html#allow)<br />[deny directive](https://chrony.tuxfamily.org/doc/3.2/chrony.conf.html#deny) |
| client_access[].subnet | no |  | string |  | This corresponds to all and subnet argument of the allow and deny directive. |
| cmdport | no | 323 | int |  | This corresponds to the cmdport directive of Chrony. [cmdport directive](https://chrony.tuxfamily.org/doc/3.2/chrony.conf.html#cmdport) |
| cmdallow | no |  | array |  | This corresponds to the cmdallow directive of Chrony. [cmdallow directive](https://chrony.tuxfamily.org/doc/3.2/chrony.conf.html#cmdallow) |
| cmddeny | no |  | array |  | This corresponds to the cmddeny directive of Chrony. [cmddeny directive](https://chrony.tuxfamily.org/doc/3.2/chrony.conf.html#cmddeny) |
| bindcmdaddress | no |  | array |  | This corresponds to the bindcmdaddress directive of Chrony. [bindcmdaddress directive](https://chrony.tuxfamily.org/doc/3.2/chrony.conf.html#bindcmdaddress)  |
| local_option | no |  | string | stratum, distance, and orphan | This corresponds to stratum and distance of the local directive of Chrony. [local directive](https://chrony.tuxfamily.org/doc/3.2/chrony.conf.html#local) |
| keyfile | no | /etc/chrony.keys | string |  | This corresponds to the keyfile directive of Chrony. [keyfile directive](https://chrony.tuxfamily.org/doc/3.2/chrony.conf.html#keyfile) |
| noclientlog | no | yes | boolean |  | This corresponds to the noclientlog directive of Chrony. [noclientlog directive](https://chrony.tuxfamily.org/doc/3.2/chrony.conf.html#noclientlog) |
| logchange | no | 0.5 | double |  | This corresponds to the logchange directive of Chrony. [logchange directive](https://chrony.tuxfamily.org/doc/3.2/chrony.conf.html#logchange) |
| logdir | no | /var/log/chrony | string |  | This corresponds to the logdir directive of Chrony. [logdir directive](https://chrony.tuxfamily.org/doc/3.2/chrony.conf.html#logdir) |
| log | no |  | string |  | This corresponds to the log directive of Chrony. [logdir directive](https://chrony.tuxfamily.org/doc/3.2/chrony.conf.html#log) |
| extra_params | no |  | array |  | This is an array of extra directive of Chrony. |
| logrotate_missingok | no | yes | boolean |  | If yes, enable missingok of logroated. |
| logrotate_nocreate | no | yes | boolean |  | If yes, enable nocreate of logroated. |
| logrotate_sharedscripts | no |  | string |  | Do update to sharedscripts content. |
| logrotate_extra_params | no |  | array |  | This is an array of extra parameters of logrotate. |
| similar_services | no |  | array |  | This is an array for stopping services similar to Chrony. |

## Dependencies

None

## Example Playbook

```
- hosts: servers
  become: yes
  roles:
    - shhirose.chrony
  vars:
    shhirose_chrony_servers:
      - type: server
        name: time1.google.com
        options: iburst
      - type: server
        name: time2.google.com
        options: iburst
    shhirose_chrony_logrotate_extra_params:
      - rotate 7
```

## License

MIT
