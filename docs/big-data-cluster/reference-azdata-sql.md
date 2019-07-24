---
title: azdata sql 參考
titleSuffix: SQL Server big data clusters
description: Azdata sql 命令的參考文章。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 90512592901fcf83e4697b5eefc80a6df7aeb032
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/23/2019
ms.locfileid: "68426018"
---
# <a name="azdata-sql"></a>azdata sql

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

下列文章提供**azdata**工具中**sql**命令的參考。 如需其他**azdata**命令的詳細資訊, 請參閱[azdata 參考](reference-azdata.md)。

## <a name="commands"></a>命令
|     |     |
| --- | --- |
[azdata sql shell](#azdata-sql-shell) | SQL DB CLI 可讓使用者透過 T-sql 與 SQL Server 進行互動。
[azdata SQL 查詢](#azdata-sql-query) | 查詢命令允許執行 T-SQL 查詢。
## <a name="azdata-sql-shell"></a>azdata sql shell
SQL DB CLI 可讓使用者透過 T-sql 與 SQL Server 進行互動。
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
增加記錄詳細資訊, 以顯示所有的調試記錄。
#### `--help -h`
顯示此說明訊息並結束。
#### `--output -o`
輸出格式。  允許的值: json、jsonc、table、tsv。  預設值: json。
#### `--query -q`
JMESPath 查詢字串。 如[http://jmespath.org/](http://jmespath.org/])需詳細資訊和範例, 請參閱。
#### `--verbose`
增加記錄詳細資訊。 使用--debug 取得完整的 debug 記錄檔。
## <a name="azdata-sql-query"></a>azdata SQL 查詢
查詢命令允許執行 T-SQL 查詢。
```bash
azdata sql query --database -d 
                 -q
```
### <a name="examples"></a>範例
選取資料表名稱的清單。  資料庫預設為 master。
```bash
azdata sql query 'SELECT name FROM SYS.TABLES'
```
### <a name="required-parameters"></a>必要參數
#### `--database -d`
要在其中執行查詢的資料庫。  預設值為 master。
#### `-q`
要執行的 t-SQL 查詢。
### <a name="global-arguments"></a>全域引數
#### `--debug`
增加記錄詳細資訊, 以顯示所有的調試記錄。
#### `--help -h`
顯示此說明訊息並結束。
#### `--output -o`
輸出格式。  允許的值: json、jsonc、table、tsv。  預設值: json。
#### `--query -q`
JMESPath 查詢字串。 如[http://jmespath.org/](http://jmespath.org/])需詳細資訊和範例, 請參閱。
#### `--verbose`
增加記錄詳細資訊。 使用--debug 取得完整的 debug 記錄檔。

## <a name="next-steps"></a>後續步驟

如需有關如何安裝**azdata**工具的詳細資訊, 請參閱[install azdata to manage SQL Server 2019 big data](deploy-install-azdata.md)叢集。
