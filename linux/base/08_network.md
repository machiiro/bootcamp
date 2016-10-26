# ネットワーク

## ifconfig - マシンのネットワークインターフェースを確認する

```bash
$ ifconfig
eth0      Link encap:Ethernet  HWaddr 06:2C:A1:83:83:B5
          inet addr:10.0.0.151  Bcast:10.0.0.255  Mask:255.255.255.0
          inet6 addr: fe80::42c:a1ff:fe83:83b5/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:9001  Metric:1
          RX packets:782321 errors:0 dropped:0 overruns:0 frame:0
          TX packets:688739 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000
          RX bytes:76371020 (72.8 MiB)  TX bytes:340366945 (324.5 MiB)

lo        Link encap:Local Loopback
          inet addr:127.0.0.1  Mask:255.0.0.0
          inet6 addr: ::1/128 Scope:Host
          UP LOOPBACK RUNNING  MTU:65536  Metric:1
          RX packets:37755 errors:0 dropped:0 overruns:0 frame:0
          TX packets:37755 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0
          RX bytes:75419781 (71.9 MiB)  TX bytes:75419781 (71.9 MiB)
```

## ping - 対象ホストとのネットワーク疎通確認を行う

```bash
$ ping www.google.co.jp
PING www.google.co.jp (216.58.221.163) 56(84) bytes of data.
64 bytes from kix03s01-in-f163.1e100.net (216.58.221.163): icmp_seq=1 ttl=57 time=8.27 ms
64 bytes from kix03s01-in-f163.1e100.net (216.58.221.163): icmp_seq=2 ttl=57 time=8.28 ms
```

## nc - 対象ホストの特定ポートに対して疎通確認を行う

```bash
$ nc -zv {IPアドレス} {ポート}
found 0 associations
found 1 connections:
     1:	flags=82<CONNECTED,PREFERRED>
	outif en0
	src xx.xx.xx.xx port 55731
	dst xx.xx.xx.xx port 80
	rank info not available
	TCP aux info available

Connection to xx.xx.xx.xx port 80 [tcp/http] succeeded!
```

## dig - ドメイン情報を DNS サーバーに問合せる

```bash
$ dig redmine.machiiro.jp

; <<>> DiG 9.8.3-P1 <<>> redmine.machiiro.jp
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 16059
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 0

;; QUESTION SECTION:
;redmine.machiiro.jp.		IN	A

;; ANSWER SECTION:
redmine.machiiro.jp.	3600	IN	A	52.193.54.224

;; Query time: 12 msec
;; SERVER: 210.145.254.169#53(210.145.254.169)
;; WHEN: Fri Mar 11 10:46:14 2016
;; MSG SIZE  rcvd: 53
```
