# マシンの情報を知る

## OS を確認する

```bash
$ cat /proc/version
Linux version 4.1.17-22.30.amzn1.x86_64 (mockbuild@gobi-build-60009) (gcc version 4.8.3 20140911 (Red Hat 4.8.3-9) (GCC) ) #1 SMP Fri Feb 5 23:44:22 UTC 2016

# RHEL/CentOS の場合
$ cat /etc/redhat-release
CentOS Linux release 7.2.1511 (Core)
```

## hostname - ホスト名を確認する

```bash
$ hostname
ip-10-0-0-151
```

## lscpu  - CPU を確認する

```bash
$ lscpu
アーキテクチャ: x86_64
CPU op-mode(s):        32-bit, 64-bit
Byte Order:            Little Endian
CPU(s):                2
On-line CPU(s) list:   0,1
コアあたりのスレッド数:1
ソケットあたりのコア数:2
Socket(s):             1
NUMAノード:         1
ベンダーID:        GenuineIntel
CPUファミリー:    6
モデル:             62
Model name:            Intel(R) Xeon(R) CPU E5-2670 v2 @ 2.50GHz
ステッピング:    4
CPU MHz:               2500.084
BogoMIPS:              5000.16
ハイパーバイザーベンダー:Xen
仮想化タイプ:    完全仮想化
L1d キャッシュ:   32K
L1i キャッシュ:   32K
L2 キャッシュ:    256K
L3 キャッシュ:    25600K
NUMAノード 0 CPU:   0,1
```

## free - メモリの使用状況を確認する

```bash
$ free
              total        used        free      shared  buff/cache   available
Mem:         468012       72076      121340        4712      274596      357228
Swap:       1048572           0     1048572
```

## df - ディスクの使用状況を確認する

```bash
$ df
ファイルシス   1K-ブロック    使用   使用可 使用% マウント位置
/dev/xvda1        30830568 3755292 26975028   13% /
devtmpfs           2015984      56  2015928    1% /dev
tmpfs              2024992       0  2024992    0% /dev/shm
```

## top - 現在のシステム状況を確認する

実行中にコマンドを受け付ける。
例えば、`Shift+p` で CPU 使用率順にソート、`Shift+m` でメモリ使用率順にソートされる。

```bash
$ top
top - 10:10:29 up 24 min,  1 user,  load average: 0.00, 0.01, 0.04
Tasks:  90 total,   2 running,  88 sleeping,   0 stopped,   0 zombie
%Cpu(s):  0.0 us,  0.0 sy,  0.0 ni,100.0 id,  0.0 wa,  0.0 hi,  0.0 si,  0.0 st
KiB Mem :   468012 total,   120384 free,    72340 used,   275288 buff/cache
KiB Swap:  1048572 total,  1048572 free,        0 used.   356964 avail Mem

  PID USER      PR  NI    VIRT    RES    SHR S %CPU %MEM     TIME+ COMMAND
    1 root      20   0   43888   6488   3912 S  0.0  1.4   0:01.05 systemd
    2 root      20   0       0      0      0 S  0.0  0.0   0:00.00 kthreadd
    3 root      20   0       0      0      0 S  0.0  0.0   0:00.00 ksoftirqd/0
    6 root      20   0       0      0      0 S  0.0  0.0   0:00.23 kworker/u2:0
    7 root      rt   0       0      0      0 S  0.0  0.0   0:00.00 migration/0
    8 root      20   0       0      0      0 S  0.0  0.0   0:00.00 rcu_bh
...
```

## uptime - 稼働時間を確認する

```bash
# マシンが再起動してたりしないか確認できる
$ uptime
 10:13:17 up 27 min,  1 user,  load average: 0.00, 0.01, 0.04
```

## date - サーバー日時を確認する

```bash
$ date
2016年  3月 10日 木曜日 19:19:27 JST
```

## w - ログインユーザーを確認する

```bash
$ w
 19:18:52 up 1 day,  6:42,  1 user,  load average: 0.00, 0.01, 0.05
USER     TTY      FROM              LOGIN@   IDLE   JCPU   PCPU WHAT
ec2-user pts/0    p84068-ipbffx02m 19:02    0.00s  0.01s  0.00s w
```
