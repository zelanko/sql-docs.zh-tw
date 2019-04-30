---
title: mssqlctl 叢集組態區段參考
titleSuffix: SQL Server big data clusters
description: Mssqlctl 叢集組態區段指令的參考文件。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 04/23/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: d5a793e7d0fcaf782a09a4981491ef0a8d90ab5a
ms.sourcegitcommit: bd5f23f2f6b9074c317c88fc51567412f08142bb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/24/2019
ms.locfileid: "63759135"
---
# <a name="mssqlctl-cluster-config-section"></a>mssqlctl cluster config section

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

下列文章提供的參考**叢集組態區段**中的命令**mssqlctl**工具。 如需其他詳細資訊**mssqlctl**命令，請參閱[mssqlctl 參考](reference-mssqlctl.md)。

## <a name="commands"></a>命令
|     |     |
| --- | --- |
[取得 mssqlctl 叢集組態區段](#mssqlctl-cluster-config-section-get) | 從組態檔中取得的區段。
[mssqlctl 叢集組態區段組](#mssqlctl-cluster-config-section-set) | 設定組態檔的區段。
## <a name="mssqlctl-cluster-config-section-get"></a>取得 mssqlctl 叢集組態區段
從選取的組態檔，根據指定的 json 路徑中取得指定的區段。
```bash
mssqlctl cluster config section get --json-path -j 
                                    --config-file -f  
                                    [--target -t]
```
### <a name="required-parameters"></a>必要參數
#### `--json-path -j`
您想從組態檔，也就是 key1.key2.key3 通往區段或值的 json 路徑。 使用 jsonpath 查詢語言， https://github.com/h2non/jsonpath-ng，例如:-j ' $。 spec.pools [嗎？ (@.spec.type = ="Master")]...端點 '
#### `--config-file -f`
叢集設定檔的路徑。
### <a name="optional-parameters"></a>選擇性參數
#### `--target -t`
放置您想在此要區段檔案的檔案路徑。
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
## <a name="mssqlctl-cluster-config-section-set"></a>mssqlctl 叢集組態區段組
根據指定的 json 路徑所選取的組態檔中設定的指定的區段。
```bash
mssqlctl cluster config section set --config-file -f 
                                    [--json-values -j]  
                                    [--patch-file -p]
```
### <a name="required-parameters"></a>必要參數
#### `--config-file -f`
在您想要設定的組態的叢集設定檔路徑
### <a name="optional-parameters"></a>選擇性參數
#### `--json-values -j`
值的 json 路徑的機碼值組清單： key1.subkey1=value1,key2.subkey2=value2。 您可能會提供內嵌的 json 值這類： 機碼 ='{「 類型 」: 「 叢集 」，"name": [測試叢集]}' 或提供檔案路徑，例如 key=./values.json
#### `--patch-file -p`
根據 jsonpatch 程式庫和 jsonpath 修補程式 json 檔案的路徑： https://github.com/stefankoegl/python-json-patch ， https://github.com/h2non/jsonpath-ng -簡單的範例: {「 修補 」: [{"op":"add"，"path":"metadata.name"、"value":"test"}，{"op":"add"，"path":"metadata.array"、"value": [1、 2、 3]}]}請包含 「 修補 」 的索引鍵且值是您想要進行修補程式陣列。  將這類執行它。 A more complex example: {"patch": [{"op": "replace", "path": "$.spec.pools[?(@.spec.type == 'Master')]..endpoints","value": {"name":[新增端點]}}]}
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