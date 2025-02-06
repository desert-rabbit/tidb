<img src="imgs/58058301.png" width="10%">

# バージョン確認方法

以下のコマンドを実行すると, バージョンが表示される.
```
mysql> select tidb_version();
```

```
| Release Version: v7.5.1
Edition: Community
Git Commit Hash: 7d16cc79e81bbf573124df3fd9351c26963f3e70
Git Branch: heads/refs/tags/v7.5.1
UTC Build Time: 2024-02-27 14:30:59
GoVersion: go1.21.6
Race Enabled: false
Check Table Before Drop: false
Store: unistore |
```

# 環境
* Mac OS 15.2
* Podman version 5.3.1
* Podman Desktop 1.16.0
* TiDB v7.5.1

# 変更履歴
* 2025.02.06 - 新規作成

-EOF-