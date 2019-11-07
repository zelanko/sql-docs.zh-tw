---
title: azdata bdc control status 參考
titleSuffix: SQL Server big data clusters
description: azdata bdc control status 命令的參考文章。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 11/04/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: ed3c104b9aea6eae06ad5f5acebb892660ca8886
ms.sourcegitcommit: 830149bdd6419b2299aec3f60d59e80ce4f3eb80
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/04/2019
ms.locfileid: "73531827"
---
# <a name="azdata-bdc-control-status"></a>azdata bdc control status

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]  

下列文章提供 `azdata` 工具中 `sql` 命令的參考。 如需其他 `azdata` 命令的詳細資訊，請參閱 [azdata 參考](reference-azdata.md)

## <a name="commands"></a>命令
|     |     |
| --- | --- |
[azdata bdc control status show](#azdata-bdc-control-status-show) | 控制服務狀態。
## <a name="azdata-bdc-control-status-show"></a>azdata bdc control status show
控制服務狀態。
```bash
azdata bdc control status show [--resource -r] 
                               [--all -a]
```
### <a name="examples"></a>範例
取得服務的狀態。
```bash
azdata bdc control status show
```
取得控制服務及所有執行個體的狀態。
```bash
azdata bdc control status show --all
```
取得控制服務內之控制資源的狀態。
```bash
azdata bdc control status show --resource control
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
JMESPath 查詢字串。 如需詳細資訊和範例，請參閱 [http://jmespath.org/](http://jmespath.org/)。
#### `--verbose`
增加記錄詳細資訊。 使用 --debug 來取得完整偵錯記錄。

## <a name="next-steps"></a>後續步驟

如需其他 `azdata` 命令的詳細資訊，請參閱 [azdata 參考](reference-azdata.md)。 如需如何安裝 `azdata` 工具的詳細資訊，請參閱[安裝 azdata 管理 SQL Server 2019 巨量資料叢集](deploy-install-azdata.md)。
