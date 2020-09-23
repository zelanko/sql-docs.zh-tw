---
title: azdata bdc config 參考
titleSuffix: SQL Server big data clusters
description: 使用此參考文章了解 azdata 工具中的 SQL 命令，特別是 bdc config 命令。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 06/22/2020
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 59ed511415e331529a1378d0db426de71ab6c667
ms.sourcegitcommit: 883435b4c7366f06ac03579752093737b098feab
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/28/2020
ms.locfileid: "89733639"
---
# <a name="azdata-bdc-config"></a>azdata bdc config

[!INCLUDE[SQL Server 2019](../../includes/applies-to-version/sqlserver2019.md)]

下文提供 `azdata` 工具中 `sql` 命令的參考。 如需其他 `azdata` 命令的詳細資訊，請參閱 [azdata 參考](reference-azdata.md)。

## <a name="commands"></a>命令
| 命令 | 說明 |
| --- | --- |
[azdata bdc config init](#azdata-bdc-config-init) | 初始化可搭配 bdc create 使用的巨量資料叢集組態設定檔。
[azdata bdc config list](#azdata-bdc-config-list) | 列出可用的設定檔選項。
[azdata bdc config show](#azdata-bdc-config-show) | 顯示 BDC 目前的設定，或您指定的本機檔案設定，亦即 custom/bdc.json。
[azdata bdc config add](#azdata-bdc-config-add) | 針對設定檔中的 json 路徑新增值。
[azdata bdc config remove](#azdata-bdc-config-remove) | 針對設定檔中的 json 路徑移除值。
[azdata bdc config replace](#azdata-bdc-config-replace) | 針對設定檔中的 json 路徑取代值。
[azdata bdc config patch](#azdata-bdc-config-patch) | 以 json 修補檔為基礎修補設定檔。
[azdata bdc config set](#azdata-bdc-config-set) | 這是進行中的工作，可設定巨量資料叢集的組態。
[azdata bdc config upgrade](#azdata-bdc-config-upgrade) | 這是進行中的工作，可升級巨量資料叢集的組態。
## <a name="azdata-bdc-config-init"></a>azdata bdc config init
初始化可搭配 bdc create 使用的巨量資料叢集組態設定檔。 您可在引數中指定組態設定檔的特定來源。
```bash
azdata bdc config init [--target -t] 
                       [--source -s]  
                       
[--force -f]  
                       
[--accept-eula -a]
```
### <a name="examples"></a>範例
引導式 BDC 設定初始化體驗；您將會接收到所需值的提示。
```bash
azdata bdc config init
```
搭配引數的 BDC 設定初始化，其會在 ./custom 中建立 aks-dev-test 的設定檔。
```bash
azdata bdc config init --source aks-dev-test --target custom
```
### <a name="optional-parameters"></a>選擇性參數
#### `--target -t`
您要放置設定檔的檔案路徑，預設為 <cwd>/custom。
#### `--source -s`
組態設定檔來源：['openshift-dev-test', 'aro-dev-test-ha', 'aks-dev-test', 'openshift-prod', 'aks-dev-test-ha', 'kubeadm-prod', 'aro-dev-test', 'kubeadm-dev-test']
#### `--force -f`
強制覆寫目標檔案。
#### `--accept-eula -a`
您接受授權條款嗎? [yes/no]。 如果您不想要使用此引數，可以將環境變數 ACCEPT_EULA 設定為 'yes'。 此產品的授權條款可在 https://aka.ms/eula-azdata-en 檢視。
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
## <a name="azdata-bdc-config-list"></a>azdata bdc config list
列出可在 `bdc config init` 中使用的設定檔選項
```bash
azdata bdc config list [--config-profile -c] 
                       [--type -t]  
                       
[--accept-eula -a]
```
### <a name="examples"></a>範例
顯示所有可用的設定檔名稱。
```bash
azdata bdc config list
```
顯示特定設定檔的 json。
```bash
azdata bdc config list --config-profile aks-dev-test
```
### <a name="optional-parameters"></a>選擇性參數
#### `--config-profile -c`
預設組態設定檔：['openshift-dev-test', 'aro-dev-test-ha', 'aks-dev-test', 'openshift-prod', 'aks-dev-test-ha', 'kubeadm-prod', 'aro-dev-test', 'kubeadm-dev-test']
#### `--type -t`
您想要的設定類型。
#### `--accept-eula -a`
您接受授權條款嗎? [yes/no]。 如果您不想要使用此引數，可以將環境變數 ACCEPT_EULA 設定為 'yes'。 此產品的授權條款可在 https://aka.ms/eula-azdata-en 檢視。
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
## <a name="azdata-bdc-config-show"></a>azdata bdc config show
顯示 BDC 目前的設定，或您指定的本機檔案設定，亦即 custom/bdc.json。 如果您只想要取得某個區段，該命令也可以接受 json 路徑。  您也可以指定要輸出至的目標檔案。  如果未指定目標檔案，系統只會將它輸出至終端機。
```bash
azdata bdc config show [--config-file -c] 
                       [--target -t]  
                       
[--json-path -j]  
                       
[--force -f]
```
### <a name="examples"></a>範例
在主控台中顯示 BDC 設定
```bash
azdata bdc config show
```
在本機設定檔中，在簡單 json 金鑰路徑的結尾取得值。
```bash
azdata bdc config show --config-file custom-config/bdc.json --json-path "metadata.name" --target section.json
```
在本機設定檔中，取得服務中的資源
```bash
azdata bdc config show --config-file custom-config/bdc.json --json-path "$.spec.services.sql.resources" --target section.json
```
### <a name="optional-parameters"></a>選擇性參數
#### `--config-file -c`
巨量資料叢集設定檔路徑 (若您不想使用目前所登入之叢集的設定，亦即 custom/bdc.json)
#### `--target -t`
要用來儲存結果的輸出檔案。 預設：導向至 stdout。
#### `--json-path -j`
導向您在設定中想要之區段或值 (也就是 key1.key2.key3) 的 json 金鑰路徑。 使用 jsonpath 查詢語言 (https://jsonpath.com/ )，例如：-j '$.spec.pools[?(@.spec.type == "Master")]..endpoints'
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
## <a name="azdata-bdc-config-add"></a>azdata bdc config add
將值新增至設定檔中的 json 路徑。  所有下列範例都是以 Bash 提供。  如果您是使用另一個命令列，請留意您可能需要適當地逸出引號。  或者，您可以使用修補檔案功能。
```bash
azdata bdc config add --config-file -c 
                      --json-values -j
```
### <a name="examples"></a>範例
範例 1 - 新增控制平面儲存體。
```bash
azdata bdc config add --config-file custom/control.json --json-values "spec.storage={"accessMode":"ReadWriteOnce","className":"managed-premium","size":"10Gi"}"
```
### <a name="required-parameters"></a>必要參數
#### `--config-file -c`
您想要設定之設定的巨量資料叢集設定檔路徑 (也就是 custom/bdc.json)
#### `--json-values -j`
針對值之 json 路徑的機碼值組清單：key1.subkey1=value1,key2.subkey2=value2. 您可以提供內嵌 json 值，例如 key='{"kind":"cluster","name":"test-cluster"}'，或是提供檔案路徑，例如 key=./values.json。 新增作業不支援條件。  若要提供的內嵌值是包含 '=' 及 ',' 的機碼值組，請避免使用這些字元。  例如 key1="key2\=val2\,key3\=val3"。 請參閱 http://jsonpatch.com/ \(英文\) 以取得路徑外觀的範例。  如果您想要存取陣列，您必須指出索引 (例如 key.0=value) 來這麼做
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
## <a name="azdata-bdc-config-remove"></a>azdata bdc config remove
移除設定檔中 json 路徑的值。  所有下列範例都是以 Bash 提供。  如果您是使用另一個命令列，請留意您可能需要適當地逸出引號。  或者，您可以使用修補檔案功能。
```bash
azdata bdc config remove --config-file -c 
                         --json-path -j
```
### <a name="examples"></a>範例
範例 1 - 移除控制平面儲存體。
```bash
azdata bdc config remove --config-file custom/control.json --json-path ".spec.storage"
```
### <a name="required-parameters"></a>必要參數
#### `--config-file -c`
您想要設定之設定的巨量資料叢集設定檔路徑 (也就是 custom/bdc.json)
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
## <a name="azdata-bdc-config-replace"></a>azdata bdc config replace
取代設定檔中 json 路徑的值。  所有下列範例都是以 Bash 提供。  如果您是使用另一個命令列，請留意您可能需要適當地逸出引號。  或者，您可以使用修補檔案功能。
```bash
azdata bdc config replace --config-file -c 
                          --json-values -j
```
### <a name="examples"></a>範例
範例 1 - 取代單一端點 (控制器端點) 的連接埠。
```bash
azdata bdc config replace --config-file custom/control.json --json-values "$.spec.endpoints[?(@.name=="Controller")].port=30080"
```
範例 2 - 取代控制平面儲存體。
```bash
azdata bdc config replace --config-file custom/control.json --json-values "spec.storage={"accessMode":"ReadWriteOnce","className":"managed-premium","size":"10Gi"}"
```
範例 3 - 取代儲存體 - 0 資源規格，包括複本。
```bash
azdata bdc config replace --config-file custom/bdc.json --json-values "$.spec.resources.storage-0.spec={"replicas": 2,"storage": {"className": "managed-premium","size": "10Gi","accessMode": "ReadWriteOnce"},"type": "Storage"}"
```
### <a name="required-parameters"></a>必要參數
#### `--config-file -c`
您想要設定之設定的巨量資料叢集設定檔路徑 (也就是 custom/bdc.json)
#### `--json-values -j`
針對值之 json 路徑的機碼值組清單：key1.subkey1=value1,key2.subkey2=value2. 您可以提供內嵌 json 值，例如 key='{"kind":"cluster","name":"test-cluster"}'，或是提供檔案路徑，例如 key=./values.json。 取代作業可透過 jsonpath 程式庫支援條件。  若要使用此方法，請以 $ 作為路徑開頭。 這能讓您執行如-j $.key1.key2[?(@.key3=='someValue'].key4=value 的條件。 若要提供的內嵌值是包含 '=' 及 ',' 的機碼值組，請避免使用這些字元。  例如 key1="key2\=val2\,key3\=val3"。 您可以參閱底下的範例。 如需其他協助，請參閱： https://jsonpath.com/ \(英文\)
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
## <a name="azdata-bdc-config-patch"></a>azdata bdc config patch
根據指定的修補檔來修補設定檔。 請參閱 http://jsonpatch.com/ \(英文\) 以深入了解路徑的撰寫方式。 基於 jsonpath 程式庫 https://jsonpath.com/ \(英文\) 的原因，取代作業可以在其路徑中使用條件。 所有修補 json 檔案都必須以 "patch" 的機碼作為開頭，其具有修補陣列及其相對應的作業 (新增、取代、移除)、路徑及值。 「移除」作業不需要值，只需要路徑。 請參閱以下的範例。
```bash
azdata bdc config patch --config-file -c 
                        --patch-file -p
```
### <a name="examples"></a>範例
範例 1 - 搭配修補檔案取代單一端點 (控制器端點) 的連接埠。
```bash
azdata bdc config patch --config-file custom/control.json --patch ./patch.json

    Patch File Example (patch.json):
        {"patch":[{"op":"replace","path":"$.spec.endpoints[?(@.name=="Controller")].port","value":30080}]}
```
範例 2 - 搭配修補檔案取代控制平面儲存體。
```bash
azdata bdc config patch --config-file custom/control.json --patch ./patch.json

    Patch File Example (patch.json):
        {"patch":[{"op":"replace","path":".spec.storage","value":{"accessMode":"ReadWriteMany","className":"managed-premium","size":"10Gi"}}]}
```
範例 3 - 搭配修補檔案取代集區儲存體，包括複本 (存放集區)。
```bash
azdata bdc config patch --config-file custom/bdc.json --patch ./patch.json

    Patch File Example (patch.json):
        {"patch":[{"op":"replace","path":"$.spec.resources.storage-0.spec","value":{"replicas": 2,"storage": {"className": "managed-premium","size": "10Gi","accessMode": "ReadWriteOnce"},"type": "Storage"}}]}
```
### <a name="required-parameters"></a>必要參數
#### `--config-file -c`
您想要設定之設定的巨量資料叢集設定檔路徑 (也就是 custom/bdc.json)
#### `--patch-file -p`
以 jsonpatch 程式庫 http://jsonpatch.com/ \(英文\) 為基礎之修補 json 檔案的路徑。 您必須以名為 "patch" 的機碼作為修補 json 檔案的開頭，其值是您要執行之修補作業的陣列。 針對修補作業的路徑，您可以使用點標記法，例如可針對大部分作業使用的 key1.key2。 如果您想要進行取代作業，且您是要取代需要條件之陣列中的值，請透過以 $ 作為路徑開頭來使用 jsonpath 標記法。 這能讓您執行如 $.key1.key2[?(@.key3=='someValue'].key4 的條件。 請參閱以下的範例。 如需條件的其他協助，請參閱： https://jsonpath.com/ \(英文\)。
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
## <a name="azdata-bdc-config-set"></a>azdata bdc config set
這是進行中的工作，可設定巨量資料叢集的組態。
```bash
azdata bdc config set --name -n 
                      
```
### <a name="examples"></a>範例
設定巨量資料叢集的組態測試。
```bash
azdata config set --name test
```
### <a name="required-parameters"></a>必要參數
#### `--name -n`
巨量資料叢集名稱，用於 kubernetes 命名空間。
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
## <a name="azdata-bdc-config-upgrade"></a>azdata bdc config upgrade
這是進行中的工作，可升級巨量資料叢集的組態。
```bash
azdata bdc config upgrade --name -n 
                          
```
### <a name="examples"></a>範例
巨量資料叢集的組態升級測試。
```bash
azdata config upgrade --name test
```
### <a name="required-parameters"></a>必要參數
#### `--name -n`
巨量資料叢集名稱，用於 kubernetes 命名空間。
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

如需其他 `azdata` 命令的詳細資訊，請參閱 [azdata 參考](reference-azdata.md)。 如需如何安裝 `azdata` 工具的詳細資訊，請參閱[安裝 azdata 來管理 SQL Server 2019 巨量資料叢集](../install/deploy-install-azdata.md)。
