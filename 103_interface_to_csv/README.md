# 概要
Junos の機器に `show interfaces` コマンドを実行して、結果をパースして、 CSV ファイルに保存します。

## ファイル説明
- `interface_to_csv.yml`: Playbook 本体
- `juniper_junos_show_interfaces.template`: パースするための TextFSM テンプレートファイル 、[networktocode/ntc-templates](https://github.com/networktocode/ntc-templates/tree/master/templates)から。
- `template_interface_junos.txt`: パースした結果を受け取り、CSV に成形する Jinja2 テンプレートファイル
- `result_interface.csv`: 出力されるCSVファイル

## 追加インストールす
Playbook 内で使用している [parse_cli_textfsm](https://docs.ansible.com/ansible/latest/user_guide/playbooks_filters.html#network-cli-filters) フィルターはあらかじめ、 textfsm をインストールしておく必要があります。
`pip install textfsm`



# 実行例
## ansible-playbook コマンド
```
[vagrant@centos7 demo]$ ansible-playbook -i inventory interface_to_csv.yml

PLAY [junos] **********************************************************

TASK [show command test] **********************************************

ok: [172.16.0.1]

TASK [output csv file] ************************************************

changed: [172.16.0.1]

PLAY RECAP ***********************************************************************
172.16.0.1          : ok=2    changed=1    unreachable=0    failed=0
```

## 保存されたCSV
```
[vagrant@centos7 demo]$ cat result_interface.csv
"INTERFACE","ADMIN_STATE","LINK_STATUS","HARDWARE_TYPE","MTU"
"ge-0/0/0","Enabled","Up","Ethernet","1514"
"ge-0/0/0.0","","","","1500"
"gr-0/0/0","Enabled","Up","GRE","Unlimited"
"ip-0/0/0","Enabled","Up","IP-over-IP","Unlimited"
"lsq-0/0/0","Enabled","Up","LinkService","1504"
"lt-0/0/0","Enabled","Up","Logical-tunnel","Unlimited"
"mt-0/0/0","Enabled","Up","GRE","Unlimited"
"sp-0/0/0","Enabled","Up","Adaptive-Services","9192"
"sp-0/0/0.0","","","","9192"
"sp-0/0/0.16383","","","","9192"
"ge-0/0/1","Enabled","Up","Ethernet","1514"
"ge-0/0/1.0","","","","1500"
"ge-0/0/2","Enabled","Up","Ethernet","1514"
"ge-0/0/2.0","","","","1500"
"dsc","Enabled","Up","Software-Pseudo","Unlimited"
"gre","Enabled","Up","GRE","Unlimited"
"ipip","Enabled","Up","IP-over-IP","Unlimited"
"irb","Enabled","Up","Ethernet","1514"
"lo0","Enabled","Up","Loopback","Unlimited"
"lo0.16384","","","","Unlimited"
"lo0.16385","","","","Unlimited"
"lsi","Enabled","Up","LSI","1496"
"mtun","Enabled","Up","GRE","Unlimited"
"pimd","Enabled","Up","PIM-Decapsulator","Unlimited"
"pime","Enabled","Up","PIM-Encapsulator","Unlimited"
"pp0","Enabled","Up","PPPoE","1532"
"ppd0","Enabled","Up","PIM-Decapsulator","Unlimited"
"ppe0","Enabled","Up","PIM-Encapsulator","Unlimited"
"st0","Enabled","Up","Secure-Tunnel","9192"
"tap","Enabled","Up","Interface-Specific","Unlimited"
"vlan","Enabled","Down","VLAN","1518"
```

# デモ動画
https://www.youtube.com/watch?v=6QqXbJBH4i8
