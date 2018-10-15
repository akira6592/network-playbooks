# 概要
Playbook や インベントリファイルを作成せずに、コマンドのみで Cisco IOS や Juniper Junos のコンフィグをファイルとして保存します。
`jq` を利用しますので、あらかじめインストールしておきます。

## 動作確認環境
- Ansible 2.7.0

# Cisco IOS 編 

## コマンド
```
export ANSIBLE_STDOUT_CALLBACK=json
export ANSIBLE_LOAD_CALLBACK_PLUGINS=True
ansible -i ios-xe-mgmt.cisco.com, all \
  -m ios_command -a "commands='show running-config'" \
  -c network_cli -u root -k -e ansible_network_os=ios \
  | jq -r ".plays[0].tasks[0].hosts[].stdout[0]" > ios_config.txt
```

## 実行例
```bash
$ export ANSIBLE_STDOUT_CALLBACK=json
$ export ANSIBLE_LOAD_CALLBACK_PLUGINS=True
$ ansible -i ios-xe-mgmt.cisco.com, all \
>   -m ios_command -a "commands='show running-config'" \
>   -c network_cli -u root -k -e ansible_network_os=ios \
>   | jq -r ".plays[0].tasks[0].hosts[].stdout[0]" > ios_config.txt
SSH password:   # パスワードを入力
＄
＄ cat junos_config.txt   # 保存したコンフィグファイルを表示
(ansible2700) [vagrant@centos7 techfest]$ cat ios_config.txt
Building configuration...

Current configuration : 4356 bytes
!
! Last configuration change at 11:27:55 UTC Mon Oct 15 2018 by NETCONF
!
version 16.8
...(略)...
```


# Juniper Junos 編
## コマンド
```bash
export ANSIBLE_STDOUT_CALLBACK=json
export ANSIBLE_LOAD_CALLBACK_PLUGINS=True

ansible -i 172.16.0.1, all \
  -m junos_command -a "commands='show configuration'" \
  -c netconf -u root -k -e ansible_network_os=junos \
  | jq -r ".plays[0].tasks[0].hosts[].stdout[0]" > junos_config.txt
```

## 実行例
```bash
$ export ANSIBLE_STDOUT_CALLBACK=json
＄ export ANSIBLE_LOAD_CALLBACK_PLUGINS=True
＄ ansible -i 172.16.0.1, all \
>   -m junos_command -a "commands='show configuration'" \
>   -c netconf -u root -k -e ansible_network_os=junos \
>   | jq -r ".plays[0].tasks[0].hosts[].stdout[0]" > junos_config.txt
SSH password:   # パスワードを入力
＄
＄ cat junos_config.txt   # 保存したコンフィグファイルを表示
## Last changed: 2018-10-04 05:56:28 UTC
version 12.1X47-D15.4;
system {
    host-name vsrx1;
...(略)...
```

# 参考資料
https://www.slideshare.net/akira6592/ansibleadhocnetworkautomation/12
