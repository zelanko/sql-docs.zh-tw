---
title: azdata arc postgres endpoint reference
titleSuffix: SQL Server big data clusters
description: azdata arc postgres endpoint 命令的參考文章。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: seanw
ms.date: 09/22/2020
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 42e5144ca4cfd3544e9a93a5464bea531af21187
ms.sourcegitcommit: d56f1eca807c55cf606a6316f3872585f014fec1
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/22/2020
ms.locfileid: "90942395"
---
# <a name="azdata-arc-postgres-endpoint"></a>azdata arc postgres endpoint

適用於 `azdata`

下列文章提供 **azdata** 工具中 **sql** 命令的參考。 如需其他 **azdata** 命令的詳細資訊，請參閱 [azdata 參考](reference-azdata.md)

## <a name="commands"></a>命令

|命令|描述|
| --- | --- |
[azdata arc postgres endpoint list](#azdata-arc-postgres-endpoint-list) | 列出 PostgreSQL 伺服器群組端點。
## <a name="azdata-arc-postgres-endpoint-list"></a>azdata arc postgres endpoint list
列出 PostgreSQL 伺服器群組端點。
```bash
azdata arc postgres endpoint list --name -n 
                                  [--engine-version -ev]
```
### <a name="examples"></a>範例
列出 PostgreSQL 伺服器群組端點。
```bash
azdata arc postgres endpoint list -n postgres01
```
### <a name="required-parameters"></a>必要參數
#### `--name -n`
PostgreSQL 伺服器群組的名稱。
### <a name="optional-parameters"></a>選擇性參數
#### `--engine-version -ev`
當不同引擎版本的兩個伺服器群組具有相同名稱時，可以將 --engine-version 與 --name 搭配使用，以識別 PostgreSQL 超大規模資料庫伺服器群組。 --engine-version 是選擇性的，在用來識別伺服器群組時，必須是 11 或 12。
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

