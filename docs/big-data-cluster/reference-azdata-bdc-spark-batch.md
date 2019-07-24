---
title: azdata bdc spark 批次參考
titleSuffix: SQL Server big data clusters
description: Azdata bdc spark 批次命令的參考文章。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 6e242b26f439b49dbf0b3cf5ab50ea46c273f45f
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/23/2019
ms.locfileid: "68426158"
---
# <a name="azdata-bdc-spark-batch"></a>azdata bdc spark 批次

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

下列文章提供**azdata**工具中**bdc spark 批次**命令的參考。 如需其他**azdata**命令的詳細資訊, 請參閱[azdata 參考](reference-azdata.md)

## <a name="commands"></a>命令
|     |     |
| --- | --- |
[azdata bdc spark 批次建立](#azdata-bdc-spark-batch-create) | 建立新的 Spark 批次。
[azdata bdc spark 批次清單](#azdata-bdc-spark-batch-list) | 列出 Spark 中的所有批次。
[azdata bdc spark 批次資訊](#azdata-bdc-spark-batch-info) | 取得 active Spark 批次的相關資訊。
[azdata bdc spark 批次記錄檔](#azdata-bdc-spark-batch-log) | 取得 Spark 批次的執行記錄。
[azdata bdc spark 批次狀態](#azdata-bdc-spark-batch-state) | 取得 Spark 批次的執行狀態。
[azdata bdc spark 批次刪除](#azdata-bdc-spark-batch-delete) | 刪除 Spark 批次。
## <a name="azdata-bdc-spark-batch-create"></a>azdata bdc spark 批次建立
這會建立新的 batch Spark 作業, 以執行提供的程式碼。
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
傳遞一個或多個 jar 檔案時所要執行的類別名稱。
#### `--arguments -a`
引數清單。  若要傳入清單, JSON 會將值編碼。  範例: ' ["entry1", "entry2"] '。
#### `--jar-files -j`
Jar 檔案路徑的清單。  若要傳入清單, JSON 會將值編碼。  範例: ' ["entry1", "entry2"] '。
#### `--py-files -p`
Python 檔案路徑的清單。  若要傳入清單, JSON 會將值編碼。  範例: ' ["entry1", "entry2"] '。
#### `--files`
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
#### `--archives`
封存路徑的清單。  若要傳入清單, JSON 會將值編碼。  範例: ' ["entry1", "entry2"] '。
#### `--queue -q`
要在其中執行會話之 Spark 佇列的名稱。
#### `--name -n`
Spark 會話的名稱。
#### `--config`
包含 Spark 設定值的名稱值組清單。  已編碼為 JSON 字典。  範例: ' {"name": "value", "name2": "value2"} '。
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
## <a name="azdata-bdc-spark-batch-list"></a>azdata bdc spark 批次清單
列出 Spark 中的所有批次。
```bash
azdata bdc spark batch list 
```
### <a name="examples"></a>範例
列出所有作用中的批次。
```bash
azdata spark batch list
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
## <a name="azdata-bdc-spark-batch-info"></a>azdata bdc spark 批次資訊
這會取得具有指定識別碼之 Spark 批次的資訊。  批次識別碼會從「spark 批次建立」傳回。
```bash
azdata bdc spark batch info --batch-id -i 
                            
```
### <a name="examples"></a>範例
取得識別碼為0的批次的批次資訊。
```bash
azdata spark batch info --batch-id 0
```
### <a name="required-parameters"></a>必要參數
#### `--batch-id -i`
Spark 批次識別碼。
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
## <a name="azdata-bdc-spark-batch-log"></a>azdata bdc spark 批次記錄檔
這會取得具有指定識別碼之 Spark 批次的批次記錄專案。  批次識別碼會從「spark 批次建立」傳回。
```bash
azdata bdc spark batch log --batch-id -i 
                           
```
### <a name="examples"></a>範例
取得識別碼為0之批次的批次記錄檔。
```bash
azdata spark batch log --batch-id 0
```
### <a name="required-parameters"></a>必要參數
#### `--batch-id -i`
Spark 批次識別碼。
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
## <a name="azdata-bdc-spark-batch-state"></a>azdata bdc spark 批次狀態
這會取得具有指定識別碼之 Spark 批次的批次狀態。  批次識別碼會從「spark 批次建立」傳回。
```bash
azdata bdc spark batch state --batch-id -i 
                             
```
### <a name="examples"></a>範例
取得識別碼為0之批次的批次狀態。
```bash
azdata spark batch state --batch-id 0
```
### <a name="required-parameters"></a>必要參數
#### `--batch-id -i`
Spark 批次識別碼。
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
## <a name="azdata-bdc-spark-batch-delete"></a>azdata bdc spark 批次刪除
這會刪除 Spark 批次。 批次識別碼會從「spark 批次建立」傳回。
```bash
azdata bdc spark batch delete --batch-id -i 
                              
```
### <a name="examples"></a>範例
刪除批次。
```bash
azdata spark batch delete --batch-id 0
```
### <a name="required-parameters"></a>必要參數
#### `--batch-id -i`
Spark 批次識別碼。
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
