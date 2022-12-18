# Ansible構築・運用ガイドブック プレイブック集の学習・実践メモ
## 概要
このリポジトリでは、『Ansible構築・運用ガイドブック』を学習時に実践したフォルダを掲載しています。


## Chapter7の設定の追加や変更について

### VirtualBox上のVyOSをコンソールで操作設定
 ID:vyos Password:vyosでログイン
 ・show intで初期の設定を確認
　　eth1とeth2が未設定
　　eth2はansibleで自動設定するために未設定にしておく
 ・eth1にvagrantfileに記載しているvyosのipアドレスを設定する
  　configure
  　　↓
　　set interfaces ethernet eth1 address 192.168.100.20
　・sshを有効にする（すでにsshが有効になっていた）
　　https://zaki-hmkc.hatenablog.com/entry/2021/04/08/100014を参照
    set service ssh
  ・ipアドレスの設定やssh有効の設定をした後、設定を有効にする
    commit → save

### /etc/ansible/ansible.cfgに追加
 [defaults]
interpreter_python=/usr/bin/python3
host_key_checking = False

※ansible.cfgを変更したくない場合は、環境変数を設定できます。  
　export ANSIBLE_HOST_KEY_CHECKING=False

### python3、pip3のインストール

sudo yum install python3
sudo yum install pip3
sudo yum install pip3.6

### pip3 listのコマンドで警告が出たときの対処法
（pip3 listの警告）
DEPRECATION: The default format will switch to columns in the future. You can use --format=(legacy|columns) (or define a format=(legacy|columns) in your pip.conf under the [list] section) to disable this warning.
　↓
【pip3 listで警告でなくすため以下の手順でcommandを打つ】
which  pip.conf
mkdir ~/.pip
touch pip.conf
sudo 777 pip.conf

vi pip.conf(編集する)
[list]
format=columns

【pip3 listで警告がでなくなる】
　pip3 list

### python3 や pip3 のコマンドを環境変数 $PATH が通っている /usr/local/bin 以下の実行ファイルにシンボリックリンクが貼る。
sudo ln -s /usr/bin/pip3.6 /usr/local/bin/pip


### ★★python-setup-py-egg-infoのエラー解決方法
ansible-playbook -i hosts vyos_interface.yml実行時に
"python-setup-py-egg-info"の内容を含んだエラーが表示された場合には
pipとsetuptoolsをアップグレードすると解消する
　↓　↓
※pipとsetuptoolsをアップグレードのコマンドを打つ
sudo python3 -m pip install --upgrade pip
sudo python3 -m pip install --upgrade setuptools

**（参考サイト）
**【解決済み】コマンド「python setuppy egg_info」がエラーコード1で失敗しました
https://jp.easeus.com/data-recovery-solution/python-setup-py-egg-info-failed-with-error-code-1.html




