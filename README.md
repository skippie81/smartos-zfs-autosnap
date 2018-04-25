# smartos-zfs-autosnap

Automated snapshots at fixed times of your zfs volumes

## Usage

```
  usage: autosnap [-h] [-d] [-p <prfix>] -t <type> [–Z] [zfs] [zfs] ...

    -p   <prfeix>   :   zfs prefix (default: autosnap)
    -d              :   dryrun mode (do not realy create or remove any snapshot)
    -t              :   snapshot type
                            H = Hourly
                            D = Dayly
                            W = Weekly
                            M = Monthly

    -h              :   display this message.
```

### Examples

```
autosnap -t H -Z
autosnap -t M pool/example
autosnap -p autosnap -t W -Z pool/example
```

### Automation

via crontab

a working entry would be

```
# m     h     dom   mon   dow     command
0       *	     *     *     *       /opt/local/bin/autosnap -t H -Z 1> /opt/local/log/autosnap_hourly.log 2>&1
5       0      *     *     *       /opt/local/bin/autosnap -t D -Z 1> /opt/local/log/autosnap_daily.log 2>&1
10      0	     *     *     1       /opt/local/bin/autosnap -t W -Z 1> /opt/local/log/autosnap.weekly.log 2>&1
30      0      1     *     *       /opt/local/bin/autosnap -t M -Z 1> /opt/local/log/autosnap.monthly.log 2>&1
```

## Install

```
curl -kLo /opt/local/bin/autosnap https://raw.githubusercontent.com/skippie81/smartos-zfs-autosnap/master/autosnap
chmod +x /opt/local/bin/autosnap 
```