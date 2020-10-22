---
title: azdata arc sql mi reference
titleSuffix: SQL Server big data clusters
description: azdata arc sql mi 命令的參考文章。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: seanw
ms.date: 09/22/2020
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 234a990cde52a6fd051410d30000413b9acfa3a0
ms.sourcegitcommit: 29a2be59c56f8a4b630af47760ef38d2bf56a3eb
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/22/2020
ms.locfileid: "92358676"
---
# <a name="azdata-arc-sql-mi"></a>azdata arc sql mi

適用於 [!INCLUDE [azure-data-cli-azdata](../../includes/azure-data-cli-azdata.md)]

下列文章提供 **azdata** 工具中 **sql** 命令的參考。 如需其他 **azdata** 命令的詳細資訊，請參閱 [azdata 參考](reference-azdata.md)

## <a name="commands"></a>命令

|命令|描述|
| --- | --- |
[azdata arc sql mi create](#azdata-arc-sql-mi-create) | 建立 SQL 受控執行個體。
[azdata arc sql mi edit](#azdata-arc-sql-mi-edit) | 編輯 SQL 受控執行個體的設定。
[azdata arc sql mi delete](#azdata-arc-sql-mi-delete) | 刪除 SQL 受控執行個體。
[azdata arc sql mi show](#azdata-arc-sql-mi-show) | 顯示 SQL 受控執行個體的詳細資料。
[azdata arc sql mi list](#azdata-arc-sql-mi-list) | 列出 SQL 受控執行個體。
[azdata arc sql mi config](reference-azdata-arc-sql-mi-config.md) | 組態命令。
## <a name="azdata-arc-sql-mi-create"></a>azdata arc sql mi create
若要設定 SQL 受控執行個體的密碼，請設定環境變數 AZDATA_PASSWORD
```bash
azdata arc sql mi create --name -n 
                         [--path]  
                         
[--cores-limit -cl]  
                         
[--cores-request -cr]  
                         
[--memory-limit -ml]  
                         
[--memory-request -mr]  
                         
[--storage-class-data -scd]  
                         
[--storage-class-logs -scl]  
                         
[--storage-class-data-logs -scdl]  
                         
[--storage-class-backups -scb]  
                         
[--volume-size-data -vsd]  
                         
[--volume-size-logs -vsl]  
                         
[--volume-size-data-logs -vsdl]  
                         
[--volume-size-backups -vsb]  
                         
[--no-external-endpoint]  
                         
[--dev]  
                         
[--no-wait]
```
### <a name="examples"></a>範例
建立 SQL 受控執行個體。
```bash
azdata arc sql mi create -n sqlmi1
```
### <a name="required-parameters"></a>必要參數
#### `--name -n`
SQL 受控執行個體的名稱。
### <a name="optional-parameters"></a>選擇性參數
#### `--path`
SQL 受控執行個體 json 檔案的 src 檔案路徑。
#### `--cores-limit -cl`
受控執行個體的核心限制 (整數)。
#### `--cores-request -cr`
受控執行個體的核心要求 (整數)。
#### `--memory-limit -ml`
受控執行個體的容量限制 (整數)。
#### `--memory-request -mr`
受控執行個體的容量要求 (以 GB 為單位的整數記憶體數量)。
#### `--storage-class-data -scd`
要用於資料的儲存類別 (.mdf)。 如果未指定任何值，則不會指定儲存類別，而會導致 Kubernetes 使用預設儲存類別。
#### `--storage-class-logs -scl`
要用於記錄的儲存類別 (/var/log)。 如果未指定任何值，則不會指定儲存類別，而會導致 Kubernetes 使用預設儲存類別。
#### `--storage-class-data-logs -scdl`
要用於資料庫記錄的儲存類別 (.ldf)。 如果未指定任何值，則不會指定儲存類別，而會導致 Kubernetes 使用預設儲存類別。
#### `--storage-class-backups -scb`
要用於備份的儲存類別 (/var/opt/mssql/backups)。 如果未指定任何值，則不會指定儲存類別，而會導致 Kubernetes 使用預設儲存類別。
#### `--volume-size-data -vsd`
要用於資料的儲存體磁碟區大小，以正數加上尾隨的 Ki (KB)、Mi (MB) 或 Gi (GB) 表示。
#### `--volume-size-logs -vsl`
要用於記錄的儲存體磁碟區大小，以正數加上尾隨的 Ki (KB)、Mi (MB) 或 Gi (GB) 表示。
#### `--volume-size-data-logs -vsdl`
要用於資料記錄的儲存體磁碟區大小，以正數加上尾隨的 Ki (KB)、Mi (MB) 或 Gi (GB) 表示。
#### `--volume-size-backups -vsb`
要用於備份的儲存體磁碟區大小，以正數加上尾隨的 Ki (KB)、Mi (MB) 或 Gi (GB) 表示。
#### `--no-external-endpoint`
若已指定，則不會建立外部服務。 否則，將會使用與資料控制器相同的服務類型來建立外部服務。
#### `--dev`
如果指定了此項目，則會將其視為開發執行個體，而不會對其計費。
#### `--no-wait`
若已給定，則命令不會等到執行個體處於就緒狀態才傳回。
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
## <a name="azdata-arc-sql-mi-edit"></a>azdata arc sql mi edit
編輯 SQL 受控執行個體的設定。
```bash
azdata arc sql mi edit --name -n 
                       [--path]  
                       
[--cores-limit -cl]  
                       
[--cores-request -cr]  
                       
[--memory-limit -ml]  
                       
[--memory-request -mr]  
                       
[--dev]  
                       
[--no-wait]
```
### <a name="examples"></a>範例
編輯 SQL 受控執行個體的設定。
```bash
azdata arc sql mi edit --path ./spec.json -n sqlmi1
```
### <a name="required-parameters"></a>必要參數
#### `--name -n`
正在編輯的 SQL 受控執行個體的名稱。 您的執行個體據以部署的名稱無法變更。
### <a name="optional-parameters"></a>選擇性參數
#### `--path`
SQL 受控執行個體 json 檔案的 src 檔案路徑。
#### `--cores-limit -cl`
受控執行個體的核心限制 (整數)。
#### `--cores-request -cr`
受控執行個體的核心要求 (整數)。
#### `--memory-limit -ml`
受控執行個體的容量限制 (整數)。
#### `--memory-request -mr`
受控執行個體的容量要求 (以 GB 為單位的整數記憶體數量)。
#### `--dev`
如果指定了此項目，則會將其視為開發執行個體，而不會對其計費。
#### `--no-wait`
若已給定，則命令不會等到執行個體處於就緒狀態才傳回。
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
## <a name="azdata-arc-sql-mi-delete"></a>azdata arc sql mi delete
刪除 SQL 受控執行個體。
```bash
azdata arc sql mi delete --name -n 
                         
```
### <a name="examples"></a>範例
刪除 SQL 受控執行個體。
```bash
azdata arc sql mi delete -n sqlmi1
```
### <a name="required-parameters"></a>必要參數
#### `--name -n`
要刪除的 SQL 受控執行個體的名稱。
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
## <a name="azdata-arc-sql-mi-show"></a>azdata arc sql mi show
顯示 SQL 受控執行個體的詳細資料。
```bash
azdata arc sql mi show --name -n 
                       [--path -p]
```
### <a name="examples"></a>範例
顯示 SQL 受控執行個體的詳細資料。
```bash
azdata arc sql mi show -n sqlmi1
```
### <a name="required-parameters"></a>必要參數
#### `--name -n`
要顯示的 SQL 受控執行個體的名稱。
### <a name="optional-parameters"></a>選擇性參數
#### `--path -p`
應在其中寫入 SQL 受控執行個體之完整規格的路徑。 如果省略，則會將規格寫入標準輸出。
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
## <a name="azdata-arc-sql-mi-list"></a>azdata arc sql mi list
列出 SQL 受控執行個體。
```bash
azdata arc sql mi list 
```
### <a name="examples"></a>範例
列出 SQL 受控執行個體。
```bash
azdata arc sql mi list
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

