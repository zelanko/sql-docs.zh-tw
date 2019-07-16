---
title: mssqlctl bdc 組態區段參考
titleSuffix: SQL Server big data clusters
description: Mssqlctl bdc 組態區段指令的參考文件。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 06/26/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 3f3ba7854b4df63495926e4cc207de7cbe6a9378
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67958196"
---
# <a name="mssqlctl-bdc-config-section"></a>mssqlctl bdc 組態區段

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

下列文章提供的參考**bdc 組態區段**中的命令**mssqlctl**工具。 如需其他詳細資訊**mssqlctl**命令，請參閱[mssqlctl 參考](reference-mssqlctl.md)。

## <a name="commands"></a>命令
|     |     |
| --- | --- |
[mssqlctl bdc 組態 區段顯示](#mssqlctl-bdc-config-section-show) | 從組態設定檔中取得的區段。
[mssqlctl bdc 組態區段組中](#mssqlctl-bdc-config-section-set) | 設定的組態設定檔的區段。
## <a name="mssqlctl-bdc-config-section-show"></a>mssqlctl bdc 組態 區段顯示
從選取的組態設定檔，根據指定的 json 路徑中取得指定的區段。
```bash
mssqlctl bdc config section show --json-path -j 
                                 --config-profile -c  
                                 [--target -t]  
                                 [--force -f]
```
### <a name="examples"></a>範例
取得值，以簡單的 json 索引鍵路徑的結尾。
```bash
mssqlctl bdc config section show --config-profile custom-config --json-path 'metadata.name' --target section.json
```
取得值，這個值結尾的條件式的 json 索引鍵路徑
```bash
mssqlctl bdc config section show --config-profile custom-config  --json-path '$.spec.pools[?(@.spec.type=="Storage")].spec' --target section.json
```
### <a name="required-parameters"></a>必要參數
#### `--json-path -j`
您想從組態設定檔的 cluster.json 檔案，也就是 key1.key2.key3 通往區段或值的 json 路徑。 使用 jsonpath 查詢語言， https://github.com/h2non/jsonpath-ng ，例如:-j ' $。 spec.pools [嗎？ (@.spec.type = ="Master")]...端點 '
#### `--config-profile -c`
BDC 組態設定檔的路徑。
### <a name="optional-parameters"></a>選擇性參數
#### `--target -t`
放置您想在此要區段檔案的檔案路徑。 預設值： 導向至 stdout。
#### `--force -f`
強制覆寫目標檔案。
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
## <a name="mssqlctl-bdc-config-section-set"></a>mssqlctl bdc 組態區段組中
選取的組態設定檔，根據指定的 json 路徑中設定的指定的區段。  在 Bash 中，會提供所有 examplesbelow。  如果使用另一個命令列，請留意，您可能需要 escapequotations 適當。  或者，您可以使用的修補程式檔案的功能。
```bash
mssqlctl bdc config section set --config-profile -c 
                                [--json-values -j]  
                                [--patch-file -p]
```
### <a name="examples"></a>範例
範例 1 （內嵌）-設定連接埠的單一端點 （控制器端點）。
```bash
mssqlctl bdc config section set --config-profile custom-config --json-values '$.spec.controlPlane.spec.endpoints[?(@.name=="Controller")].port=30080'
```
範例 1 （修補程式）-設定修補程式檔案的單一端點 （控制器端點） 的連接埠。
```bash
mssqlctl bdc config section set --config-profile custom-config --patch ./patch.json

    Patch File Example (patch.json): 
        {"patch":[{"op":"replace","path":"$.spec.controlPlane.spec.endpoints[?(@.name=='Controller')].port","value":30080}]}
```
範例 2 （內嵌）-設定控制平面儲存體。
```bash
mssqlctl bdc config section set --config-profile custom-config --json-values 'spec.controlPlane.spec.storage=spec.controlPlane.spec.storage={"accessMode":"ReadWriteOnce","className":"managed-premium","size":"10Gi"}'
```
範例 2 (patch)-設定控制平面儲存體與修補程式檔案。
```bash
mssqlctl bdc config section set --config-profile custom-config --patch ./patch.json

    Patch File Example (patch.json): 
        {"patch":[{"op":"replace","path":"spec.controlPlane.spec.storage","value":{"accessMode":"ReadWriteMany","className":"managed-premium","size":"10Gi"}}]}
```
例如 3(inline)-設定集區儲存體，包括複本 （儲存體集區）。
```bash
mssqlctl bdc config section set --config-profile custom-config --json-values '$.spec.pools[?(@.spec.type == "Storage")].spec={"replicas": 2,"storage": {"className": "managed-premium","size": "10Gi","accessMode": "ReadWriteOnce"},"type": "Storage"}'
```
範例 3 (patch)-設定集區儲存體，包括與修補程式檔案的複本 （儲存體集區）。
```bash
mssqlctl bdc config section set --config-profile custom-config --patch ./patch.json

    Patch File Example (patch.json): 
        {"patch":[{"op":"replace","path":"$.spec.pools[?(@.spec.type == 'Storage')].spec","value":{"replicas": 2,"storage": {"className": "managed-premium","size": "10Gi","accessMode": "ReadWriteOnce"},"type": "Storage"}}]}
```
### <a name="required-parameters"></a>必要參數
#### `--config-profile -c`
BDC 組態設定檔路徑，在您想要設定的組態
### <a name="optional-parameters"></a>選擇性參數
#### `--json-values -j`
值的 json 路徑的機碼值組清單： key1.subkey1=value1,key2.subkey2=value2。 您可能會提供內嵌的 json 值這類： 機碼 ='{「 類型 」: 「 叢集 」，"name": [測試叢集]}' 或提供檔案路徑，例如 key=./values.json。 如果您想要設定值，需要條件，請使用 jsonpath 標記法，以開始您的路徑為 $。 這可讓您執行的條件，例如-j $。 key1.key2 [嗎？ (@.key3= = 'someValue'].key4 = value。 您可能會看到下列的範例。 如需其他協助，請參閱： https://jsonpath.com/
#### `--patch-file -p`
Jsonpatch 程式庫都根據修補程式 json 檔案的路徑： http://jsonpatch.com/ 。 您必須使用金鑰，稱為 「 修補 」，其值是您想要進行修補作業的陣列，來啟動您修補程式的 json 檔案。 修補作業的路徑，您可以使用點標記法，例如 key1.key2 進行大部分的操作。 如果您想要執行取代作業，而且您要取代需要條件式陣列中的值，請使用 jsonpath 標記法，以開始您的路徑為 $。 這可讓您執行的條件，例如 $。 key1.key2 [嗎？ (@.key3= = 'someValue'].key4。 請參閱下面的範例。 如需其他協助，請參閱： https://jsonpath.com/ 。
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