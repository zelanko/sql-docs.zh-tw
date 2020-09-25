---
title: azdata postgres 參考
titleSuffix: SQL Server big data clusters
description: azdata postgres 命令的參考文章。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: seanw
ms.date: 09/22/2020
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 80b83f53c486a90c635924accf36e5acff98fe2c
ms.sourcegitcommit: d56f1eca807c55cf606a6316f3872585f014fec1
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/22/2020
ms.locfileid: "90942358"
---
# <a name="azdata-postgres"></a>azdata postgres

適用於 `azdata`

下列文章提供 **azdata** 工具中 **sql** 命令的參考。 如需其他 **azdata** 命令的詳細資訊，請參閱 [azdata 參考](reference-azdata.md)

## <a name="commands"></a>命令

|命令|描述|
| --- | --- |
[azdata postgres shell](#azdata-postgres-shell) | Postgres 的命令列殼層介面。 請參閱https://www.pgcli.com/
[azdata postgres query](#azdata-postgres-query) | 查詢命令允許在資料庫工作階段中執行 PostgreSQL 命令。
## <a name="azdata-postgres-shell"></a>azdata postgres shell
Postgres 的命令列殼層介面。 請參閱https://www.pgcli.com/
```bash
azdata postgres shell [--dbname -d] 
                      [--host]  
                      
[--port -p]  
                      
[--password -w]  
                      
[--no-password]  
                      
[--single-connection]  
                      
[--username -u]  
                      
[--pgclirc]  
                      
[--dsn]  
                      
[--list-dsn]  
                      
[--row-limit]  
                      
[--less-chatty]  
                      
[--prompt]  
                      
[--prompt-dsn]  
                      
[--list -l]  
                      
[--auto-vertical-output]  
                      
[--warn]  
                      
[--no-warn]
```
### <a name="examples"></a>範例
啟動互動式體驗的範例命令列。
```bash
azdata postgres shell
```
使用所提供資料庫和使用者的範例命令列
```bash
azdata postgres shell --dbname <database> --username <username> --host <host>
```
要開始使用完整連接字串的範例命令列。
```bash
azdata postgres shell --dbname postgres://user:passw0rd@example.com:5432/master 
```
### <a name="optional-parameters"></a>選擇性參數
#### `--dbname -d`
所要連線的資料庫名稱。
#### `--host`
Postgres 資料庫的主機位址。
#### `--port -p`
Postgres 執行個體接聽所在的連接埠號碼。
#### `--password -w`
強制密碼提示。
#### `--no-password`
永不提示輸入密碼。
#### `--single-connection`
請勿為了完成而使用不同的連線。
#### `--username -u`
用於連線到 postgres 資料庫的使用者名稱。
#### `--pgclirc`
pgclirc 檔案的位置。
#### `--dsn`
使用已設定到 pgclirc 檔案的 [alias_dsn] 區段中的 DSN。
#### `--list-dsn`
已設定到 pgclirc 檔案的 [alias_dsn] 區段中的 DSN 清單。
#### `--row-limit`
設定資料列限制提示的閾值。 使用 0 來停用提示。
#### `--less-chatty`
在啟動時略過簡介並於結束時退出。
#### `--prompt`
提示格式(預設值："\u@\h:\d>")。
#### `--prompt-dsn`
使用 DSN 別名進行連線的提示格式 (預設值："\u@\h:\d>")。
#### `--list -l`
列出可用的資料庫，然後結束。
#### `--auto-vertical-output`
如果結果寬度大於終端機寬度，則會自動切換到垂直輸出模式。
#### `--warn`
在執行破壞性查詢之前發出警告。
#### `--no-warn`
在執行破壞性查詢之前發出警告。
### <a name="global-arguments"></a>全域引數
#### `--debug`
增加記錄詳細資訊，以顯示所有偵錯記錄。
#### `--help -h`
顯示此說明訊息並結束。
#### `--output -o`
輸出格式。  允許的值：json、jsonc、table、tsv。  預設值：json。
#### `--query -q`
JMESPath 查詢字串。 如需詳細資訊和範例，請參閱 [http://jmespath.org/](http://jmespath.org)。
#### `--verbose`
增加記錄詳細資訊。 使用 --debug 來取得完整偵錯記錄。
## <a name="azdata-postgres-query"></a>azdata postgres query
查詢命令允許在資料庫工作階段中執行 PostgreSQL 命令。
```bash
azdata postgres query --q -q 
                      [--host]  
                      
[--dbname -d]  
                      
[--port -p]  
                      
[--username -u]
```
### <a name="examples"></a>範例
列出 information_schema 中的所有資料表。
```bash
azdata postgres query --host <host> --username <username> -q "SELECT * FROM information_schema.tables"
```
### <a name="required-parameters"></a>必要參數
#### `--q -q`
要執行的 PostgreSQ 查詢。
### <a name="optional-parameters"></a>選擇性參數
#### `--host`
Postgres 資料庫的主機位址。
`localhost`
#### `--dbname -d`
要在其中執行查詢的資料庫。
#### `--port -p`
Postgres 執行個體接聽所在的連接埠號碼。
`5432`
#### `--username -u`
用於連線到 postgres 資料庫的使用者名稱。
### <a name="global-arguments"></a>全域引數
#### `--debug`
增加記錄詳細資訊，以顯示所有偵錯記錄。
#### `--help -h`
顯示此說明訊息並結束。
#### `--output -o`
輸出格式。  允許的值：json、jsonc、table、tsv。  預設值：json。
#### `--query -q`
JMESPath 查詢字串。 如需詳細資訊和範例，請參閱 [http://jmespath.org/](http://jmespath.org)。
#### `--verbose`
增加記錄詳細資訊。 使用 --debug 來取得完整偵錯記錄。

## <a name="next-steps"></a>後續步驟

如需其他 **azdata** 命令的詳細資訊，請參閱 [azdata 參考](reference-azdata.md)。 

如需如何安裝 **azdata** 工具的詳細資訊，請參閱[安裝 azdata](..\install\deploy-install-azdata.md)。

