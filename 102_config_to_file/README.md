# 概要
Junos の機器に `show configuration` コマンドを実行して、結果を `show_config_ホスト名.txt` というファイルに保存します。


# 実行例

```
[vagrant@centos7 demo]$ ansible-playbook -i inventory config_to_file.yml

PLAY [junos] **********************************************************

TASK [show command test] **********************************************

ok: [172.16.0.1]

TASK [save config to file] ********************************************

changed: [172.16.0.1]

PLAY RECAP ************************************************************
172.16.0.1           : ok=2    changed=1    unreachable=0    failed=0

[vagrant@centos7 demo]$ cat show_config_172.16.0.1.txt
## Last changed: 2018-06-28 05:45:50 UTC
version 12.1X47-D15.4;
system {
    host-name vsrx1;
    root-authentication {
        encrypted-password "$1$nq.N1UsY$Jx...(略)...";
        ssh-rsa "ssh-rsa AAAAB3NzaC1yc2...(略)....";
    }
...(略)....
 ge-0/0/1 {
        unit 0 {
            family inet {
                address 172.16.0.1/24;
            }
        }
    }
...(略)....
}
```

# デモ動画
https://www.youtube.com/watch?v=aRfWXE0uUUU