---
title: azdata bdc spark status 參考
titleSuffix: SQL Server big data clusters
description: azdata bdc spark status 命令的參考文章。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 06/22/2020
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 971854997519e4ef9b1e11d0063da1bbc2c583e4
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/28/2020
ms.locfileid: "87243469"
---
# <a name="azdata-bdc-spark-status"></a>azdata bdc spark status

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

下文提供 `azdata` 工具中 `sql` 命令的參考。 如需其他 `azdata` 命令的詳細資訊，請參閱 [azdata 參考](reference-azdata.md)。

## <a name="commands"></a>命令
| 命令 | 說明 |
| --- | --- |
[azdata bdc spark status show](#azdata-bdc-spark-status-show) | Spark 服務狀態。
## <a name="azdata-bdc-spark-status-show"></a>azdata bdc spark status show
Spark 服務狀態。
```bash
azdata bdc spark status show [--resource -r] 
                             [--all -a]
```
### <a name="examples"></a>範例
取得 Spark 服務的狀態。
```bash
azdata bdc spark status show
```
取得含所有執行個體的 Spark 服務狀態。
```bash
azdata bdc spark status show --all
```
取得 Spark 服務內儲存體資源的狀態。
```bash
azdata bdc spark status show --resource storage-0
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

如需其他 `azdata` 命令的詳細資訊，請參閱 [azdata 參考](reference-azdata.md)。 如需如何安裝 `azdata` 工具的詳細資訊，請參閱[安裝 azdata 來管理 SQL Server 2019 巨量資料叢集](deploy-install-azdata.md)。
