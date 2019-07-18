---
title: mssqlctl bdc 存放集區掛接參考
titleSuffix: SQL Server big data clusters
description: Mssqlctl bdc 存放集區的掛接命令的參考文件。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 06/26/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: b6a412c6d7cab9fb869a9aa8ee1b62ae0ed3f717
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67958007"
---
# <a name="mssqlctl-bdc-storage-pool-mount"></a>mssqlctl bdc 存放集區的掛接

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

下列文章提供的參考**bdc 存放集區掛接**中的命令**mssqlctl**工具。 如需其他詳細資訊**mssqlctl**命令，請參閱[mssqlctl 參考](reference-mssqlctl.md)。

## <a name="commands"></a>命令
|     |     |
| --- | --- |
[建立 mssqlctl bdc 存放集區的掛接](#mssqlctl-bdc-storage-pool-mount-create) | 在 HDFS 中的遠端存放區的掛接。
[mssqlctl bdc 存放集區掛接 delete](#mssqlctl-bdc-storage-pool-mount-delete) | 刪除掛接在 HDFS 中的遠端存放區。
[mssqlctl bdc 存放集區掛接狀態](#mssqlctl-bdc-storage-pool-mount-status) | Mount(s) 的狀態。
## <a name="mssqlctl-bdc-storage-pool-mount-create"></a>建立 mssqlctl bdc 存放集區的掛接
在 HDFS 中的遠端存放區的掛接。 應指定的認證來存取遠端存放區中，如果有的話，使用環境變數 MOUNT_CREDENTIALS 為逗號分隔清單的索引鍵 = 值 」 配對。 必須逸出任何索引鍵或值的逗號。
```bash
mssqlctl bdc storage-pool mount create --remote-uri 
                                       --mount-path
```
### <a name="examples"></a>範例
若要使用的共用的金鑰的 HDFS 路徑 /mounts/adlsv2/data 上裝載容器 「 資料 」 在第 2 代 ADLS 帳戶 」 adlsv2example"
```bash
Set the MOUNT_CREDENTIALS environment variable as "fs.azure.abfs.account.name=<your-storage-account-name>.dfs.core.windows.net,fs.azure.account.key.<your-storage-account-name>.dfs.core.windows.net=<storage-account-access-key>".
mssqlctl bdc storage-pool mount create --remote-uri abfs://data@adlsv2example.dfs.core.windows.net/
    --mount-path /mounts/adlsv2/data
```
若要裝載遠端 HDFS BDC (hdfs://namenode1:8080 /) 上本機 HDFS 路徑 /mounts hdfs /
```bash
mssqlctl bdc storage-pool mount create --remote-uri hdfs://namenode1:8080/ --mount-path /mounts/hdfs/
```
### <a name="required-parameters"></a>必要參數
#### `--remote-uri`
要掛接 （來源掛接） 的遠端存放區的 URI。
#### `--mount-path`
HDFS 路徑掛上對建立 （掛上的目的地）。
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
## <a name="mssqlctl-bdc-storage-pool-mount-delete"></a>mssqlctl bdc 存放集區掛接 delete
刪除掛接在 HDFS 中的遠端存放區。
```bash
mssqlctl bdc storage-pool mount delete --mount-path 
                                       
```
### <a name="examples"></a>範例
刪除掛接端建立 /mounts/adlsv2/data 第 2 代 ADLS 儲存體帳戶。
```bash
mssqlctl bdc storage-pool mount delete --mount-path /mounts/adlsv2/data
```
### <a name="required-parameters"></a>必要參數
#### `--mount-path`
對應至掛接的 HDFS 路徑的已遭刪除。
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
## <a name="mssqlctl-bdc-storage-pool-mount-status"></a>mssqlctl bdc 存放集區掛接狀態
Mount(s) 的狀態。
```bash
mssqlctl bdc storage-pool mount status [--mount-path] 
                                       
```
### <a name="examples"></a>範例
取得以路徑掛接狀態
```bash
mssqlctl bdc storage-pool mount status --mount-path /mounts/hdfs
```
取得所有掛接的狀態。
```bash
mssqlctl bdc storage-pool mount status
```
### <a name="optional-parameters"></a>選擇性參數
#### `--mount-path`
掛接路徑。
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

如需其他詳細資訊**mssqlctl**命令，請參閱[mssqlctl 參考](reference-mssqlctl.md)。 如需有關如何安裝**mssqlctl**工具，請參閱[安裝來管理 SQL Server 2019 巨量資料叢集 mssqlctl](deploy-install-mssqlctl.md)。