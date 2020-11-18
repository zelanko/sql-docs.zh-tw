---
title: azdata sql 參考
titleSuffix: SQL Server big data clusters
description: azdata sql 命令的參考文章。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: seanw
ms.date: 09/22/2020
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 794c7be56eaa0591d120b4fea40a725fdeecaac1
ms.sourcegitcommit: 29a2be59c56f8a4b630af47760ef38d2bf56a3eb
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/22/2020
ms.locfileid: "92358106"
---
# <a name="azdata-sql"></a>azdata sql

適用於 [!INCLUDE [azure-data-cli-azdata](../../includes/azure-data-cli-azdata.md)]

下列文章提供 **azdata** 工具中 **sql** 命令的參考。 如需其他 **azdata** 命令的詳細資訊，請參閱 [azdata 參考](reference-azdata.md)

## <a name="commands"></a>命令

|命令|說明|
| --- | --- |
[azdata sql shell](#azdata-sql-shell) | SQL CLI 可讓使用者透過 T-SQL 與 SQL Server 和 Azure SQL 互動。
[azdata sql query](#azdata-sql-query) | SQL CLI 可讓使用者透過 T-SQL 與 SQL Server 和 Azure SQL 互動。
## <a name="azdata-sql-shell"></a>azdata sql shell
SQL CLI 可讓使用者透過 T-SQL 與 SQL Server 和 Azure SQL 互動。
```bash
azdata sql shell [--username -u] 
                 [--database -d]  
                 
[--server -s]  
                 
[--integrated -e]  
                 
[--mssqlclirc]  
                 
[--row-limit]  
                 
[--less-chatty]  
                 
[--auto-vertical-output]  
                 
[--encrypt -n]  
                 
[--trust-server-certificate -c]  
                 
[--connect-timeout -l]  
                 
[--application-intent -k]  
                 
[--multi-subnet-failover -m]  
                 
[--packet-size]  
                 
[--dac-connection -a]  
                 
[--input-file -i]  
                 
[--output-file]  
                 
[--enable-sqltoolsservice-logging]  
                 
[--prompt]
```
### <a name="examples"></a>範例
啟動互動式體驗的範例命令列。
```bash
azdata sql shell
```
使用所提供伺服器、使用者與資料庫的範例命令列
```bash
azdata sql shell --server localhost --username sa --database master         
```
### <a name="optional-parameters"></a>選擇性參數
#### `--username -u`
使用者名稱以連線到資料庫。
#### `--database -d`
所要連線的資料庫名稱。
#### `--server -s`
SQL Server 執行個體名稱或位址。
#### `--integrated -e`
使用 Windows 上的整合式驗證。
#### `--mssqlclirc`
mssqlclirc 設定檔的位置。
#### `--row-limit`
設定資料列限制提示的閾值。 使用 0 來停用提示。
#### `--less-chatty`
在啟動時略過簡介並於結束時退出。
#### `--auto-vertical-output`
如果結果寬度大於終端寬度，則自動切換到垂直輸出模式。
#### `--encrypt -n`
SQL Server 會在伺服器已安裝憑證的情況下，對所有資料使用 SSL 加密。
#### `--trust-server-certificate -c`
會通道加密，同時略過驗證信任的憑證鏈結。
#### `--connect-timeout -l`
在終止要求之前等待伺服器連線的時間 (以秒為單位)。
#### `--application-intent -k`
宣告當連線到 SQL Server 可用性群組中的資料庫時的應用程式工作負載類型。
#### `--multi-subnet-failover -m`
如果應用程式要連線到不同子網路上的 AlwaysOn 可用性群組，則設定此選項能以更快的速度偵測目前使用中的伺服器並建立連線。
#### `--packet-size`
用於與 SQL Server 通訊之網路封包的大小 (位元組)。
#### `--dac-connection -a`
使用專用管理員連接 (DAC) 來連線到 SQL Server。
#### `--input-file -i`
指定包含要處理之 SQL 陳述式批次的檔案。
#### `--output-file`
指定從查詢接收輸出的檔案。
#### `--enable-sqltoolsservice-logging`
啟用 SqlToolsService 的診斷記錄。
#### `--prompt`
提示格式 (預設值：\d>
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
## <a name="azdata-sql-query"></a>azdata sql query
SQL CLI 可讓使用者透過 T-SQL 與 SQL Server 和 Azure SQL 互動。
```bash
azdata sql query -q 
                 [--database -d]  
                 
[--username -u]  
                 
[--server -s]  
                 
[--integrated -e]
```
### <a name="examples"></a>範例
用於選取資料表名稱清單的範例命令列。
```bash
azdata sql query --server localhost --username sa --database master -q "SELECT name FROM SYS.TABLES"
```
### <a name="required-parameters"></a>必要參數
#### `-q`
要執行的 T-SQL 查詢。
### <a name="optional-parameters"></a>選擇性參數
#### `--database -d`
所要連線的資料庫名稱。
`master`
#### `--username -u`
使用者名稱以連線到資料庫。
#### `--server -s`
SQL Server 執行個體名稱或位址。
#### `--integrated -e`
使用 Windows 上的整合式驗證。
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

如需如何安裝 **azdata** 工具的詳細資訊，請參閱 [安裝 azdata](..\install\deploy-install-azdata.md)。

