---
title: azdata bdc hdfs 掛接參考
titleSuffix: SQL Server big data clusters
description: Azdata bdc hdfs 掛接命令的參考文章。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 7f0b259a3ac4ac0850fa05de3867e928b035307b
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/23/2019
ms.locfileid: "68426268"
---
# <a name="azdata-bdc-hdfs-mount"></a>azdata bdc hdfs 掛接

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

下列文章提供**azdata**工具中**bdc hdfs 掛接**命令的參考。 如需其他**azdata**命令的詳細資訊, 請參閱[azdata 參考](reference-azdata.md)。

## <a name="commands"></a>命令
|     |     |
| --- | --- |
[azdata bdc hdfs 掛接建立](#azdata-bdc-hdfs-mount-create) | 在 HDFS 中建立遠端存放區的裝載。
[azdata bdc hdfs 掛接刪除](#azdata-bdc-hdfs-mount-delete) | 刪除 HDFS 中的遠端存放區裝載。
[azdata bdc hdfs 掛接狀態](#azdata-bdc-hdfs-mount-status) | 掛接的狀態。
[azdata bdc hdfs 掛接重新整理](#azdata-bdc-hdfs-mount-refresh) | 重新整理 HDFS 中的掛接內容。
## <a name="azdata-bdc-hdfs-mount-create"></a>azdata bdc hdfs 掛接建立
在 HDFS 中建立遠端存放區的裝載。 存取遠端存放的認證 (如果有的話) 應使用環境變數 MOUNT_CREDENTIALS 來指定, 以逗號分隔的索引鍵 = 值組清單。 索引鍵或值中的任何逗號都必須經過轉義。
```bash
azdata bdc hdfs mount create --remote-uri -r 
                             --mount-path -m
```
### <a name="examples"></a>範例
若要使用共用金鑰在 HDFS 路徑/mounts/adlsv2/data 上掛接 ADLS Gen 2 帳戶 "adlsv2example" 中的容器 "data"
```bash
Set the MOUNT_CREDENTIALS environment variable as "fs.azure.abfs.account.name=<your-storage-account-name>.dfs.core.windows.net,fs.azure.account.key.<your-storage-account-name>.dfs.core.windows.net=<storage-account-access-key>".
azdata bdc hdfs mount create --remote-uri abfs://data@adlsv2example.dfs.core.windows.net/
    --mount-path /mounts/adlsv2/data
```
在本機 HDFS 路徑/mounts/hdfs/上掛接遠端 HDFS BDC (hdfs://namenode1:8080/)
```bash
azdata bdc hdfs mount create --remote-uri hdfs://namenode1:8080/ --mount-path /mounts/hdfs/
```
### <a name="required-parameters"></a>必要參數
#### `--remote-uri -r`
要裝載之遠端存放區的 URI (裝載的來源)。
#### `--mount-path -m`
必須建立掛接的 HDFS 路徑 (掛接的目的地)。
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
## <a name="azdata-bdc-hdfs-mount-delete"></a>azdata bdc hdfs 掛接刪除
刪除 HDFS 中的遠端存放區裝載。
```bash
azdata bdc hdfs mount delete --mount-path -m 
                             
```
### <a name="examples"></a>範例
針對 ADLS Gen 2 儲存體帳戶, 刪除在/mounts/adlsv2/data 上建立的掛接。
```bash
azdata bdc hdfs mount delete --mount-path /mounts/adlsv2/data
```
### <a name="required-parameters"></a>必要參數
#### `--mount-path -m`
對應至必須刪除之掛接的 HDFS 路徑。
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
## <a name="azdata-bdc-hdfs-mount-status"></a>azdata bdc hdfs 掛接狀態
掛接的狀態。
```bash
azdata bdc hdfs mount status [--mount-path -m] 
                             
```
### <a name="examples"></a>範例
依路徑取得掛接狀態
```bash
azdata bdc hdfs mount status --mount-path /mounts/hdfs
```
取得所有裝載的狀態。
```bash
azdata bdc hdfs mount status
```
### <a name="optional-parameters"></a>選擇性參數
#### `--mount-path -m`
掛接路徑。
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
## <a name="azdata-bdc-hdfs-mount-refresh"></a>azdata bdc hdfs 掛接重新整理
重新整理 HDFS 中的掛接內容。
```bash
azdata bdc hdfs mount refresh --mount-path -m 
                              
```
### <a name="examples"></a>範例
重新整理在/mounts/adlsv2/data. 建立的掛接
```bash
azdata bdc hdfs mount refresh --mount-path /mounts/adlsv2/data
```
### <a name="required-parameters"></a>必要參數
#### `--mount-path -m`
對應至必須重新整理之掛接的 HDFS 路徑。
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
