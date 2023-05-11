# 概要

スタティックルートの追加

1. `before_check` ロール: 追加するルートがまだないことを確認（show ip routeベース）
1. `configure` ロール: ルートを追加
1. `after_check` ロール: 追加したルートがあることを確認（show ip routeベース、show running-configuベース）


# 実行例

一連の流れ:

```sh
ansible-playbook -i inventory/ playbook.yml 
```

ルートの削除:
```sh
ansible-playbook -i inventory/ playbook.yml -t reset
```