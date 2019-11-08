---
title: azdata bdc spark session 參考
titleSuffix: SQL Server big data clusters
description: azdata bdc spark session 命令的參考文章。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 11/04/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: f1da72349e7594d267ae0d965ddad03cee93017b
ms.sourcegitcommit: 830149bdd6419b2299aec3f60d59e80ce4f3eb80
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/04/2019
ms.locfileid: "73531737"
---
# <a name="azdata-bdc-spark-session"></a>azdata bdc spark session

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]  

下文提供 `azdata` 工具中 `sql` 命令的參考。 如需其他 `azdata` 命令的詳細資訊，請參閱 [azdata 參考](reference-azdata.md)

## <a name="commands"></a>命令
|     |     |
| --- | --- |
[azdata bdc spark session create](#azdata-bdc-spark-session-create) | 建立新的 Spark 工作階段。
[azdata bdc spark session list](#azdata-bdc-spark-session-list) | 列出 Spark 中所有作用中的工作階段。
[azdata bdc spark session info](#azdata-bdc-spark-session-info) | 取得作用中 Spark 工作階段的相關資訊。
[azdata bdc spark session log](#azdata-bdc-spark-session-log) | 取得作用中 Spark 工作階段的執行記錄。
[azdata bdc spark session state](#azdata-bdc-spark-session-state) | 取得作用中 Spark 工作階段的執行狀態。
[azdata bdc spark session delete](#azdata-bdc-spark-session-delete) | 刪除 Spark 工作階段。
## <a name="azdata-bdc-spark-session-create"></a>azdata bdc spark session create
這會建立新的互動式 Spark 工作階段。 呼叫者必須指定 Spark 工作階段的類型。 此工作階段的存留期會超過 azdata 執行的存留期，且必須使用 'spark session delete' 刪除
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
建立工作階段。
```bash
azdata spark session create --session-kind pyspark
```
### <a name="optional-parameters"></a>選擇性參數
#### `--session-kind -k`
要建立之工作階段類型的名稱。  spark、pyspark、sparkr 或 sql 其中之一。
#### `--jar-files -j`
jar 檔案路徑的清單。  為了傳入清單，JSON 會將值編碼。  範例：'["entry1", "entry2"]'。
#### `--py-files -p`
Python 檔案路徑的清單。  為了傳入清單，JSON 會將值編碼。  範例：'["entry1", "entry2"]'。
#### `--files -f`
檔案路徑的清單。  為了傳入清單，JSON 會將值編碼。  範例：'["entry1", "entry2"]'。
#### `--driver-memory`
要配置給驅動程式的記憶體數量。  將單位指定為值的一部分。  範例：512M 或 2G。
#### `--driver-cores`
要配置給驅動程式的 CPU 核心數量。
#### `--executor-memory`
要配置給執行程式的記憶體數量。  將單位指定為值的一部分。  範例：512M 或 2G。
#### `--executor-cores`
要配置給執行程式的 CPU 核心數量。
#### `--executor-count`
要執行之執行程式的執行個體數目。
#### `--archives -a`
封存路徑的清單。  為了傳入清單，JSON 會將值編碼。  範例：'["entry1", "entry2"]'。
#### `--queue -q`
要執行工作階段所在之 Spark 佇列的名稱。
#### `--name -n`
Spark 工作階段的名稱。
#### `--config -c`
包含 Spark 設定值之名稱值組的清單。  編碼為 JSON 字典。  範例：'{"name":"value", "name2":"value2"}'。
#### `--timeout-seconds -t`
以秒為單位的工作階段閒置逾時。
### <a name="global-arguments"></a>全域引數
#### `--debug`
增加記錄詳細資訊，以顯示所有偵錯記錄。
#### `--help -h`
顯示此說明訊息並結束。
#### `--output -o`
輸出格式。  允許的值：json、jsonc、table、tsv。  預設值：json。
#### `--query -q`
JMESPath 查詢字串。 如需詳細資訊和範例，請參閱 [http://jmespath.org/](http://jmespath.org/)。
#### `--verbose`
增加記錄詳細資訊。 使用 --debug 來取得完整偵錯記錄。
## <a name="azdata-bdc-spark-session-list"></a>azdata bdc spark session list
列出 Spark 中所有作用中的工作階段。
```bash
azdata bdc spark session list 
```
### <a name="examples"></a>範例
列出所有作用中的工作階段。
```bash
azdata spark session list
```
### <a name="global-arguments"></a>全域引數
#### `--debug`
增加記錄詳細資訊，以顯示所有偵錯記錄。
#### `--help -h`
顯示此說明訊息並結束。
#### `--output -o`
輸出格式。  允許的值：json、jsonc、table、tsv。  預設值：json。
#### `--query -q`
JMESPath 查詢字串。 如需詳細資訊和範例，請參閱 [http://jmespath.org/](http://jmespath.org/)。
#### `--verbose`
增加記錄詳細資訊。 使用 --debug 來取得完整偵錯記錄。
## <a name="azdata-bdc-spark-session-info"></a>azdata bdc spark session info
這會取得具有指定識別碼的作用中 Spark 工作階段的工作階段資訊。  工作階段識別碼會從 'spark session create' 傳回。
```bash
azdata bdc spark session info --session-id -i 
            ```
### Examples
Get session info for session with ID of 0.
```bash
azdata spark session info --session-id 0
```
### <a name="required-parameters"></a>必要參數
#### `--session-id -i`
Spark 工作階段識別碼。
### <a name="global-arguments"></a>全域引數
#### `--debug`
增加記錄詳細資訊，以顯示所有偵錯記錄。
#### `--help -h`
顯示此說明訊息並結束。
#### `--output -o`
輸出格式。  允許的值：json、jsonc、table、tsv。  預設值：json。
#### `--query -q`
JMESPath 查詢字串。 如需詳細資訊和範例，請參閱 [http://jmespath.org/](http://jmespath.org/)。
#### `--verbose`
增加記錄詳細資訊。 使用 --debug 來取得完整偵錯記錄。
## <a name="azdata-bdc-spark-session-log"></a>azdata bdc spark session log
這會取得具有指定識別碼的作用中 Spark 工作階段的工作階段記錄項目。  工作階段識別碼會從 'spark session create' 傳回。
```bash
azdata bdc spark session log --session-id -i 
           ```
### Examples
Get session log for session with ID of 0.
```bash
azdata spark session log --session-id 0
```
### <a name="required-parameters"></a>必要參數
#### `--session-id -i`
Spark 工作階段識別碼。
### <a name="global-arguments"></a>全域引數
#### `--debug`
增加記錄詳細資訊，以顯示所有偵錯記錄。
#### `--help -h`
顯示此說明訊息並結束。
#### `--output -o`
輸出格式。  允許的值：json、jsonc、table、tsv。  預設值：json。
#### `--query -q`
JMESPath 查詢字串。 如需詳細資訊和範例，請參閱 [http://jmespath.org/](http://jmespath.org/)。
#### `--verbose`
增加記錄詳細資訊。 使用 --debug 來取得完整偵錯記錄。
## <a name="azdata-bdc-spark-session-state"></a>azdata bdc spark session state
這會取得具有指定識別碼的作用中 Spark 工作階段的工作階段狀態。  工作階段識別碼會從 'spark session create' 傳回。
```bash
azdata bdc spark session state --session-id -i 
             ```
### Examples
Get session state for session with ID of 0.
```bash
azdata spark session state --session-id 0
```
### <a name="required-parameters"></a>必要參數
#### `--session-id -i`
Spark 工作階段識別碼。
### <a name="global-arguments"></a>全域引數
#### `--debug`
增加記錄詳細資訊，以顯示所有偵錯記錄。
#### `--help -h`
顯示此說明訊息並結束。
#### `--output -o`
輸出格式。  允許的值：json、jsonc、table、tsv。  預設值：json。
#### `--query -q`
JMESPath 查詢字串。 如需詳細資訊和範例，請參閱 [http://jmespath.org/](http://jmespath.org/)。
#### `--verbose`
增加記錄詳細資訊。 使用 --debug 來取得完整偵錯記錄。
## <a name="azdata-bdc-spark-session-delete"></a>azdata bdc spark session delete
這會刪除互動式 Spark 工作階段。 工作階段識別碼會從 'spark session create' 傳回。
```bash
azdata bdc spark session delete --session-id -i 
              ```
### Examples
Delete a session.
```bash
azdata spark session delete --session-id 0
```
### <a name="required-parameters"></a>必要參數
#### `--session-id -i`
Spark 工作階段識別碼。
### <a name="global-arguments"></a>全域引數
#### `--debug`
增加記錄詳細資訊，以顯示所有偵錯記錄。
#### `--help -h`
顯示此說明訊息並結束。
#### `--output -o`
輸出格式。  允許的值：json、jsonc、table、tsv。  預設值：json。
#### `--query -q`
JMESPath 查詢字串。 如需詳細資訊和範例，請參閱 [http://jmespath.org/](http://jmespath.org/)。
#### `--verbose`
增加記錄詳細資訊。 使用 --debug 來取得完整偵錯記錄。

## <a name="next-steps"></a>後續步驟

如需其他 `azdata` 命令的詳細資訊，請參閱 [azdata 參考](reference-azdata.md)。 如需如何安裝 `azdata` 工具的詳細資訊，請參閱[安裝 azdata 來管理 SQL Server 2019 巨量資料叢集](deploy-install-azdata.md)。
