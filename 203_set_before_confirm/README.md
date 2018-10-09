# 概要
コンフィグ投入前に、キー入力によるワンックション挟みます。
- `y`: 処理継続
- `y`以外: 処理中止

# 実行例
## OK で続ける場合
```
[vagrant@centos7 demo]$ ansible-playbook -i inventory set_before_confirm.yml

PLAY [junos] ******************************************************

TASK [confirm] ****************************************************

[confirm]
continue? [y/N]:　y <- ここで処理が止まるので、OKであれば y を入力
ok: [172.16.0.1]

TASK [abort] ******************************************************
skipping: [172.16.0.1]

TASK [config test] ************************************************
changed: [172.16.0.1]

PLAY RECAP ********************************************************
172.16.0.1        : ok=2    changed=1    unreachable=0    failed=0
```

## NG で中止する場合

```
[vagrant@centos7 demo]$ ansible-playbook -i inventory set_before_confirm.yml

PLAY [junos] ********************************************************************

TASK [confirm] ********************************************************************

[confirm]
continue? [y/N]: N  <- こんどは N を入力して中止する
ok: [172.16.0.1]

TASK [abort] ********************************************************
fatal: [172.16.0.1]: FAILED! => {"changed": false, "msg": "Failed as requested from task"}

PLAY RECAP *********************************************************************
172.16.0.1          : ok=1    changed=0    unreachable=0    failed=1
```

# デモ動画
https://www.youtube.com/watch?v=S7BKjJn0h2U