<img src="imgs/58058301.png" width="10%">

# TiDBインストール(Podman Desktopより)
1. Podman Desktopからimages→Pullを選択する
1. 検索窓にpingcap tidbなどと入力し, docker.io/pingcap/tidbを選択する.
   ![1](imgs/スクリーンショット%202025-02-01%2018.53.18.png)
1. Pull Imageボタンをクリック
1. Pullが完了したら,Doneボタンに切り替わる
   ![2](imgs/スクリーンショット%202025-02-01%2018.57.11.png)
1. ImagesからPullしたtidbのイメージの▶️をクリック
   ![3](imgs/スクリーンショット%202025-02-01%2018.59.47.png)
1. 遷移した画面でStart Containerボタンをクリックする
   ![4](imgs/スクリーンショット%202025-02-01%2019.02.29.png)

# mysql-clientをインストール
同一container内にインストールする.
1. /etc/yum.repos.dにmysql-client.repoを作成する.
    ```bash
    vi /etc/yum.repos.d/mysql-client.repo
    ```
1. 以下の内容を記述する.
    ```
    [mysql84-community]
    name=MySQL 8.4 Community Server
    baseurl=https://repo.mysql.com/yum/mysql-8.4-community/el/9/aarch64/
    enabled=1
    gpgcheck=1
    gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-mysql
    ```
    1. baseurlについて<br/>
        以下のURLで確認する.<br/>
        [https://repo.mysql.com/yum/](https://repo.mysql.com/yum/)<br/>
        1. mysql-{version}-community/を選択する.
        2. el/を選択する.
        3. 9/を選択する.
        4. CPUの確認を実施して, aarch64/を選択する.
        5. mysql-community-client-{version}..>でバージョン確認.
    1. CPUの確認<br/>
        以下のコマンドで確認する.
        ```bash
        > uname -a
        ....aarch64 aarch64 aarch64 GNU/Linux
        ```
        aarch64と表示された.
    1. GPGキーについて<br/>
        以下のURLのサイトを表示する.<br/>
        [http://pgp.mit.edu](http://pgp.mit.edu)
        1. Search String:にmysqlと入力する.
        1. Do the search!ボタンをクリックする.
        1. -----BEGINから-----ENDの行までをコピーする.
        1. /etc/pki/rpm-gpgにRPM-GPG-KEY-mysqlファイルを作成する.
            ```bash
            vi /etc/pki/rpm-gpg/RPM-GPG-KEY-mysql
            ```
        1. コピーしたキーを上記のRPM-GPG-KEY-mysqlファイルに貼り付ける.
1. 以下のコマンドでrepoが表示されることを確認する.
    ```bash
    > dnf repolist enabled | grep mysql
    ```
    ![5](imgs/スクリーンショット%202025-02-02%204.05.24.png)
    途中でIs this ok [y/N]:と表示されるのでyを入力
1. Complete!と表示されればインストール完了.
    ![6](imgs/スクリーンショット%202025-02-02%204.08.47.png)
1. 以下のコマンドを実行し,ログインできればTiDBへの接続完了.
    ```bash
    > mysql -h 127.0.0.1 -P 4000 -u root 
    ```
    ![7](imgs/スクリーンショット%202025-02-02%204.15.19.png)


# 環境
* Mac OS 15.2
* Podman version 5.3.1
* Podman Desktop 1.16.0
* TiDB v7.5.1

# 参考
* [dockerhub](https://hub.docker.com/r/pingcap/tidb)
* [【RockyLinux8】みんな大好き MySQL8.0のインストール【Community Clientのみ】](https://qiita.com/cokemaniaIIDX/items/fe9e6e77699ec2705124)
* [LinuxでOSが32bit版か64bit版かを確認する方法 (uname)](http://tech.clickyourstyle.com/articles/47)

# 変更履歴
* 2025.02.01 - 新規作成

-EOF-