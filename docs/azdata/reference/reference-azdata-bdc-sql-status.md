---
title: azdata bdc sql status 參考
titleSuffix: SQL Server big data clusters
description: azdata bdc sql status 命令的參考文章。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: seanw
ms.date: 09/22/2020
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: d08f72b30a9fa3c278a0562d406ad439346de2e9
ms.sourcegitcommit: 29a2be59c56f8a4b630af47760ef38d2bf56a3eb
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/22/2020
ms.locfileid: "92358386"
---
# <a name="azdata-bdc-sql-status"></a>azdata bdc sql status

適用於 [!INCLUDE [azure-data-cli-azdata](../../includes/azure-data-cli-azdata.md)]

下列文章提供 **azdata** 工具中 **sql** 命令的參考。 如需其他 **azdata** 命令的詳細資訊，請參閱 [azdata 參考](reference-azdata.md)

## <a name="commands"></a>命令

|命令|說明|
| --- | --- |
[azdata bdc hdfs status show](#azdata-bdc-sql-status-show) | Sql-server 服務狀態。
## <a name="azdata-bdc-sql-status-show"></a>azdata bdc hdfs status show
Sql-server 服務狀態。
```bash
azdata bdc sql status show [--resource -r] 
                           [--all -a]
```
### <a name="examples"></a>範例
取得 SQL 服務的狀態。
```bash
azdata bdc sql status show
```
取得含所有執行個體的 SQL 服務狀態。
```bash
azdata bdc sql status show --all
```
取得 SQL 服務內主要資源的狀態。
```bash
azdata bdc sql status show --resource master
```
### <a name="optional-parameters"></a>選擇性參數
#### `--resource -r`
取得此服務中的此資源。
#### `--all -a`
顯示此服務中各項資源的所有執行個體。
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

