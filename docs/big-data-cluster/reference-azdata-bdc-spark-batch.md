---
title: azdata bdc spark batch 參考
titleSuffix: SQL Server big data clusters
description: azdata bdc spark batch 命令的參考文章。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 11/04/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: fc3dc5a987ae55ba410ca64c15a3a4b776465b54
ms.sourcegitcommit: 830149bdd6419b2299aec3f60d59e80ce4f3eb80
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/04/2019
ms.locfileid: "73531764"
---
# <a name="azdata-bdc-spark-batch"></a>azdata bdc spark batch

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]  

下列文章提供 `azdata` 工具中 `sql` 命令的參考。 如需其他 `azdata` 命令的詳細資訊，請參閱 [azdata 參考](reference-azdata.md)

## <a name="commands"></a>命令
|     |     |
| --- | --- |
[azdata bdc spark batch create](#azdata-bdc-spark-batch-create) | 建立新的 Spark 批次。
[azdata bdc spark batch list](#azdata-bdc-spark-batch-list) | 列出 Spark 中的所有批次。
[azdata bdc spark batch info](#azdata-bdc-spark-batch-info) | 取得作用中 Spark 批次的相關資訊。
[azdata bdc spark batch log](#azdata-bdc-spark-batch-log) | 取得 Spark 批次的執行記錄。
[azdata bdc spark batch state](#azdata-bdc-spark-batch-state) | 取得 Spark 批次的執行狀態。
[azdata bdc spark batch delete](#azdata-bdc-spark-batch-delete) | 刪除 Spark 批次。
## <a name="azdata-bdc-spark-batch-create"></a>azdata bdc spark batch create
這會建立新的批次 Spark 作業，其能執行所提供的程式碼。
```bash
azdata bdc spark batch create --file -f 
                              [--class-name -c]  
                              [--arguments -a]  
                              [--jar-files -j]  
                              [--py-files -p]  
                              [--files]  
                              [--driver-memory]  
                              [--driver-cores]  
                              [--executor-memory]  
                              [--executor-cores]  
                              [--executor-count]  
                              [--archives]  
                              [--queue -q]  
                              [--name -n]  
                              [--config]
```
### <a name="examples"></a>範例
建立新的 Spark 批次。
```bash
azdata spark batch create --code "2+2"
```
### <a name="required-parameters"></a>必要參數
#### `--file -f`
要執行之檔案的路徑。
### <a name="optional-parameters"></a>選擇性參數
#### `--class-name -c`
在傳入一或多個 jar 檔案時要執行之類別的名稱。
#### `--arguments -a`
引數的清單。  為了傳入清單，JSON 會將值編碼。  範例：'["entry1", "entry2"]'。
#### `--jar-files -j`
jar 檔案路徑的清單。  為了傳入清單，JSON 會將值編碼。  範例：'["entry1", "entry2"]'。
#### `--py-files -p`
Python 檔案路徑的清單。  為了傳入清單，JSON 會將值編碼。  範例：'["entry1", "entry2"]'。
#### `--files`
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
#### `--archives`
封存路徑的清單。  為了傳入清單，JSON 會將值編碼。  範例：'["entry1", "entry2"]'。
#### `--queue -q`
要執行工作階段所在之 Spark 佇列的名稱。
#### `--name -n`
Spark 工作階段的名稱。
#### `--config`
包含 Spark 設定值之名稱值組的清單。  編碼為 JSON 字典。  範例：'{"name":"value", "name2":"value2"}'。
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
## <a name="azdata-bdc-spark-batch-list"></a>azdata bdc spark batch list
列出 Spark 中的所有批次。
```bash
azdata bdc spark batch list 
```
### <a name="examples"></a>範例
列出所有作用中批次。
```bash
azdata spark batch list
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
## <a name="azdata-bdc-spark-batch-info"></a>azdata bdc spark batch info
這會取得具有指定識別碼之 Spark 批次的相關資訊。  批次識別碼會從 'spark batch create' 傳回。
```bash
azdata bdc spark batch info --batch-id -i 
          ```
### Examples
Get batch info for batch with ID of 0.
```bash
azdata spark batch info --batch-id 0
```
### <a name="required-parameters"></a>必要參數
#### `--batch-id -i`
Spark 批次識別碼號碼。
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
## <a name="azdata-bdc-spark-batch-log"></a>azdata bdc spark batch log
這會取得具有指定識別碼之 Spark 批次的批次記錄項目。  批次識別碼會從 'spark batch create' 傳回。
```bash
azdata bdc spark batch log --batch-id -i 
         ```
### Examples
Get batch log for batch with ID of 0.
```bash
azdata spark batch log --batch-id 0
```
### <a name="required-parameters"></a>必要參數
#### `--batch-id -i`
Spark 批次識別碼號碼。
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
## <a name="azdata-bdc-spark-batch-state"></a>azdata bdc spark batch state
這會取得具有指定識別碼之 Spark 批次的批次狀態。  批次識別碼會從 'spark batch create' 傳回。
```bash
azdata bdc spark batch state --batch-id -i 
           ```
### Examples
Get batch state for batch with ID of 0.
```bash
azdata spark batch state --batch-id 0
```
### <a name="required-parameters"></a>必要參數
#### `--batch-id -i`
Spark 批次識別碼號碼。
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
## <a name="azdata-bdc-spark-batch-delete"></a>azdata bdc spark batch delete
這會刪除 Spark 批次。 批次識別碼會從 'spark batch create' 傳回。
```bash
azdata bdc spark batch delete --batch-id -i 
            ```
### Examples
Delete a batch.
```bash
azdata spark batch delete --batch-id 0
```
### <a name="required-parameters"></a>必要參數
#### `--batch-id -i`
Spark 批次識別碼號碼。
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

如需其他 `azdata` 命令的詳細資訊，請參閱 [azdata 參考](reference-azdata.md)。 如需如何安裝 `azdata` 工具的詳細資訊，請參閱[安裝 azdata 管理 SQL Server 2019 巨量資料叢集](deploy-install-azdata.md)。
