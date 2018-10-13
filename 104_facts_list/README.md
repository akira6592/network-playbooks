# 概要
Cisco IOS の機器の、ホスト名、モデル名、バージョン、シリアル番号の一覧のCSVを出力します。

## ファイル説明
- `facts_list.yml`: Playbook 本体
- `facts_list.js`: CSV出力用Jinja2テンプレート 
- `facts_list.csv`: 出力されるCSVファイル


# 実行例
## ansible-playbook コマンド
```
(ansible2700) [vagrant@centos7 techfest]$ ansible-playbook -i inventory.ini facts_list.yml

PLAY [ios] ******************************************************************************

TASK [ios_facts] ***************************************************************************
ok: [ios1]
ok: [ios2]

TASK [template] ****************************************************************************
changed: [ios1]

PLAY RECAP *********************************************************************************
ios1                    : ok=2    changed=1    unreachable=0    failed=0
ios2                    : ok=1    changed=0    unreachable=0    failed=0
```

## 保存されたCSV
```
[vagrant@centos7 demo]$ cat facts_list.csv
"hostname","model","version","serialnum"
"leaf1","C9300-48U","16.06.03","FCW22XXXXX1"
"leaf2","C9300-48U","16.06.03","FCW22XXXXX2"
```

