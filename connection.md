# TiDBへの接続

## podman networkの設定
container間の通信ができないので, podman networkで通信ができるようにする.<br/>
TiDBのコンテナに, pythonのコンテナから接続することを例にする.
1. networkを新規に作成する.名前はmy-networkとする.<br/>
    ホストOSにて以下のコマンドを実行する.
    ```bash
    % podman network create my-network
    ```
1. 作成したnetworkにコンテナを追加する.<br/>
    TiDBのコンテナ名はagitated-rhodes.<br/>
    pythonのコンテナ名はeager-hermann.<br/>
    ホストOSで以下のコマンドを実行する.
    ```bash
    % podman network connect my-network agitated-rhodes
    % podman network connect my-network eager-hermann
    ```

## mysql-connector-python
1. mysql-connector-pythonをインストール<br/>
    pythonのコンテナ内で以下のコマンドを実行.
    ```bash
    (.venv)> pip install mysql-connector-python
    ```

1. pythonのコンテナ内で, プログラムを作成して実行
    ```python
    import mysql.connector

    conn = mysql.connector.connect(
        host="agitated_rhodes",
        port=4000,
        user="root",
        password="",
    )
    cursor = conn.cursor()
    cursor.close()
    conn.close()
    ```

# 環境
* Mac OS 15.2
* Podman 5.3.2
* Podman Desktop 1.16.0
* TiDB v7.5.1
* mysql-connector-python 9.2.0

# 変更履歴
* 2025.02.04 - 環境情報を追記
* 2025.02.02 - 新規作成

-EOF-