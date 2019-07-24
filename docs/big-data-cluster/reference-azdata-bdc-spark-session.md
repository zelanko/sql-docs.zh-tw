---
title: azdata bdc spark 會話參考
titleSuffix: SQL Server big data clusters
description: Azdata bdc spark 會話命令的參考文章。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 20b7ac3dcf72482e80278ce0f0df922026232a6d
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/23/2019
ms.locfileid: "68426098"
---
# <a name="azdata-bdc-spark-session"></a>azdata bdc spark 會話

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)] 

下列文章提供**azdata**工具中**bdc spark 會話**命令的參考。 如需其他**azdata**命令的詳細資訊, 請參閱[azdata 參考](reference-azdata.md)

## <a name="commands"></a>命令
|     |     |
| --- | --- |
[azdata bdc spark 會話建立](#azdata-bdc-spark-session-create) | 建立新的 Spark 會話。
[azdata bdc spark 會話清單](#azdata-bdc-spark-session-list) | 列出 Spark 中所有作用中的會話。
[azdata bdc spark 會話資訊](#azdata-bdc-spark-session-info) | 取得作用中 Spark 會話的相關資訊。
[azdata bdc spark 會話記錄檔](#azdata-bdc-spark-session-log) | 取得作用中 Spark 會話的執行記錄。
[azdata bdc spark 會話狀態](#azdata-bdc-spark-session-state) | 取得作用中 Spark 會話的執行狀態。
[azdata bdc spark 會話刪除](#azdata-bdc-spark-session-delete) | 刪除 Spark 會話。
## <a name="azdata-bdc-spark-session-create"></a>azdata bdc spark 會話建立
這會建立新的互動式 Spark 會話。 呼叫端必須指定 Spark 會話的類型。 此會話不在 azdata 執行的存留期間內, 必須使用 [spark 會話刪除] 加以刪除
```bash
azdata bdc spark session create [--session-kind -k] 
                                [--jar-files -j]  
                                [--py-files -p]  
                                [--files -f]  
                                [--driver-memory]  
                                [--driver-cores]  
                                [--executor-memory]  
                                [--executor-cores]  
                                [--executor-count]  
                                [--archives -a]  
                                [--queue -q]  
                                [--name -n]  
                                [--config -c]  
                                [--timeout-seconds -t]
```
### <a name="examples"></a>範例
建立會話。
```bash
azdata spark session create --session-kind pyspark
```
### <a name="optional-parameters"></a>選擇性參數
#### `--session-kind -k`
要建立的會話類型名稱。  Spark、pyspark、sparkr 或 sql 其中之一。
#### `--jar-files -j`
Jar 檔案路徑的清單。  若要傳入清單, JSON 會將值編碼。  範例: ' ["entry1", "entry2"] '。
#### `--py-files -p`
Python 檔案路徑的清單。  若要傳入清單, JSON 會將值編碼。  範例: ' ["entry1", "entry2"] '。
#### `--files -f`
檔案路徑的清單。  若要傳入清單, JSON 會將值編碼。  範例: ' ["entry1", "entry2"] '。
#### `--driver-memory`
要配置給驅動程式的記憶體數量。  將 [單位] 指定為 [值] 的一部分。  範例512M 或2G。
#### `--driver-cores`
要配置給驅動程式的 CPU 核心數量。
#### `--executor-memory`
要配置給執行程式的記憶體數量。  將 [單位] 指定為 [值] 的一部分。  範例512M 或2G。
#### `--executor-cores`
要配置給執行程式的 CPU 核心數量。
#### `--executor-count`
要執行之執行程式的實例數目。
#### `--archives -a`
封存路徑的清單。  若要傳入清單, JSON 會將值編碼。  範例: ' ["entry1", "entry2"] '。
#### `--queue -q`
要在其中執行會話之 Spark 佇列的名稱。
#### `--name -n`
Spark 會話的名稱。
#### `--config -c`
包含 Spark 設定值的名稱值組清單。  已編碼為 JSON 字典。  範例: ' {"name": "value", "name2": "value2"} '。
#### `--timeout-seconds -t`
會話閒置時間 (秒)。
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
## <a name="azdata-bdc-spark-session-list"></a>azdata bdc spark 會話清單
列出 Spark 中所有作用中的會話。
```bash
azdata bdc spark session list 
```
### <a name="examples"></a>範例
列出所有作用中的會話。
```bash
azdata spark session list
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
## <a name="azdata-bdc-spark-session-info"></a>azdata bdc spark 會話資訊
這會取得具有指定識別碼之作用中 Spark 會話的會話資訊。  會話識別碼會從「spark 會話建立」傳回。
```bash
azdata bdc spark session info --session-id -i 
                              
```
### <a name="examples"></a>範例
取得識別碼為0之會話的會話資訊。
```bash
azdata spark session info --session-id 0
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
## <a name="azdata-bdc-spark-session-log"></a>azdata bdc spark 會話記錄檔
這會取得具有指定識別碼之作用中 Spark 會話的會話記錄專案。  會話識別碼會從「spark 會話建立」傳回。
```bash
azdata bdc spark session log --session-id -i 
                             
```
### <a name="examples"></a>範例
取得識別碼為0之會話的會話記錄檔。
```bash
azdata spark session log --session-id 0
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
## <a name="azdata-bdc-spark-session-state"></a>azdata bdc spark 會話狀態
這會取得具有指定識別碼之作用中 Spark 會話的會話狀態。  會話識別碼會從「spark 會話建立」傳回。
```bash
azdata bdc spark session state --session-id -i 
                               
```
### <a name="examples"></a>範例
取得識別碼為0之會話的會話狀態。
```bash
azdata spark session state --session-id 0
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
## <a name="azdata-bdc-spark-session-delete"></a>azdata bdc spark 會話刪除
這會刪除互動式 Spark 會話。 會話識別碼會從「spark 會話建立」傳回。
```bash
azdata bdc spark session delete --session-id -i 
                                
```
### <a name="examples"></a>範例
刪除會話。
```bash
azdata spark session delete --session-id 0
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

## <a name="next-steps"></a>後續步驟

如需其他**azdata**命令的詳細資訊, 請參閱[azdata 參考](reference-azdata.md)。 如需有關如何安裝**azdata**工具的詳細資訊, 請參閱[install azdata to manage SQL Server 2019 big data](deploy-install-azdata.md)叢集。
