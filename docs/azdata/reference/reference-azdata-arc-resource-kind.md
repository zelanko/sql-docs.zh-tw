---
title: azdata arc resource-kind reference
titleSuffix: SQL Server big data clusters
description: azdata arc resource-kind 命令的參考文章。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: seanw
ms.date: 09/22/2020
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: fa4f920aeda7141160e3d8d6846e151585ceefac
ms.sourcegitcommit: d56f1eca807c55cf606a6316f3872585f014fec1
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/22/2020
ms.locfileid: "90942379"
---
# <a name="azdata-arc-resource-kind"></a>azdata arc resource-kind

適用於 `azdata`

下列文章提供 **azdata** 工具中 **sql** 命令的參考。 如需其他 **azdata** 命令的詳細資訊，請參閱 [azdata 參考](reference-azdata.md)

## <a name="commands"></a>命令

|命令|描述|
| --- | --- |
[azdata arc resource-kind list](#azdata-arc-resource-kind-list) | 列出 Arc 可供定義和建立的自訂資源類型。
[azdata arc resource-kind get](#azdata-arc-resource-kind-get) | 取得 Arc 資源種類的範本檔案。
## <a name="azdata-arc-resource-kind-list"></a>azdata arc resource-kind list
列出 Arc 可供定義和建立的自訂資源類型。 列出之後，您可以繼續取得定義或建立該自訂資源所需的範本檔案。
```bash
azdata arc resource-kind list 
```
### <a name="examples"></a>範例
用來列出 Arc 的可用自訂資源類型的範例命令。
```bash
azdata arc resource-kind list
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
## <a name="azdata-arc-resource-kind-get"></a>azdata arc resource-kind get
取得 Arc 資源種類的範本檔案。
```bash
azdata arc resource-kind get --kind -k 
                             [--dest -d]
```
### <a name="examples"></a>範例
用來取得 Arc 資源種類之 CRD 範本檔案的範例命令。
```bash
azdata arc resource-kind get --kind sqldb
```
### <a name="required-parameters"></a>必要參數
#### `--kind -k`
需要使用範本檔案的 Arc 資源種類。
### <a name="optional-parameters"></a>選擇性參數
#### `--dest -d`
您要用來放置範本檔案的目錄。
`template`
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

