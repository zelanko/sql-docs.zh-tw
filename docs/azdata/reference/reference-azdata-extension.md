---
title: azdata 延伸模組參考
titleSuffix: SQL Server big data clusters
description: azdata 延伸模組命令的參考文章。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: seanw
ms.date: 09/22/2020
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 07862632feeb4fc33f82597cf7d2b1319f320776
ms.sourcegitcommit: 29a2be59c56f8a4b630af47760ef38d2bf56a3eb
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/22/2020
ms.locfileid: "92358141"
---
# <a name="azdata-extension"></a>azdata 延伸模組

適用於 [!INCLUDE [azure-data-cli-azdata](../../includes/azure-data-cli-azdata.md)]

下列文章提供 **azdata** 工具中 **sql** 命令的參考。 如需其他 **azdata** 命令的詳細資訊，請參閱 [azdata 參考](reference-azdata.md)

## <a name="commands"></a>命令

|命令|說明|
| --- | --- |
[azdata extension add](#azdata-extension-add) | 新增延伸模組。
[azdata extension remove](#azdata-extension-remove) | 移除延伸模組。
[azdata extension list](#azdata-extension-list) | 列出所有已安裝的延伸模組。
## <a name="azdata-extension-add"></a>azdata extension add
新增延伸模組。
```bash
azdata extension add --source -s 
                     [--index]  
                     
[--pip-proxy]  
                     
[--pip-extra-index-urls]  
                     
[--yes -y]
```
### <a name="examples"></a>範例
從 URL 新增延伸模組。
```bash
azdata extension add --source https://contoso.com/some_ext-0.0.1-py2.py3-none-any.whl```
Add extension from local disk.
```bash
azdata extension add --source ~/some_ext-0.0.1-py2.py3-none-any.whl```
Add extension from local disk and use pip proxy for dependencies.
```bash
azdata extension add --source ~/some_ext-0.0.1-py2.py3-none-any.whl --pip-proxy https://user:pass@proxy.server:8080
```
### <a name="required-parameters"></a>必要參數
#### `--source -s`
磁碟上的延伸模組路徑或延伸模組的 URL
### <a name="optional-parameters"></a>選擇性參數
#### `--index`
Python Package Index 的基底 URL (預設為 https://pypi.org/simple) 。 這應該指向符合 PEP 503 規範的存放庫 (簡易存放庫 API)，或以相同格式顯示的本機目錄。
#### `--pip-proxy`
用於延伸模組相依性的 pip proxy，格式為 [user:passwd@]proxy.server:port
#### `--pip-extra-index-urls`
要使用之套件索引的額外 URL 清單 (以空格分隔)。 這應該指向符合 PEP 503 規範的存放庫 (簡易存放庫 API)，或以相同格式顯示的本機目錄。
#### `--yes -y`
不提示確認。
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
## <a name="azdata-extension-remove"></a>azdata extension remove
移除延伸模組。
```bash
azdata extension remove --name -n 
                        [--yes -y]
```
### <a name="examples"></a>範例
移除延伸模組。
```bash
azdata extension remove --name some-ext
```
### <a name="required-parameters"></a>必要參數
#### `--name -n`
延伸模組的名稱
### <a name="optional-parameters"></a>選擇性參數
#### `--yes -y`
不提示確認。
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
## <a name="azdata-extension-list"></a>azdata extension list
列出所有已安裝的延伸模組。
```bash
azdata extension list 
```
### <a name="examples"></a>範例
列出延伸模組。
```bash
azdata extension list
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

