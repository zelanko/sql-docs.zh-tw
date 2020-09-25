---
title: azdata arc dc config reference
titleSuffix: SQL Server big data clusters
description: azdata arc dc config 命令的參考文章。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: seanw
ms.date: 09/22/2020
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 302235f43791f1be918f1e78114a40bcb23ea818
ms.sourcegitcommit: d56f1eca807c55cf606a6316f3872585f014fec1
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/22/2020
ms.locfileid: "90942369"
---
# <a name="azdata-arc-dc-config"></a>azdata arc dc config

適用於 `azdata`

下列文章提供 **azdata** 工具中 **sql** 命令的參考。 如需其他 **azdata** 命令的詳細資訊，請參閱 [azdata 參考](reference-azdata.md)

## <a name="commands"></a>命令

|命令|描述|
| --- | --- |
[azdata arc dc config init](#azdata-arc-dc-config-init) | 初始化可用來建立控制項的資料控制器組態設定檔。
[azdata arc dc config list](#azdata-arc-dc-config-list) | 列出可用的設定檔選項。
[azdata arc dc config add](#azdata-arc-dc-config-add) | 針對設定檔中的 json 路徑新增值。
[azdata arc dc config remove](#azdata-arc-dc-config-remove) | 針對設定檔中的 json 路徑移除值。
[azdata arc dc config replace](#azdata-arc-dc-config-replace) | 針對設定檔中的 json 路徑取代值。
[azdata arc dc config patch](#azdata-arc-dc-config-patch) | 以 json 修補檔為基礎修補設定檔。
## <a name="azdata-arc-dc-config-init"></a>azdata arc dc config init
初始化可用來建立控制項的資料控制器組態設定檔。 您可在引數中指定組態設定檔的特定來源。
```bash
azdata arc dc config init [--path -p] 
                          [--source -s]  
                          
[--force -f]
```
### <a name="examples"></a>範例
引導式資料控制器設定初始化體驗；系統將會提示您提供所需的值。
```bash
azdata arc dc config init
```
搭配引數的 arc dc 設定初始化，其會在 ./custom 中建立 aks-dev-test 的設定檔。
```bash
azdata arc dc config init --source aks-dev-test --path custom
```
### <a name="optional-parameters"></a>選擇性參數
#### `--path -p`
您要放置設定檔的檔案路徑，預設為 <cwd>/custom。
#### `--source -s`
組態設定檔來源：['azure-arc-aks-premium-storage', 'azure-arc-ake', 'azure-arc-openshift', 'azure-arc-gke', 'azure-arc-aks-default-storage', 'azure-arc-aks-dev-test', 'azure-arc-kubeadm', 'azure-arc-kubeadm-dev-test', 'azure-arc-eks', 'azure-arc-azure-openshift', 'azure-arc-aks-hci']
#### `--force -f`
強制覆寫目標檔案。
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
## <a name="azdata-arc-dc-config-list"></a>azdata arc dc config list
列出可在 `arc dc config init` 中使用的設定檔選項
```bash
azdata arc dc config list [--config-profile -c] 
                          
```
### <a name="examples"></a>範例
顯示所有可用的設定檔名稱。
```bash
azdata arc dc config list
```
顯示特定設定檔的 json。
```bash
azdata arc dc config list --config-profile aks-dev-test
```
### <a name="optional-parameters"></a>選擇性參數
#### `--config-profile -c`
預設組態設定檔：['azure-arc-aks-premium-storage', 'azure-arc-ake', 'azure-arc-openshift', 'azure-arc-gke', 'azure-arc-aks-default-storage', 'azure-arc-aks-dev-test', 'azure-arc-kubeadm', 'azure-arc-kubeadm-dev-test', 'azure-arc-eks', 'azure-arc-azure-openshift', 'azure-arc-aks-hci']
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
## <a name="azdata-arc-dc-config-add"></a>azdata arc dc config add
將值新增至設定檔中的 json 路徑。  所有下列範例都是以 Bash 提供。  如果您是使用另一個命令列，請留意您可能需要適當地逸出引號。  或者，您可以使用修補檔案功能。
```bash
azdata arc dc config add --path -p 
                         --json-values -j
```
### <a name="examples"></a>範例
範例 1 - 新增資料控制器儲存體。
```bash
azdata arc dc config add --path custom/control.json --json-values "spec.storage={"accessMode":"ReadWriteOnce","className":"managed-premium","size":"10Gi"}"
```
### <a name="required-parameters"></a>必要參數
#### `--path -p`
您要設定之設定的資料控制器組態檔路徑，也就是 custom/control.json
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
## <a name="azdata-arc-dc-config-remove"></a>azdata arc dc config remove
移除設定檔中 json 路徑的值。  所有下列範例都是以 Bash 提供。  如果您是使用另一個命令列，請留意您可能需要適當地逸出引號。  或者，您可以使用修補檔案功能。
```bash
azdata arc dc config remove --path -p 
                            --json-path -j
```
### <a name="examples"></a>範例
範例 1 - 移除資料控制器儲存體。
```bash
azdata arc dc config remove --path custom/control.json --json-path ".spec.storage"
```
### <a name="required-parameters"></a>必要參數
#### `--path -p`
您要設定之設定的資料控制器組態檔路徑，也就是 custom/control.json
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
## <a name="azdata-arc-dc-config-replace"></a>azdata arc dc config replace
取代設定檔中 json 路徑的值。  所有下列範例都是以 Bash 提供。  如果您是使用另一個命令列，請留意您可能需要適當地逸出引號。  或者，您可以使用修補檔案功能。
```bash
azdata arc dc config replace --path -p 
                             --json-values -j
```
### <a name="examples"></a>範例
範例 1 - 取代單一端點 (資料控制器端點) 的連接埠。
```bash
azdata arc dc config replace --path custom/control.json --json-values "$.spec.endpoints[?(@.name=="Controller")].port=30080"
```
範例 2 - 取代資料控制器儲存體。
```bash
azdata arc dc config replace --path custom/control.json --json-values "spec.storage={"accessMode":"ReadWriteOnce","className":"managed-premium","size":"10Gi"}"
```
### <a name="required-parameters"></a>必要參數
#### `--path -p`
您要設定之設定的資料控制器組態檔路徑，也就是 custom/control.json
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
## <a name="azdata-arc-dc-config-patch"></a>azdata arc dc config patch
根據指定的修補檔來修補設定檔。 請參閱 http://jsonpatch.com/ \(英文\) 以深入了解路徑的撰寫方式。 基於 jsonpath 程式庫 https://jsonpath.com/ \(英文\) 的原因，取代作業可以在其路徑中使用條件。 所有修補 json 檔案都必須以 "patch" 的機碼作為開頭，其具有修補陣列及其相對應的作業 (新增、取代、移除)、路徑及值。 「移除」作業不需要值，只需要路徑。 請參閱以下的範例。
```bash
azdata arc dc config patch --path 
                           --patch-file -p
```
### <a name="examples"></a>範例
範例 1 - 使用修補檔案取代單一端點 (資料控制器端點) 的連接埠。
```bash
azdata arc dc config patch --path custom/control.json --patch ./patch.json

    Patch File Example (patch.json):
        {"patch":[{"op":"replace","path":"$.spec.endpoints[?(@.name=="Controller")].port","value":30080}]}
```
範例 2 - 使用修補檔案取代資料控制器儲存體。
```bash
azdata arc dc config patch --path custom/control.json --patch ./patch.json

    Patch File Example (patch.json):
        {"patch":[{"op":"replace","path":".spec.storage","value":{"accessMode":"ReadWriteMany","className":"managed-premium","size":"10Gi"}}]}
```
### <a name="required-parameters"></a>必要參數
#### `--path`
您要設定之設定的資料控制器組態檔路徑，也就是 custom/control.json
#### `--patch-file -p`
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

