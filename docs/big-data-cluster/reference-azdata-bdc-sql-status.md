---
title: azdata bdc sql 狀態參考
titleSuffix: SQL Server big data clusters
description: Azdata bdc sql status 命令的參考文章。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/28/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: c5c2cdd924f266400125080d21d0461d5f599190
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2019
ms.locfileid: "70158253"
---
# <a name="azdata-bdc-sql-status"></a>azdata bdc sql 狀態

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]  

本文是**azdata**的參考文章。 

## <a name="commands"></a>命令
|     |     |
| --- | --- |
[azdata bdc sql 狀態顯示](#azdata-bdc-sql-status-show) | Sql server 服務狀態。
## <a name="azdata-bdc-sql-status-show"></a>azdata bdc sql 狀態顯示
Sql server 服務狀態。
```bash
azdata bdc sql status show [--resource -r] 
                           [--all -a]
```
### <a name="examples"></a>範例
取得 sql 服務的狀態。
```bash
azdata bdc sql status show
```
取得具有所有實例的 sql 服務狀態。
```bash
azdata bdc sql status show --all
```
取得 sql 服務內主要資源的狀態。
```bash
azdata bdc sql status show --resource master
```
### <a name="optional-parameters"></a>選擇性參數
#### `--resource -r`
在此服務中取得此資源。
#### `--all -a`
顯示服務內每個資源的所有實例。
### <a name="global-arguments"></a>全域引數
#### `--debug`
增加記錄詳細資訊，以顯示所有偵錯記錄。
#### `--help -h`
顯示此說明訊息並結束。
#### `--output -o`
輸出格式。  允許的值：json、jsonc、table、tsv。  預設值：json。
#### `--query -q`
JMESPath 查詢字串。 如需詳細資訊和範例，請參閱 [http://jmespath.org/](http://jmespath.org/])。
#### `--verbose`
增加記錄詳細資訊。 使用 --debug 來取得完整偵錯記錄。

## <a name="next-steps"></a>後續步驟

- 如需其他 **azdata** 命令的詳細資訊，請參閱 [azdata 參考](reference-azdata.md)。 

- 如需如何安裝 **azdata** 工具的詳細資訊，請參閱[安裝 azdata 來管理 SQL Server 2019 巨量資料叢集](deploy-install-azdata.md)。
