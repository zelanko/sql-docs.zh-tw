---
title: azdata sql 參考
titleSuffix: SQL Server big data clusters
description: azdata sql 命令的參考文章。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 06/22/2020
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: bb7dd195d489be289cf434e8e4651ac17c6a6709
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/28/2020
ms.locfileid: "87242979"
---
# <a name="azdata-sql"></a>azdata sql

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

下文提供 `azdata` 工具中 `sql` 命令的參考。 如需其他 `azdata` 命令的詳細資訊，請參閱 [azdata 參考](reference-azdata.md)。

## <a name="commands"></a>命令
| 命令 | 說明 |
| --- | --- |
[azdata sql shell](#azdata-sql-shell) | SQL DB CLI 可讓使用者透過 T-SQL 與 SQL Server 互動。
[azdata sql query](#azdata-sql-query) | 查詢命令允許執行 T-SQL 查詢。
## <a name="azdata-sql-shell"></a>azdata sql shell
SQL DB CLI 可讓使用者透過 T-SQL 與 SQL Server 互動。
```bash
azdata sql shell 
```
### <a name="examples"></a>範例
啟動互動式體驗的範例命令列。
```bash
azdata sql shell
```
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
查詢命令允許執行 T-SQL 查詢。
```bash
azdata sql query --database -d 
                 -q
```
### <a name="examples"></a>範例
選取資料表名稱的清單。  資料庫預設為主要。
```bash
azdata sql query "SELECT name FROM SYS.TABLES"
```
### <a name="required-parameters"></a>必要參數
#### `--database -d`
要在其中執行查詢的資料庫。  預設值是主要。
#### `-q`
要執行的 T-SQL 查詢。
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

如需其他 `azdata` 命令的詳細資訊，請參閱 [azdata 參考](reference-azdata.md)。 如需如何安裝 `azdata` 工具的詳細資訊，請參閱[安裝 azdata 來管理 SQL Server 2019 巨量資料叢集](deploy-install-azdata.md)。
