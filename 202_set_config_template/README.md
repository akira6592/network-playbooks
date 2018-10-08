# 概要
Junos の機器にテンプレートと変数から生成したコマンドを投入します。

# 実行例
```
[vagrant@centos7 demo]$ ansible-playbook -i inventory set_config_template.yml

PLAY [junos] *********************************************************

TASK [config test] ***************************************************
changed: [172.16.0.1]

PLAY RECAP **********************************************************************
172.16.0.1          : ok=1    changed=1    unreachable=0    failed=0

```