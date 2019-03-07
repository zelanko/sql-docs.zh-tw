---
title: mssqlctl 應用程式範本參考
titleSuffix: SQL Server 2019 big data clusters
description: Mssqlctl 應用程式範本命令的參考文件。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 02/28/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 16583ba970bfc13312864ea2e9d2571b04c20fcb
ms.sourcegitcommit: d7ed341b2c635dcdd6b0f5f4751bb919a75a6dfe
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2019
ms.locfileid: "57527221"
---
# <a name="mssqlctl-app-template"></a>mssqlctl 應用程式範本

下列文章提供的參考**應用程式範本**中的命令**mssqlctl**工具。 如需其他詳細資訊**mssqlctl**命令，請參閱[mssqlctl 參考](reference-mssqlctl.md)。

## <a id="commands"></a> 命令

|||
|---|---|
| [list](#list) | 擷取支援的範本。 |
| [pull](#pull) | 下載支援的範本。 |

## <a id="list"></a> mssqlctl 應用程式範本清單

擷取支援的範本。

```
mssqlctl app template list
   --url
```

### <a name="parameters"></a>參數

| 參數 | 描述 |
|---|---|
| **--url -u** | 指定不同的範本存放庫位置。 預設值： https://github.com/Microsoft/sql-server-samples.git。 |

### <a name="examples"></a>範例

擷取預設範本儲存機制位置下的所有範本。

```
mssqlctl app template list
```

擷取不同的存放庫位置下的所有範本。

```
mssqlctl app template list --url https://github.com/diffrent/templates.git
```

## <a id="pull"></a> mssqlctl 應用程式範本提取

下載支援的範本。

```
mssqlctl app template pull
   --destination
   --name
   --url
```

### <a name="parameters"></a>參數

| 參數 | 描述 |
|---|---|
| **--destination -d** | 應用程式基本架構的範本放在何處。  預設值:。 / 範本。 |
| **--name -n** | 範本名稱。 如需完整的清單，支援的範本名稱關閉執行`mssqlctl app template list`。 |
| **--url -u** | 指定不同的範本存放庫位置。 預設：
https://github.com/Microsoft/sql-server-samples.git. |

### <a name="examples"></a>範例

下載預設範本儲存機制位置下的所有範本。

```
mssqlctl app template pull
```

下載不同的存放庫位置下的所有範本。

```
mssqlctl app template list --url https://github.com/diffrent/templates.git
```

下載個別的範本名稱。

```
mssqlctl app template pull --name ssis
```

## <a name="next-steps"></a>後續步驟

如需其他詳細資訊**mssqlctl**命令，請參閱[mssqlctl 參考](reference-mssqlctl.md)。 如需有關如何安裝**mssqlctl**工具，請參閱[安裝來管理 SQL Server 2019 巨量資料叢集 mssqlctl](deploy-install-mssqlctl.md)。