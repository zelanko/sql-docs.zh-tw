---
title: azdata arc postgres server backup reference
titleSuffix: SQL Server big data clusters
description: azdata arc postgres server backup 命令的參考文章。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: seanw
ms.date: 09/22/2020
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 3e8eba05f00bf625097776fd7f117524c6a8aca4
ms.sourcegitcommit: d56f1eca807c55cf606a6316f3872585f014fec1
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/22/2020
ms.locfileid: "90942387"
---
# <a name="azdata-arc-postgres-server-backup"></a>azdata arc postgres server backup

適用於 `azdata`

下列文章提供 **azdata** 工具中 **sql** 命令的參考。 如需其他 **azdata** 命令的詳細資訊，請參閱 [azdata 參考](reference-azdata.md)

## <a name="commands"></a>命令

|命令|描述|
| --- | --- |
[azdata arc postgres server backup create](#azdata-arc-postgres-server-backup-create) | 建立 PostgreSQL 伺服器群組的備份。
[azdata arc postgres server backup delete](#azdata-arc-postgres-server-backup-delete) | 刪除 PostgreSQL 伺服器群組的備份。
[azdata arc postgres server backup restore](#azdata-arc-postgres-server-backup-restore) | 還原 PostgreSQL 伺服器群組的備份。
[azdata arc postgres server backup restorestatus](#azdata-arc-postgres-server-backup-restorestatus) | 取得最新還原作業的狀態 (如果有的話)。
[azdata arc postgres server backup show](#azdata-arc-postgres-server-backup-show) | 顯示 PostgreSQL 伺服器群組備份的相關詳細資料。
## <a name="azdata-arc-postgres-server-backup-create"></a>azdata arc postgres server backup create
建立 PostgreSQL 伺服器群組的備份。
```bash
azdata arc postgres server backup create 
```
### <a name="examples"></a>範例
建立服務 'pg' 的備份。
```bash
azdata arc postgres server backup create -sn pg
```
建立服務 'pg' 的具名備份。
```bash
azdata arc postgres server backup create -sn pg -n backup1
```
### <a name="global-arguments"></a>全域引數
#### `--debug`
增加記錄詳細資訊，以顯示所有偵錯記錄。
#### `--help -h`
顯示此說明訊息並結束。
#### `--output -o`
輸出格式。  允許的值：json、jsonc、table、tsv。  預設值：json。
#### `--query -q`
JMESPath 查詢字串。 如需詳細資訊和範例，請參閱 [http://jmespath.org/](http://jmespath.org)。
#### `--verbose`
增加記錄詳細資訊。 使用 --debug 來取得完整偵錯記錄。
## <a name="azdata-arc-postgres-server-backup-delete"></a>azdata arc postgres server backup delete
刪除 PostgreSQL 伺服器群組的備份。
```bash
azdata arc postgres server backup delete 
```
### <a name="examples"></a>範例
刪除 PostgreSQL 伺服器群組的備份。
```bash
azdata arc postgres backup delete -sn pg -id e07dd3940e374bd9acbc86869cbc123d
```
### <a name="global-arguments"></a>全域引數
#### `--debug`
增加記錄詳細資訊，以顯示所有偵錯記錄。
#### `--help -h`
顯示此說明訊息並結束。
#### `--output -o`
輸出格式。  允許的值：json、jsonc、table、tsv。  預設值：json。
#### `--query -q`
JMESPath 查詢字串。 如需詳細資訊和範例，請參閱 [http://jmespath.org/](http://jmespath.org)。
#### `--verbose`
增加記錄詳細資訊。 使用 --debug 來取得完整偵錯記錄。
## <a name="azdata-arc-postgres-server-backup-restore"></a>azdata arc postgres server backup restore
還原 PostgreSQL 伺服器群組的備份。
```bash
azdata arc postgres server backup restore 
```
### <a name="examples"></a>範例
還原最新的備份。
```bash
azdata arc postgres server restore -sn pg```
Restore a backup by ID
```bash
azdata arc postgres server restore -sn pg -id 123e4567e89b12d3a456426655440000
```
### <a name="global-arguments"></a>全域引數
#### `--debug`
增加記錄詳細資訊，以顯示所有偵錯記錄。
#### `--help -h`
顯示此說明訊息並結束。
#### `--output -o`
輸出格式。  允許的值：json、jsonc、table、tsv。  預設值：json。
#### `--query -q`
JMESPath 查詢字串。 如需詳細資訊和範例，請參閱 [http://jmespath.org/](http://jmespath.org)。
#### `--verbose`
增加記錄詳細資訊。 使用 --debug 來取得完整偵錯記錄。
## <a name="azdata-arc-postgres-server-backup-restorestatus"></a>azdata arc postgres server backup restorestatus
取得最新還原作業的狀態 (如果有的話)。
```bash
azdata arc postgres server backup restorestatus 
```
### <a name="examples"></a>範例
依識別碼取得服務 'pg' 最近的還原狀態。
```bash
azdata arc postgres server backup restorestatus -sn pg -id 123e4567e89b12d3a456426655440000
```
### <a name="global-arguments"></a>全域引數
#### `--debug`
增加記錄詳細資訊，以顯示所有偵錯記錄。
#### `--help -h`
顯示此說明訊息並結束。
#### `--output -o`
輸出格式。  允許的值：json、jsonc、table、tsv。  預設值：json。
#### `--query -q`
JMESPath 查詢字串。 如需詳細資訊和範例，請參閱 [http://jmespath.org/](http://jmespath.org)。
#### `--verbose`
增加記錄詳細資訊。 使用 --debug 來取得完整偵錯記錄。
## <a name="azdata-arc-postgres-server-backup-show"></a>azdata arc postgres server backup show
顯示 PostgreSQL 伺服器群組備份的相關詳細資料。
```bash
azdata arc postgres server backup show 
```
### <a name="examples"></a>範例
依識別碼取得服務 'pg' 的備份
```bash
azdata arc postgres server backup show -sn pg -id 123e4567e89b12d3a456426655440000
```
### <a name="global-arguments"></a>全域引數
#### `--debug`
增加記錄詳細資訊，以顯示所有偵錯記錄。
#### `--help -h`
顯示此說明訊息並結束。
#### `--output -o`
輸出格式。  允許的值：json、jsonc、table、tsv。  預設值：json。
#### `--query -q`
JMESPath 查詢字串。 如需詳細資訊和範例，請參閱 [http://jmespath.org/](http://jmespath.org)。
#### `--verbose`
增加記錄詳細資訊。 使用 --debug 來取得完整偵錯記錄。

## <a name="next-steps"></a>後續步驟

如需其他 **azdata** 命令的詳細資訊，請參閱 [azdata 參考](reference-azdata.md)。 

如需如何安裝 **azdata** 工具的詳細資訊，請參閱[安裝 azdata](..\install\deploy-install-azdata.md)。

