---
title: azdata bdc app 狀態參考
titleSuffix: SQL Server big data clusters
description: 使用此參考文章了解 azdata 工具中的 SQL 命令，特別是 bdc app status 命令。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 06/22/2020
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: fd6288649db641bc846b8ebed3b997aa0092d36e
ms.sourcegitcommit: 883435b4c7366f06ac03579752093737b098feab
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/28/2020
ms.locfileid: "89733640"
---
# <a name="azdata-bdc-app-status"></a>azdata bdc app 狀態

[!INCLUDE[SQL Server 2019](../../includes/applies-to-version/sqlserver2019.md)]

下文提供 `azdata` 工具中 `sql` 命令的參考。 如需其他 `azdata` 命令的詳細資訊，請參閱 [azdata 參考](reference-azdata.md)。

## <a name="commands"></a>命令
| 命令 | 說明 |
| --- | --- |
[azdata bdc 應用程式狀態顯示](#azdata-bdc-app-status-show) | 應用程式服務狀態。
## <a name="azdata-bdc-app-status-show"></a>azdata bdc 應用程式狀態顯示
應用程式服務狀態。
```bash
azdata bdc app status show [--resource -r] 
                           [--all -a]
```
### <a name="examples"></a>範例
取得應用程式服務的狀態。
```bash
azdata bdc app status show
```
取得應用程式服務及其所有執行個體的狀態。
```bash
azdata bdc app status show --all
```
取得應用程式服務內 appproxy 資源的狀態。
```bash
azdata bdc app status show --resource appproxy
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

如需其他 `azdata` 命令的詳細資訊，請參閱 [azdata 參考](reference-azdata.md)。 如需如何安裝 `azdata` 工具的詳細資訊，請參閱[安裝 azdata 來管理 SQL Server 2019 巨量資料叢集](../install/deploy-install-azdata.md)。
