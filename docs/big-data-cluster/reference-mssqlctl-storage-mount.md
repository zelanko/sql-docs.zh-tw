---
title: mssqlctl 儲存體掛接參考
titleSuffix: SQL Server big data clusters
description: Mssqlctl 儲存體掛接命令的參考文件。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 04/23/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 523253e8d1ff2d621d9f7a5ef90dbc957fba82ec
ms.sourcegitcommit: bd5f23f2f6b9074c317c88fc51567412f08142bb
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/24/2019
ms.locfileid: "63473491"
---
# <a name="mssqlctl-storage-mount"></a>mssqlctl storage mount

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

下列文章提供的參考**儲存體掛接**中的命令**mssqlctl**工具。 如需其他詳細資訊**mssqlctl**命令，請參閱[mssqlctl 參考](reference-mssqlctl.md)。

## <a name="commands"></a>命令
|     |     |
| --- | --- |
[mssqlctl storage mount create](#mssqlctl-storage-mount-create) | 在 HDFS 中的遠端存放區的掛接。
[mssqlctl storage mount delete](#mssqlctl-storage-mount-delete) | 刪除掛接在 HDFS 中的遠端存放區。
[mssqlctl 儲存體掛接狀態](#mssqlctl-storage-mount-status) | Mount(s) 的狀態。
## <a name="mssqlctl-storage-mount-create"></a>建立 mssqlctl 儲存體掛接
在 HDFS 中的遠端存放區的掛接。
```bash
mssqlctl storage mount create --remote-uri 
                              --mount-path  
                              [--credential-file]
```
### <a name="examples"></a>範例
若要使用的共用的金鑰的 HDFS 路徑 /mounts/adlsv2/data 上裝載容器 「 資料 」 在第 2 代 ADLS 帳戶 」 adlsv2example"
```bash
mssqlctl storage mount create --remote-uri abfs://data@adlsv2example.dfs.core.windows.net/
    --mount-path /mounts/adlsv2/data --credentials credential_file
```
若要裝載遠端 HDFS 叢集 (hdfs://namenode1:8080 /) 上本機 HDFS 路徑 /mounts hdfs /
```bash
mssqlctl storage mount create --remote-uri hdfs://namenode1:8080/ --mount-path /mounts/hdfs/
```
### <a name="required-parameters"></a>必要參數
#### `--remote-uri`
要掛接 （來源掛接） 的遠端存放區的 URI。
#### `--mount-path`
HDFS 路徑掛上對建立 （掛上的目的地）。
### <a name="optional-parameters"></a>選擇性參數
#### `--credential-file`
包含的認證來存取遠端存放區的檔案。 認證必須指定為索引鍵 = 值 」 配對一個索引鍵 = 每行的值。 任何在索引鍵或值的 equals 必須逸出。 預設為必要項無認證。 必要的金鑰，取決於所掛接的遠端存放區的類型和授權使用的類型。
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
## <a name="mssqlctl-storage-mount-delete"></a>mssqlctl 儲存體掛接 delete
刪除掛接在 HDFS 中的遠端存放區。
```bash
mssqlctl storage mount delete --mount-path 
                              
```
### <a name="examples"></a>範例
刪除掛接端建立 /mounts/adlsv2/data 第 2 代 ADLS 儲存體帳戶。
```bash
mssqlctl storage mount delete --mount-path /mounts/adlsv2/data
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
## <a name="mssqlctl-storage-mount-status"></a>mssqlctl 儲存體掛接狀態
Mount(s) 的狀態。
```bash
mssqlctl storage mount status [--mount-path] 
                              
```
### <a name="examples"></a>範例
取得以路徑掛接狀態
```bash
mssqlctl storage mount status --mount-path /mounts/hdfs
```
取得所有掛接的狀態。
```bash
mssqlctl storage mount status
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