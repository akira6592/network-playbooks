# 概要
Junos の機器に `show version` コマンドを実行して画面上に表示します。

# 実行例
```
[vagrant@centos7 demo]$ ansible-playbook -i inventory show_command_simple.yml

PLAY [junos] ******************************************************************

TASK [show command test] ******************************************************

ok: [172.16.0.1]

TASK [debug output] ***********************************************************

ok: [172.16.0.1] => {
    "msg": [
        "Hostname: vsrx1",
        "Model: firefly-perimeter",
        "JUNOS Software Release [12.1X47-D15.4]"
    ]
}

PLAY RECAP ********************************************************************
172.16.0.1                 : ok=2    changed=0    unreachable=0    failed=0
```

# デモ動画
https://www.youtube.com/watch?v=pBhnsvKeZeU