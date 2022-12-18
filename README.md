# Ansible構築・運用ガイドブック プレイブック集の学習・実践メモ
## 概要
このリポジトリでは、『Ansible構築・運用ガイドブック』を学習時に実践したフォルダを掲載しています。

## 設定の追加や変更について
### /etc/ansible/ansible.cfgに追加
 [defaults]
interpreter_python=/usr/bin/python3
host_key_checking = False

※ansible.cfgを変更したくない場合は、環境変数を設定できます。  
　export ANSIBLE_HOST_KEY_CHECKING=False

### python3 や pip3 のコマンドを環境変数 $PATH が通っている /usr/local/bin 以下の実行ファイルにシンボリックリンクが貼る。
sudo ln -s /usr/bin/pip3.6 /usr/local/bin/pip





