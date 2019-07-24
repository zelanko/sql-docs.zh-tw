---
title: azdata bdc 設定參考
titleSuffix: SQL Server big data clusters
description: Azdata bdc 命令的參考文章。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: ed777391af3695da69e04c0e2693cff912c76771
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/23/2019
ms.locfileid: "68426288"
---
# <a name="azdata-bdc-config"></a>azdata bdc 設定

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

下列文章提供**azdata**工具中**bdc**設定命令的參考。 如需其他**azdata**命令的詳細資訊, 請參閱[azdata 參考](reference-azdata.md)。

## <a name="commands"></a>命令
|     |     |
| --- | --- |
[azdata bdc config init](#azdata-bdc-config-init) | 初始化可與叢集建立搭配使用的 Big Data 叢集設定檔。
[azdata bdc 設定清單](#azdata-bdc-config-list) | 列出可用的設定設定檔選項。
[azdata bdc config show](#azdata-bdc-config-show) | 顯示 BDC 的目前設定, 或您指定的本機檔案 (也就是自訂/cluster. json) 的設定檔。
[azdata bdc config add](#azdata-bdc-config-add) | 在設定檔中新增 json 路徑的值。
[azdata bdc 設定移除](#azdata-bdc-config-remove) | 移除設定檔中 json 路徑的值。
[azdata bdc config replace](#azdata-bdc-config-replace) | 取代設定檔中 json 路徑的值。
[azdata bdc 設定修補程式](#azdata-bdc-config-patch) | 修補以 json 修補程式檔案為基礎的設定檔。
## <a name="azdata-bdc-config-init"></a>azdata bdc config init
初始化可與叢集建立搭配使用的 Big Data 叢集設定檔。 設定設定檔的特定來源可以在3個選項的引數中指定。
```bash
azdata bdc config init [--target -t] 
                       [--source -s]  
                       [--force -f]  
                       [--accept-eula -a]
```
### <a name="examples"></a>範例
引導式 BDC 設定 init 體驗-您將會收到所需值的提示。
```bash
azdata bdc config init
```
具有引數的 BDC 設定 init, 會在/custom. 中建立 aks-dev-test 的設定設定檔。
```bash
azdata bdc config init --source aks-dev-test --target custom
```
### <a name="optional-parameters"></a>選擇性參數
#### `--target -t`
您想要放置設定檔的檔案路徑, 預設為使用自訂-config.xml 的 cwd。
#### `--source -s`
設定檔來源: [' aks-開發/測試 ', ' kubeadm-開發/測試 ', ' minikube-開發/測試 ']
#### `--force -f`
強制覆寫目標檔案。
#### `--accept-eula -a`
您接受授權條款嗎？ [是/否]。 如果您不想要使用這個 arg, 您可以將環境變數 ACCEPT_EULA 設定為 [是]。 此產品的授權條款可于 https://aka.ms/azdata-eula 查看。
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
## <a name="azdata-bdc-config-list"></a>azdata bdc 設定清單
列出可用的設定設定檔選項, 以用於`bdc config init`
```bash
azdata bdc config list [--config-profile -c] 
                       [--type -t]  
                       [--accept-eula -a]
```
### <a name="examples"></a>範例
顯示所有可用的設定設定檔名稱。
```bash
azdata bdc config list
```
顯示特定設定設定檔的 json。
```bash
azdata bdc config list --config-profile aks-dev-test
```
### <a name="optional-parameters"></a>選擇性參數
#### `--config-profile -c`
預設設定檔: [' aks-開發/測試 ', ' kubeadm-開發/測試 ', ' minikube-開發/測試 ']
#### `--type -t`
您想要查看的設定類型。
`cluster`
#### `--accept-eula -a`
您接受授權條款嗎？ [是/否]。 如果您不想要使用這個 arg, 您可以將環境變數 ACCEPT_EULA 設定為 [是]。 此產品的授權條款可于 https://aka.ms/azdata-eula 查看。
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
## <a name="azdata-bdc-config-show"></a>azdata bdc config show
顯示 BDC 的目前設定, 或您指定的本機檔案 (也就是自訂/cluster. json) 的設定檔。 如果您只想要取得區段, 此命令也可以接受 json 路徑。  您也可以指定要輸出至的目標檔案。  如果未指定目標檔案, 它只會輸出到終端機。
```bash
azdata bdc config show [--config-file -c] 
                       [--target -t]  
                       [--json-path -j]  
                       [--force -f]
```
### <a name="examples"></a>範例
在您的主控台中顯示 BDC 設定
```bash
azdata bdc config show
```
在本機設定檔案中, 取得簡單 json 金鑰路徑結尾的值。
```bash
azdata bdc config show --config-file custom-config/cluster.json --json-path 'metadata.name' --target section.json
```
在本機設定檔中, 使用條件式的 json 索引鍵路徑結尾取得值
```bash
azdata bdc config show --config-file custom-config/cluster.json  --json-path '$.spec.pools[?(@.spec.type=="Storage")].spec' --target section.json
```
### <a name="optional-parameters"></a>選擇性參數
#### `--config-file -c`
如果您不想要 currentlylogged 到的叢集設定 (也就是自訂/cluster), 則需要海量資料叢集設定檔案路徑。
#### `--target -t`
用來儲存結果的輸出檔。 預設值: 導向至 stdout。
#### `--json-path -j`
Json 金鑰路徑, 它會從設定中導向到您想要的區段或值, 例如 key1. key3。 會使用 jsonpath 查詢語言, https://jsonpath.com/ 例如:-j ' $. 集區 [？ (@.spec.type = = "Master")].。終點
#### `--force -f`
強制覆寫目標檔案。
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
## <a name="azdata-bdc-config-add"></a>azdata bdc config add
將值新增至設定檔中的 json 路徑。  以下是 Bash 中提供的所有範例。  如果使用另一個命令列, 請注意, 您可能需要適當地 escapequotations。  或者, 您可以使用修補檔案功能。
```bash
azdata bdc config add --config-file -c 
                      --json-values -j
```
### <a name="examples"></a>範例
Ex 1-新增控制平面儲存區。
```bash
azdata bdc config add --config-file custom/control.json --json-values 'spec.storage={"accessMode":"ReadWriteOnce","className":"managed-premium","size":"10Gi"}'
```
### <a name="required-parameters"></a>必要參數
#### `--config-file -c`
您想要設定之設定檔的 Big data cluster config 檔案路徑, 亦即自訂/cluster json
#### `--json-values -j`
值的 json 路徑索引鍵值組清單: key1. subkey1 = value1, key2. subkey2 = value2。 您可以提供內嵌 json 值, 例如: key = ' {"kind": "cluster", "name": "test-cluster"} "或提供檔案路徑, 例如 key =./values.json。 [新增] 不支援條件。  如需 http://jsonpatch.com/ 路徑外觀的範例, 請參閱。  如果您想要存取陣列, 您必須藉由指示索引來執行此動作, 例如 key. 0 = value。
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
## <a name="azdata-bdc-config-remove"></a>azdata bdc 設定移除
移除設定檔中 json 路徑的值。  以下是 Bash 中提供的所有範例。  如果使用另一個命令列, 請注意, 您可能需要適當地 escapequotations。  或者, 您可以使用修補檔案功能。
```bash
azdata bdc config remove --config-file -c 
                         --json-path -j
```
### <a name="examples"></a>範例
Ex 1-移除控制平面儲存區。
```bash
azdata bdc config remove --config-file custom/control.json --json-path '.spec.storage'
```
### <a name="required-parameters"></a>必要參數
#### `--config-file -c`
您想要設定之設定檔的 Big data cluster config 檔案路徑, 亦即自訂/cluster json
#### `--json-path -j`
以 jsonpatch 程式庫為基礎的 json 路徑清單, 指出您想要移除的值, 例如: key1. subkey1、key2 subkey2。 [移除] 不支援條件。 如需 http://jsonpatch.com/ 路徑外觀的範例, 請參閱。  如果您想要存取陣列, 您必須藉由指示索引來執行此動作, 例如 key. 0 = value。
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
## <a name="azdata-bdc-config-replace"></a>azdata bdc config replace
取代設定檔中 json 路徑的值。  所有 examplesbelow 都是在 Bash 中提供。  如果使用另一個命令列, 請注意, 您可能需要適當地 escapequotations。  或者, 您可以使用修補檔案功能。
```bash
azdata bdc config replace --config-file -c 
                          --json-values -j
```
### <a name="examples"></a>範例
Ex 1-取代單一端點 (控制器端點) 的埠。
```bash
azdata bdc config replace --config-file custom/control.json --json-values '$.spec.endpoints[?(@.name=="Controller")].port=30080'
```
Ex 2-取代控制平面儲存區。
```bash
azdata bdc config replace --config-file custom/control.json --json-values 'spec.storage={"accessMode":"ReadWriteOnce","className":"managed-premium","size":"10Gi"}'
```
Ex 3-取代集區儲存體, 包括複本 (儲存集區)。
```bash
azdata bdc config replace --config-file custom/cluster.json --json-values '$.spec.pools[?(@.spec.type == "Storage")].spec={"replicas": 2,"storage": {"className": "managed-premium","size": "10Gi","accessMode": "ReadWriteOnce"},"type": "Storage"}'
```
### <a name="required-parameters"></a>必要參數
#### `--config-file -c`
您想要設定之設定檔的 Big data cluster config 檔案路徑, 亦即自訂/cluster json
#### `--json-values -j`
值的 json 路徑索引鍵值組清單: key1. subkey1 = value1, key2. subkey2 = value2。 您可以提供內嵌 json 值, 例如: key = ' {"kind": "cluster", "name": "test-cluster"} "或提供檔案路徑, 例如 key =./values.json。 Replace 透過 jsonpath 程式庫來支援條件。  若要使用此方法, 請使用 $ 來啟動您的路徑。 這可讓您執行條件, 例如-j $. key1. key2 [？ (@.key3= = ' someValue ']。 key4 = value。 您可能會看到下列範例。 如需其他協助, 請參閱: https://jsonpath.com/
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
## <a name="azdata-bdc-config-patch"></a>azdata bdc 設定修補程式
根據指定的修補檔案修補設定檔。 請參閱 http://jsonpatch.com/ 以進一步瞭解路徑的撰寫方式。 取代作業可以在其路徑中使用條件, 因為 jsonpath 程式庫 https://jsonpath.com/ 。 所有修補程式 json 檔案的開頭都必須是 "patch" 的索引鍵, 其中包含修補程式陣列及其對應的 op (add、replace、remove)、path 和 value。 「移除」 op 不需要值, 只要是路徑。 請參閱下列範例。
```bash
azdata bdc config patch --config-file -c 
                        --patch-file -p
```
### <a name="examples"></a>範例
Ex 1-以 patch 檔案取代單一端點 (控制器端點) 的埠。
```bash
azdata bdc config patch --config-file custom/control.json --patch ./patch.json

    Patch File Example (patch.json): 
        {"patch":[{"op":"replace","path":"$.spec.endpoints[?(@.name=='Controller')].port","value":30080}]}
```
Ex 2-以 patch 檔案取代控制平面儲存區。
```bash
azdata bdc config patch --config-file custom/control.json --patch ./patch.json

    Patch File Example (patch.json): 
        {"patch":[{"op":"replace","path":".spec.storage","value":{"accessMode":"ReadWriteMany","className":"managed-premium","size":"10Gi"}}]}
```
Ex 3-取代集區儲存體, 包括具有修補程式檔案的複本 (存放集區)。
```bash
azdata bdc config patch --config-file custom/cluster.json --patch ./patch.json

    Patch File Example (patch.json): 
        {"patch":[{"op":"replace","path":"$.spec.pools[?(@.spec.type == 'Storage')].spec","value":{"replicas": 2,"storage": {"className": "managed-premium","size": "10Gi","accessMode": "ReadWriteOnce"},"type": "Storage"}}]}
```
### <a name="required-parameters"></a>必要參數
#### `--config-file -c`
您想要設定之設定檔的 Big data cluster config 檔案路徑, 亦即自訂/cluster json
#### `--patch-file -p`
以 jsonpatch 程式庫為基礎之修補程式 json 檔案的路徑: http://jsonpatch.com/ 。 您必須使用名為 "patch" 的金鑰來啟動修補程式 json 檔案, 其值為您想要進行的修補作業陣列。 針對修補作業的路徑, 您可以使用點標記法 (例如, key1. key2) 來進行大部分的作業。 如果您想要執行取代作業, 而您要取代需要條件的陣列中的值, 請使用 jsonpath 標記法, 並以 $ 開頭您的路徑。 這可讓您執行如 $. key1. key2 [？ (@.key3= = ' someValue ']. key4。 請參閱下列範例。 如需條件的其他協助, 請參閱 https://jsonpath.com/:。
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