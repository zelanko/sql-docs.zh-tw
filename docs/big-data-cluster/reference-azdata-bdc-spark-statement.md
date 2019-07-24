---
title: azdata bdc spark 語句參考
titleSuffix: SQL Server big data clusters
description: Azdata bdc spark 語句命令的參考文章。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 778980ac6b93e7db79d59182fbd18ab4cfdb8b75
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/23/2019
ms.locfileid: "68426088"
---
# <a name="azdata-bdc-spark-statement"></a>azdata bdc spark 語句

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)] 

下列文章提供**azdata**工具中**bdc spark 語句**命令的參考。 如需其他**azdata**命令的詳細資訊, 請參閱[azdata 參考](reference-azdata.md)

## <a name="commands"></a>命令
|     |     |
| --- | --- |
[azdata bdc spark 語句清單](#azdata-bdc-spark-statement-list) | 列出給定 Spark 會話中的所有語句。
[azdata bdc spark 語句建立](#azdata-bdc-spark-statement-create) | 在給定的會話中建立新的 Spark 語句。
[azdata bdc spark 語句資訊](#azdata-bdc-spark-statement-info) | 取得給定 Spark 會話中所要求語句的相關資訊。
[azdata bdc spark 語句取消](#azdata-bdc-spark-statement-cancel) | 取消給定 Spark 會話中的語句。
## <a name="azdata-bdc-spark-statement-list"></a>azdata bdc spark 語句清單
列出給定 Spark 會話中的所有語句。
```bash
azdata bdc spark statement list --session-id -i 
                                
```
### <a name="examples"></a>範例
列出所有的 session 語句。
```bash
azdata spark statement list --session-id 0
```
### <a name="required-parameters"></a>必要參數
#### `--session-id -i`
Spark 會話識別碼。
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
## <a name="azdata-bdc-spark-statement-create"></a>azdata bdc spark 語句建立
這會在給定的會話中建立並執行新的語句。  如果執行快速, 則結果會包含執行的輸出。  否則, 在語句完成之後, 可以使用「spark 會話資訊」來抓取結果。
```bash
azdata bdc spark statement create --session-id -i 
                                  --code -c
```
### <a name="examples"></a>範例
執行語句。
```bash
azdata spark statement create --session-id 0 --code "2+2"
```
### <a name="required-parameters"></a>必要參數
#### `--session-id -i`
Spark 會話識別碼。
#### `--code -c`
字串, 包含要當做語句一部分執行的程式碼。
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
## <a name="azdata-bdc-spark-statement-info"></a>azdata bdc spark 語句資訊
這會在語句完成時, 取得執行狀態和執行結果。 語句識別碼會從 ' spark 語句 create ' 傳回。
```bash
azdata bdc spark statement info --session-id -i 
                                --statement-id -s
```
### <a name="examples"></a>範例
識別碼為0且語句識別碼為0之會話的 Get 語句資訊。
```bash
azdata spark statement info --session-id 0 --statement-id 0
```
### <a name="required-parameters"></a>必要參數
#### `--session-id -i`
Spark 會話識別碼。
#### `--statement-id -s`
指定會話識別碼內的 Spark 語句識別碼。
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
## <a name="azdata-bdc-spark-statement-cancel"></a>azdata bdc spark 語句取消
這會取消給定 Spark 會話中的語句。 語句識別碼會從 ' spark 語句 create ' 傳回。
```bash
azdata bdc spark statement cancel --session-id -i 
                                  --statement-id -s
```
### <a name="examples"></a>範例
取消語句。
```bash
azdata spark statement cancel --session-id 0 --statement-id 0
```
### <a name="required-parameters"></a>必要參數
#### `--session-id -i`
Spark 會話識別碼。
#### `--statement-id -s`
指定會話識別碼內的 Spark 語句識別碼。
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

如需其他**azdata**命令的詳細資訊, 請參閱[azdata 參考](reference-azdata.md)。 如需有關如何安裝**azdata**工具的詳細資訊, 請參閱[install azdata to manage SQL Server 2019 big data](deploy-install-azdata.md)叢集。
