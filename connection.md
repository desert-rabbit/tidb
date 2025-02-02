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
1. mysql-connector-pythonをインストール
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


# 変更履歴
* 2025.02.02 - 新規作成

-EOF-