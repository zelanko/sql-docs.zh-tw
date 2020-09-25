---
title: azdata arc postgres server reference
titleSuffix: SQL Server big data clusters
description: azdata arc postgres server 命令的參考文章。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: seanw
ms.date: 09/22/2020
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 3f34baeca8914adfcceda30766d46da50aa13517
ms.sourcegitcommit: d56f1eca807c55cf606a6316f3872585f014fec1
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/22/2020
ms.locfileid: "90942383"
---
# <a name="azdata-arc-postgres-server"></a>azdata arc postgres server

適用於 `azdata`

下列文章提供 **azdata** 工具中 **sql** 命令的參考。 如需其他 **azdata** 命令的詳細資訊，請參閱 [azdata 參考](reference-azdata.md)

## <a name="commands"></a>命令

|命令|描述|
| --- | --- |
[azdata arc postgres server create](#azdata-arc-postgres-server-create) | 建立 PostgreSQL 伺服器群組。
[azdata arc postgres server edit](#azdata-arc-postgres-server-edit) | 編輯 PostgreSQL 伺服器群組的設定。
[azdata arc postgres server delete](#azdata-arc-postgres-server-delete) | 刪除 PostgreSQL 伺服器群組。
[azdata arc postgres server show](#azdata-arc-postgres-server-show) | 顯示 PostgreSQL 伺服器群組的詳細資料。
[azdata arc postgres server list](#azdata-arc-postgres-server-list) | 列出 PostgreSQL 伺服器群組。
[azdata arc postgres server config](reference-azdata-arc-postgres-server-config.md) | 組態命令。
[azdata arc postgres server backup](reference-azdata-arc-postgres-server-backup.md) | 管理 PostgreSQL 伺服器群組備份。
## <a name="azdata-arc-postgres-server-create"></a>azdata arc postgres server create
若要設定伺服器群組的密碼，請設定環境變數 AZDATA_PASSWORD
```bash
azdata arc postgres server create --name -n 
                                  [--path]  
                                  
[--cores-limit -cl]  
                                  
[--cores-request -cr]  
                                  
[--memory-limit -ml]  
                                  
[--memory-request -mr]  
                                  
[--storage-class-data -scd]  
                                  
[--storage-class-logs -scl]  
                                  
[--storage-class-backups -scb]  
                                  
[--extensions]  
                                  
[--volume-size-data -vsd]  
                                  
[--volume-size-logs -vsl]  
                                  
[--volume-size-backups -vsb]  
                                  
[--workers -w]  
                                  
[--engine-version -ev]  
                                  
[--no-external-endpoint]  
                                  
[--dev]  
                                  
[--port]  
                                  
[--no-wait]  
                                  
[--engine-settings -e]
```
### <a name="examples"></a>範例
建立 PostgreSQL 伺服器群組。
```bash
azdata arc postgres server create -n pg1
```
使用引擎設定建立 PostgreSQL 伺服器群組。 下列兩個範例都是有效的。
```bash
azdata arc postgres server create -n pg1 --engine-settings "key1=val1"
azdata arc postgres server create -n pg1 --engine-settings "key2=val2"
```
### <a name="required-parameters"></a>必要參數
#### `--name -n`
執行個體的名稱。
### <a name="optional-parameters"></a>選擇性參數
#### `--path`
PostgreSQL 伺服器群組的來源 json 檔案路徑。 這是選擇性的。
#### `--cores-limit -cl`
每個節點可以使用的 Postgres 執行個體 CPU 核心數目上限。 支援小數核心數。
#### `--cores-request -cr`
每個節點為了排程服務所需的可用 CPU 核心數目下限。 支援小數核心數。
#### `--memory-limit -ml`
Postgres 執行個體的記憶體限制，以數值加上尾隨的 Ki (KB)、Mi (MB) 或 Gi (GB) 表示。
#### `--memory-request -mr`
Postgres 執行個體的記憶體要求，以數值加上尾隨的 Ki (KB)、Mi (MB) 或 Gi (GB) 表示。
#### `--storage-class-data -scd`
要用於資料永續性磁碟區的儲存類別。
#### `--storage-class-logs -scl`
要用於記錄永續性磁碟區的儲存類別。
#### `--storage-class-backups -scb`
要用於備份永續性磁碟區的儲存類別。
#### `--extensions`
啟動時應載入的 Postgres 延伸模組清單 (以逗號分隔)。 請參閱 Postgres 文件以了解支援的值。
#### `--volume-size-data -vsd`
要用於資料的儲存體磁碟區大小，以正數加上尾隨的 Ki (KB)、Mi (MB) 或 Gi (GB) 表示。
#### `--volume-size-logs -vsl`
要用於記錄的儲存體磁碟區大小，以正數加上尾隨的 Ki (KB)、Mi (MB) 或 Gi (GB) 表示。
#### `--volume-size-backups -vsb`
要用於備份的儲存體磁碟區大小，以正數加上尾隨的 Ki (KB)、Mi (MB) 或 Gi (GB) 表示。
#### `--workers -w`
要在分區叢集中佈建的背景工作節點數目；若是單一節點 Postgres 則為零 (預設值)。
#### `--engine-version -ev`
必須是 11 或 12。 預設值為 12。
#### `--no-external-endpoint`
若已指定，則不會建立外部服務。 否則，將會使用與資料控制器相同的服務類型來建立外部服務。
#### `--dev`
如果指定了此項目，則會將其視為開發執行個體，而不會對其計費。
#### `--port`
選擇性。
#### `--no-wait`
若已給定，則命令不會等到執行個體處於就緒狀態才傳回。
#### `--engine-settings -e`
以逗號分隔的 Postgres 引擎設定清單，格式為 'key1=val1, key2=val2'。
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
## <a name="azdata-arc-postgres-server-edit"></a>azdata arc postgres server edit
編輯 PostgreSQL 伺服器群組的設定。
```bash
azdata arc postgres server edit --name -n 
                                [--path]  
                                
[--workers -w]  
                                
[--engine-version -ev]  
                                
[--cores-limit -cl]  
                                
[--cores-request -cr]  
                                
[--memory-limit -ml]  
                                
[--memory-request -mr]  
                                
[--extensions]  
                                
[--dev]  
                                
[--port]  
                                
[--no-wait]  
                                
[--engine-settings -e]  
                                
[--replace-engine-settings -re]  
                                
[--admin-password]
```
### <a name="examples"></a>範例
編輯 PostgreSQL 伺服器群組的設定。
```bash
azdata arc postgres server edit --src ./spec.json -n pg1
```
使用引擎設定編輯 PostgreSQL 伺服器群組。
```bash
azdata arc postgres server edit -n pg1 --engine-settings "key2=val2"
```
編輯 PostgreSQL 伺服器群組，並將現有的引擎設定取代為新設定 key1=val1。
```bash
azdata arc postgres server edit -n pg1 --engine-settings "key1=val1" --replace-engine-settings
```
### <a name="required-parameters"></a>必要參數
#### `--name -n`
正在編輯的 PostgreSQL 伺服器群組的名稱。 您的執行個體據以部署的名稱無法變更。
### <a name="optional-parameters"></a>選擇性參數
#### `--path`
PostgreSQL 伺服器群組的來源 json 檔案路徑。 這是選擇性的。
#### `--workers -w`
要在分區叢集中佈建的背景工作節點數目；若是單一節點 Postgres 則為零 (預設值)。
#### `--engine-version -ev`
引擎版本無法變更。 當不同引擎版本的兩個伺服器群組具有相同名稱時，可以將 --engine-version 與 --name 搭配使用，以識別 PostgreSQL 超大規模資料庫伺服器群組。 --engine-version 是選擇性的，在用來識別伺服器群組時，必須是 11 或 12。
#### `--cores-limit -cl`
每個節點可以使用的 Postgres 執行個體 CPU 核心數目上限 (支援小數核心數)。 若要移除 cores_limit，請將其值指定為空字串。
#### `--cores-request -cr`
每個節點為了排程服務所需的可用 CPU 核心數目下限 (支援小數核心數)。 若要移除 cores_request，請將其值指定為空字串。
#### `--memory-limit -ml`
Postgres 執行個體的記憶體限制，以數值加上尾隨的 Ki (KB)、Mi (MB) 或 Gi (GB) 表示。 若要移除 memory_limit，請將其值指定為空字串。
#### `--memory-request -mr`
Postgres 執行個體的記憶體要求，以數值加上尾隨的 Ki (KB)、Mi (MB) 或 Gi (GB) 表示。 若要移除 memory_request，請將其值指定為空字串。
#### `--extensions`
啟動時應載入的 Postgres 延伸模組清單 (以逗號分隔)。 請參閱 Postgres 文件以了解支援的值。
#### `--dev`
如果指定了此項目，則會將其視為開發執行個體，而不會對其計費。
#### `--port`
選擇性。
#### `--no-wait`
若已給定，則命令不會等到執行個體處於就緒狀態才傳回。
#### `--engine-settings -e`
以逗號分隔的 Postgres 引擎設定清單，格式為 'key1=val1, key2=val2'。 提供的設定將會與現有的設定合併。 若要移除設定，請提供 'removedKey=' 之類的空值。 如果您變更需要重新啟動的引擎設定，服務將會立即重新啟動以套用設定。
#### `--replace-engine-settings -re`
使用 --engine-settings 指定時，會將所有現有的自訂引擎設定取代成一組新的設定和值。
#### `--admin-password`
若已指定，Postgres 伺服器的管理員密碼會設定為 AZDATA_PASSWORD 環境變數的值 (如果有的話)，否則會出現提示的值。
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
## <a name="azdata-arc-postgres-server-delete"></a>azdata arc postgres server delete
刪除 PostgreSQL 伺服器群組。
```bash
azdata arc postgres server delete --name -n 
                                  [--engine-version -ev]
```
### <a name="examples"></a>範例
刪除 PostgreSQL 伺服器群組。
```bash
azdata arc postgres server delete -n pg1
```
### <a name="required-parameters"></a>必要參數
#### `--name -n`
PostgreSQL 伺服器群組的名稱。
### <a name="optional-parameters"></a>選擇性參數
#### `--engine-version -ev`
當不同引擎版本的兩個伺服器群組具有相同名稱時，可以將 --engine-version 與 --name 搭配使用，以識別 PostgreSQL 超大規模資料庫伺服器群組。 --engine-version 是選擇性的，在用來識別伺服器群組時，必須是 11 或 12。
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
## <a name="azdata-arc-postgres-server-show"></a>azdata arc postgres server show
顯示 PostgreSQL 伺服器群組的詳細資料。
```bash
azdata arc postgres server show --name -n 
                                [--engine-version -ev]  
                                
[--path -p]
```
### <a name="examples"></a>範例
顯示 PostgreSQL 伺服器群組的詳細資料。
```bash
azdata arc postgres server show -n pg1
```
### <a name="required-parameters"></a>必要參數
#### `--name -n`
PostgreSQL 伺服器群組的名稱。
### <a name="optional-parameters"></a>選擇性參數
#### `--engine-version -ev`
當不同引擎版本的兩個伺服器群組具有相同名稱時，可以將 --engine-version 與 --name 搭配使用，以識別 PostgreSQL 超大規模資料庫伺服器群組。 --engine-version 是選擇性的，在用來識別伺服器群組時，必須是 11 或 12。
#### `--path -p`
應在其中寫入 PostgreSQL 伺服器群組之完整規格的路徑。 如果省略，則會將規格寫入標準輸出。
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
## <a name="azdata-arc-postgres-server-list"></a>azdata arc postgres server list
列出 PostgreSQL 伺服器群組。
```bash
azdata arc postgres server list 
```
### <a name="examples"></a>範例
列出 PostgreSQL 伺服器群組。
```bash
azdata arc postgres server list
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

