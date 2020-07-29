---
title: azdata bdc status 參考
titleSuffix: SQL Server big data clusters
description: azdata bdc status 命令的參考文章。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 06/22/2020
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 731b8c169816b365469521e2b8c952044599b68c
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/28/2020
ms.locfileid: "87242373"
---
# <a name="azdata-bdc-status"></a>azdata bdc status

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

下文提供 `azdata` 工具中 `sql` 命令的參考。 如需其他 `azdata` 命令的詳細資訊，請參閱 [azdata 參考](reference-azdata.md)。

## <a name="commands"></a>命令
| 命令 | 說明 |
| --- | --- |
[azdata bdc status show](#azdata-bdc-status-show) | 顯示 BDC 的狀態。
## <a name="azdata-bdc-status-show"></a>azdata bdc status show
顯示 BDC 的狀態。
```bash
azdata bdc status show [--resource -r] 
                       [--all -a]
```
### <a name="examples"></a>範例
使用者登入的 BDC 狀態。
```bash
azdata bdc status show
```
包含所有資源執行個體的 BDC 狀態。
```bash
azdata bdc status show --all
```
包含控制資源之服務的 BDC 狀態。
```bash
azdata bdc status show --resource control
```
### <a name="optional-parameters"></a>選擇性參數
#### `--resource -r`
取得與此資源建立關聯的服務。
#### `--all -a`
顯示服務內每個資源的所有執行個體。
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
