# IVRE Tests #

This repository contains sample files and binaries used for
[IVRE](https://ivre.rocks/) tests.

## Samples ##

They are not supposed to be somehow realistic but rather to help test
most of IVRE features.

The files in this repository have been created by IVRE's
contributors, except:

- Some of the files in this repository come from the
  [Wireshark wiki](https://wiki.wireshark.org/):

  - `dns.pcap`
  - `imap.pcap`
  - `http.pcap`
  - `telnet-raw.pcap`
  - `nb6-startup.pcap`
  - `nb6-http.pcap`
  - `nb6-telephone.pcap`
  - `nb6-hotspot.pcap`
  - `Teredo.pcap`
  - `sr-header.pcap`

- The file `SSHv2.pcap` comes from [Packetlife](http://packetlife.net/media/captures/).

- The file `gre-sample.pcap` comes from [Cloudshark](https://www.cloudshark.org/).

- The file `2015-09-18-Nuclear-EK-traffic.pcap` comes from a blog
  post:
  [NUCLEAR EK FROM 178.62.72.26 - OAACDERESFTU.TK](https://www.malware-traffic-analysis.net/2015/09/18/index.html).

- The file `ipv6_all.xml` comes from the
  [logstash-codec-nmap](https://github.com/logstash-plugins/logstash-codec-nmap/)
  repository.

## MongoDB backup ##

The Elasticsearch backend can only be used for the `view` purpose. For
that, it needs data from `nmap` and `passive` purposes to build the
view. In Travis-CI, the Elasticsearch backend uses a MongoDB server to
provide the `nmap` and `passive` purposes.

The backend is located in
`tests/mongodb_backup/backup_nmap_passive.tar.bz2` and can be build
using the following commands:

```sh
DB=mongodb python tests.py 30_nmap 40_passive
rm -rf ./backup/ && mkdir ./backup/
mongodump --db=ivre --out=./backup/
mv ./backup/ivre/*.bson ./backup/
tar jcf ./backup_nmap_passive.tar.bz2 ./backup/{hosts,passive,scans}.bson
```
