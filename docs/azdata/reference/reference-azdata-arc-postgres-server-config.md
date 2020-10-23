---
title: azdata arc postgres server config reference
titleSuffix: SQL Server big data clusters
description: azdata arc postgres server config 命令的參考文章。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: seanw
ms.date: 09/22/2020
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 0c955a422d75e7f57fde2272675240e9b5337141
ms.sourcegitcommit: 29a2be59c56f8a4b630af47760ef38d2bf56a3eb
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/22/2020
ms.locfileid: "92358736"
---
# <a name="azdata-arc-postgres-server-config"></a>azdata arc postgres server config

適用於 [!INCLUDE [azure-data-cli-azdata](../../includes/azure-data-cli-azdata.md)]

下列文章提供 **azdata** 工具中 **sql** 命令的參考。 如需其他 **azdata** 命令的詳細資訊，請參閱 [azdata 參考](reference-azdata.md)

## <a name="commands"></a>命令

|命令|描述|
| --- | --- |
[azdata arc postgres server config init](#azdata-arc-postgres-server-config-init) | 初始化 PostgreSQL 伺服器群組的 CRD 和規格檔案。
[azdata arc postgres server config add](#azdata-arc-postgres-server-config-add) | 針對設定檔中的 json 路徑新增值。
[azdata arc postgres server config remove](#azdata-arc-postgres-server-config-remove) | 針對設定檔中的 json 路徑移除值。
[azdata arc postgres server config replace](#azdata-arc-postgres-server-config-replace) | 針對設定檔中的 json 路徑取代值。
[azdata arc postgres server config patch](#azdata-arc-postgres-server-config-patch) | 以 json 修補檔為基礎修補設定檔。
## <a name="azdata-arc-postgres-server-config-init"></a>azdata arc postgres server config init
初始化 PostgreSQL 伺服器群組的 CRD 和規格檔案。
```bash
azdata arc postgres server config init --path -p 
                                       [--engine-version -ev]
```
### <a name="examples"></a>範例
初始化 PostgreSQL 伺服器群組的 CRD 和規格檔案。
```bash
azdata arc postgres server config init --path ./template
```
### <a name="required-parameters"></a>必要參數
#### `--path -p`
應在其中寫入 PostgreSQL 伺服器群組之 CRD 和規格的路徑。
### <a name="optional-parameters"></a>選擇性參數
#### `--engine-version -ev`
必須是 11 或 12。 預設值為 12。
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
## <a name="azdata-arc-postgres-server-config-add"></a>azdata arc postgres server config add
將值新增至設定檔中的 json 路徑。  所有下列範例都是以 Bash 提供。  如果您是使用另一個命令列，請留意您可能需要適當地逸出引號。  或者，您可以使用修補檔案功能。
```bash
azdata arc postgres server config add --path -p 
                                      --json-values -j
```
### <a name="examples"></a>範例
範例 1 - 新增儲存體。
```bash
azdata arc postgres server config add --path custom/spec.json --json-values "spec.storage={"accessMode":"ReadWriteOnce","className":"managed-premium","size":"10Gi"}"
```
### <a name="required-parameters"></a>必要參數
#### `--path -p`
自訂資源規格的路徑，即 custom/spec.json
#### `--json-values -j`
針對值之 json 路徑的機碼值組清單：key1.subkey1=value1,key2.subkey2=value2. 您可以提供內嵌 json 值，例如 key='{"kind":"cluster","name":"test-cluster"}'，或是提供檔案路徑，例如 key=./values.json。 新增作業不支援條件。  如果您要提供的內嵌值是包含 "=" 和 "," 的機碼值組，請將這些字元逸出。  例如 key1="key2\=val2\,key3\=val3"。 請參閱 http://jsonpatch.com/ \(英文\) 以取得路徑外觀的範例。  如果您想要存取陣列，您必須指出索引 (例如 key.0=value) 來這麼做
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
## <a name="azdata-arc-postgres-server-config-remove"></a>azdata arc postgres server config remove
移除設定檔中 json 路徑的值。  所有下列範例都是以 Bash 提供。  如果您是使用另一個命令列，請留意您可能需要適當地逸出引號。  或者，您可以使用修補檔案功能。
```bash
azdata arc postgres server config remove --path -p 
                                         --json-path -j
```
### <a name="examples"></a>範例
範例 1 - 移除儲存體。
```bash
azdata arc postgres server config remove --path custom/spec.json --json-path ".spec.storage"
```
### <a name="required-parameters"></a>必要參數
#### `--path -p`
自訂資源規格的路徑，即 custom/spec.json
#### `--json-path -j`
根據 jsonpatch 程式庫的 json 路徑清單，其能指出您想要移除的值，例如：key1.subkey1,key2.subkey2。 移除作業不支援條件。 請參閱 http://jsonpatch.com/ \(英文\) 以取得路徑外觀的範例。  如果您想要存取陣列，您必須指出索引 (例如 key.0=value) 來這麼做
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
## <a name="azdata-arc-postgres-server-config-replace"></a>azdata arc postgres server config replace
取代設定檔中 json 路徑的值。  所有下列範例都是以 Bash 提供。  如果您是使用另一個命令列，請留意您可能需要適當地逸出引號。  或者，您可以使用修補檔案功能。
```bash
azdata arc postgres server config replace --path -p 
                                          --json-values -j
```
### <a name="examples"></a>範例
範例 1 - 取代單一端點的連接埠。
```bash
azdata arc postgres server config replace --path custom/spec.json --json-values "$.spec.endpoints[?(@.name=="Controller")].port=30080"
```
範例 2 - 取代儲存體。
```bash
azdata arc postgres server config replace --path custom/spec.json --json-values "spec.storage={"accessMode":"ReadWriteOnce","className":"managed-premium","size":"10Gi"}"
```
### <a name="required-parameters"></a>必要參數
#### `--path -p`
自訂資源規格的路徑，即 custom/spec.json
#### `--json-values -j`
針對值之 json 路徑的機碼值組清單：key1.subkey1=value1,key2.subkey2=value2. 您可以提供內嵌 json 值，例如 key='{"kind":"cluster","name":"test-cluster"}'，或是提供檔案路徑，例如 key=./values.json。 取代作業可透過 jsonpath 程式庫支援條件。  若要使用此方法，請以 $ 作為路徑開頭。 這可讓您執行如 -j $.key1.key2[?(@.key3=="someValue"].key4=value 的條件。 如果您要提供的內嵌值是包含 "=" 和 "," 的機碼值組，請將這些字元逸出。  例如 key1="key2\=val2\,key3\=val3"。 您可以參閱底下的範例。 如需其他協助，請參閱： https://jsonpath.com/ \(英文\)
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
## <a name="azdata-arc-postgres-server-config-patch"></a>azdata arc postgres server config patch
根據指定的修補檔來修補設定檔。 請參閱 http://jsonpatch.com/ \(英文\) 以深入了解路徑的撰寫方式。 基於 jsonpath 程式庫 https://jsonpath.com/ \(英文\) 的原因，取代作業可以在其路徑中使用條件。 所有修補 json 檔案都必須以 "patch" 的機碼作為開頭，其具有修補陣列及其相對應的作業 (新增、取代、移除)、路徑及值。 「移除」作業不需要值，只需要路徑。 請參閱以下的範例。
```bash
azdata arc postgres server config patch --path -p 
                                        --patch-file
```
### <a name="examples"></a>範例
範例 1 - 使用修補檔案取代單一端點的連接埠。
```bash
azdata arc postgres server config patch --path custom/spec.json --patch ./patch.json

    Patch File Example (patch.json):
        {"patch":[{"op":"replace","path":"$.spec.endpoints[?(@.name=="Controller")].port","value":30080}]}
```
範例 2 - 使用修補檔案取代儲存體。
```bash
azdata arc postgres server config patch --path custom/spec.json --patch ./patch.json

    Patch File Example (patch.json):
        {"patch":[{"op":"replace","path":".spec.storage","value":{"accessMode":"ReadWriteMany","className":"managed-premium","size":"10Gi"}}]}
```
### <a name="required-parameters"></a>必要參數
#### `--path -p`
自訂資源規格的路徑，即 custom/spec.json
#### `--patch-file`
以 jsonpatch 程式庫 http://jsonpatch.com/ \(英文\) 為基礎之修補 json 檔案的路徑。 您必須以名為 "patch" 的機碼作為修補 json 檔案的開頭，其值是您要執行之修補作業的陣列。 針對修補作業的路徑，您可以使用點標記法，例如可針對大部分作業使用的 key1.key2。 如果您想要進行取代作業，且您是要取代需要條件之陣列中的值，請透過以 $ 作為路徑開頭來使用 jsonpath 標記法。 這可讓您執行如 $.key1.key2[?(@.key3=="someValue"].key4 的條件。 請參閱以下的範例。 如需條件的其他協助，請參閱： https://jsonpath.com/ \(英文\)。
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

