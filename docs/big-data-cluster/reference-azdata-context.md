---
title: azdata context 參考
titleSuffix: SQL Server big data clusters
description: azdata context 命令的參考文章。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 11/04/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: f2716a8176124539aa7caf382193359ff5435aa6
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "74820989"
---
# <a name="azdata-context"></a>azdata context

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]  

下文提供 `azdata` 工具中 `context` 命令的參考。 如需其他 `azdata` 命令的詳細資訊，請參閱 [azdata 參考](reference-azdata.md)

## <a name="commands"></a>命令
|     |     |
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
JMESPath 查詢字串。 如需詳細資訊和範例，請參閱 [http://jmespath.org/](http://jmespath.org/)。
#### `--verbose`
增加記錄詳細資訊。 使用 --debug 來取得完整偵錯記錄。
## <a name="azdata-context-delete"></a>azdata context delete
如果刪除的內容為使用中，則使用者需要設定新的使用中內容。 若要查看可供設定或刪除的內容，請使用 `azdata context list`
```bash
azdata context delete --namespace -n 
    ```
### Examples
Deletes contextNamespace from the user profile.
```bash
azdata context delete -n contextNamespace
```
### <a name="required-parameters"></a>必要參數
#### `--namespace -n`
所要刪除內容的命名空間。
### <a name="global-arguments"></a>全域引數
#### `--debug`
增加記錄詳細資訊，以顯示所有偵錯記錄。
#### `--help -h`
顯示此說明訊息並結束。
#### `--output -o`
輸出格式。  允許的值：json、jsonc、table、tsv。  預設值：json。
#### `--query -q`
JMESPath 查詢字串。 如需詳細資訊和範例，請參閱 [http://jmespath.org/](http://jmespath.org/)。
#### `--verbose`
增加記錄詳細資訊。 使用 --debug 來取得完整偵錯記錄。
## <a name="azdata-context-set"></a>azdata context set
若要查看可供設定的內容，請使用 `azdata context list`。 如果沒有列出任何內容，則您必須登入才能在使用者設定檔 `azdata login` 中建立內容。 您登入的內容將成為使用中內容。 如果您登入多個實體，則可以使用此命令在使用中內容之間切換。 若要查看目前使用中的內容，請使用 `azdata context list --active`
```bash
azdata context set --namespace -n 
 ```
### <a name="examples"></a>範例
將 contextNamespace 設定為使用者設定檔中的使用中內容。
```bash
azdata context set -n contextNamespace
```
### <a name="required-parameters"></a>必要參數
#### `--namespace -n`
所要設定內容的命名空間。
### <a name="global-arguments"></a>全域引數
#### `--debug`
增加記錄詳細資訊，以顯示所有偵錯記錄。
#### `--help -h`
顯示此說明訊息並結束。
#### `--output -o`
輸出格式。  允許的值：json、jsonc、table、tsv。  預設值：json。
#### `--query -q`
JMESPath 查詢字串。 如需詳細資訊和範例，請參閱 [http://jmespath.org/](http://jmespath.org/)。
#### `--verbose`
增加記錄詳細資訊。 使用 --debug 來取得完整偵錯記錄。

## <a name="next-steps"></a>後續步驟

如需其他 `azdata` 命令的詳細資訊，請參閱 [azdata 參考](reference-azdata.md)。 如需如何安裝 `azdata` 工具的詳細資訊，請參閱[安裝 azdata 來管理 SQL Server 2019 巨量資料叢集](deploy-install-azdata.md)。
