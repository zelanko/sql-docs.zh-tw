---
title: azdata context 參考
titleSuffix: SQL Server big data clusters
description: azdata context 命令的參考文章。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: seanw
ms.date: 09/22/2020
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 1d48ef786389c5ef32b1f3fd49c88b0a9d3aac18
ms.sourcegitcommit: d56f1eca807c55cf606a6316f3872585f014fec1
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/22/2020
ms.locfileid: "90914736"
---
# <a name="azdata-context"></a>azdata context

適用於 `azdata`

下列文章提供 **azdata** 工具中 **sql** 命令的參考。 如需其他 **azdata** 命令的詳細資訊，請參閱 [azdata 參考](reference-azdata.md)

## <a name="commands"></a>命令

|命令|說明|
| --- | --- |
[azdata context list](#azdata-context-list) | 列出使用者設定檔中可用的內容。
[azdata context delete](#azdata-context-delete) | 從使用者設定檔刪除具有指定命名空間的內容。
[azdata context set](#azdata-context-set) | 將具有指定命名空間的內容，設定為使用者設定檔中的使用中內容。
## <a name="azdata-context-list"></a>azdata context list
您可以使用 `azdata context set` 或 `azdata context delete` 來設定或刪除其中任何一項。 若要登入至新的內容，請使用 `azdata login`。
```bash
azdata context list [--active -a] 
                    
```
### <a name="examples"></a>範例
列出使用者設定檔中所有可用的內容。
```bash
azdata context list
```
列出使用者設定檔中的使用中內容。
```bash
azdata context list --active
```
### <a name="optional-parameters"></a>選擇性參數
#### `--active -a`
僅列出目前使用中的內容。
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
## <a name="azdata-context-delete"></a>azdata context delete
如果刪除的內容為使用中，則使用者需要設定新的使用中內容。 若要查看可供設定或刪除的內容，請使用 `azdata context list`
```bash
azdata context delete --namespace -ns 
                      
```
### <a name="examples"></a>範例
刪除使用者設定檔中的 contextNamespace。
```bash
azdata context delete -n contextNamespace
```
### <a name="required-parameters"></a>必要參數
#### `--namespace -ns`
所要刪除內容的命名空間。
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
## <a name="azdata-context-set"></a>azdata context set
若要查看可供設定的內容，請使用 `azdata context list`。 如果沒有列出任何內容，則您必須登入才能在使用者設定檔 `azdata login` 中建立內容。 您登入的內容將成為使用中內容。 如果您登入多個實體，則可以使用此命令在使用中內容之間切換。 若要查看目前使用中的內容，請使用 `azdata context list --active`
```bash
azdata context set --namespace -ns 
                   
```
### <a name="examples"></a>範例
將 contextNamespace 設定為使用者設定檔中的使用中內容。
```bash
azdata context set -n contextNamespace
```
### <a name="required-parameters"></a>必要參數
#### `--namespace -ns`
所要設定內容的命名空間。
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

