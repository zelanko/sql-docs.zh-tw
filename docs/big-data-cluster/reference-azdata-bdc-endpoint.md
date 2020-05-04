---
title: azdata bdc endpoint 參考
titleSuffix: SQL Server big data clusters
description: azdata bdc endpoint 命令的參考文章。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 11/04/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 71f52b8312518cf669751d50dcc857c3d892bd98
ms.sourcegitcommit: db1b6153f0bc2d221ba1ce15543ecc83e1045453
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/30/2020
ms.locfileid: "82588074"
---
# <a name="azdata-bdc-endpoint"></a>azdata bdc endpoint

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]  

下列文章提供 `azdata` 工具中 `bdc endpoint` 命令的參考。 如需其他 `azdata` 命令的詳細資訊，請參閱 [azdata 參考](reference-azdata.md)

## <a name="commands"></a>命令
|     |     |
| --- | --- |
[azdata bdc endpoint list](#azdata-bdc-endpoint-list) | 列出巨量資料叢集的端點。
## <a name="azdata-bdc-endpoint-list"></a>azdata bdc endpoint list
列出巨量資料叢集的端點。

```bash
azdata bdc endpoint list [--endpoint-name -e] 
```

### <a name="optional-parameters"></a>選擇性參數

#### `--endpoint-name -e`

巨量資料叢集端點名稱。

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
