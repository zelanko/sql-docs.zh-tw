---
title: mssqlctl sql 參考
titleSuffix: SQL Server big data clusters
description: Mssqlctl sql 命令的參考文件。
author: rothja
ms.author: jroth
manager: jroth
ms.date: 06/26/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 536d4712a6ccb288ca60c038a37e99c2be8a5eba
ms.sourcegitcommit: ce5770d8b91c18ba5ad031e1a96a657bde4cae55
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/25/2019
ms.locfileid: "67394200"
---
# <a name="mssqlctl-sql"></a>mssqlctl sql

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

下列文章提供的參考**sql**中的命令**mssqlctl**工具。 如需其他詳細資訊**mssqlctl**命令，請參閱[mssqlctl 參考](reference-mssqlctl.md)。

## <a name="commands"></a>命令
|     |     |
| --- | --- |
[mssqlctl sql shell](#mssqlctl-sql-shell) | SQL DB CLI 可讓使用者透過 T-SQL 的 SQL 伺服器互動。
[mssqlctl sql 查詢](#mssqlctl-sql-query) | 查詢命令可讓您執行 T-SQL 查詢。
## <a name="mssqlctl-sql-shell"></a>mssqlctl sql shell
SQL DB CLI 可讓使用者透過 T-SQL 的 SQL 伺服器互動。
```bash
mssqlctl sql shell 
```
### <a name="examples"></a>範例
若要啟動的互動式體驗的範例命令列。
```bash
mssqlctl sql shell
```
### <a name="global-arguments"></a>全域引數
#### `--debug`
增加記錄詳細程度以顯示所有偵錯記錄檔。
#### `--help -h`
顯示此說明訊息並結束。
#### `--output -o`
輸出格式。  允許的值： json、 jsonc、 table、 tsv。  預設值： json。
#### `--query -q`
JMESPath 查詢字串。 請參閱[ http://jmespath.org/ ](http://jmespath.org/])如需詳細資訊和範例。
#### `--verbose`
增加記錄詳細程度。 使用--debug 取得完整的偵錯記錄。
## <a name="mssqlctl-sql-query"></a>mssqlctl sql 查詢
查詢命令可讓您執行 T-SQL 查詢。
```bash
mssqlctl sql query --database -d 
                   -q
```
### <a name="examples"></a>範例
選取資料表名稱的清單。  Master 資料庫預設值。
```bash
mssqlctl sql query 'SELECT name FROM SYS.TABLES'
```
### <a name="required-parameters"></a>必要參數
#### `--database -d`
若要執行查詢的資料庫。  預設值為 master。
#### `-q`
要執行的 T-SQL 查詢。
### <a name="global-arguments"></a>全域引數
#### `--debug`
增加記錄詳細程度以顯示所有偵錯記錄檔。
#### `--help -h`
顯示此說明訊息並結束。
#### `--output -o`
輸出格式。  允許的值： json、 jsonc、 table、 tsv。  預設值： json。
#### `--query -q`
JMESPath 查詢字串。 請參閱[ http://jmespath.org/ ](http://jmespath.org/])如需詳細資訊和範例。
#### `--verbose`
增加記錄詳細程度。 使用--debug 取得完整的偵錯記錄。

## <a name="next-steps"></a>後續步驟

如需有關如何安裝**mssqlctl**工具，請參閱[安裝來管理 SQL Server 2019 巨量資料叢集 mssqlctl](deploy-install-mssqlctl.md)。