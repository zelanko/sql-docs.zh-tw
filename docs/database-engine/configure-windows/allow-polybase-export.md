---
title: 允許 PolyBase 匯出組態選項 | Microsoft Docs
description: 設定 SQL Server 中的 `allow polybase export` 組態選項
ms.custom: ''
ms.date: 07/10/2020
ms.prod: sql
ms.prod_service: ''
ms.reviewer: ''
ms.technology: polybase
ms.topic: conceptual
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: c25a7e42b55561ed6337281497e847999d722292
ms.sourcegitcommit: dacd9b6f90e6772a778a3235fb69412662572d02
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2020
ms.locfileid: "86279645"
---
# <a name="set-allow-polybase-export-configuration-option"></a>設定 `allow polybase export` 組態選項

[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]

`allow polybase export` 伺服器組態選項允許 `INSERT` 到 Hadoop 外部資料表。 

此功能不支援插入其他外部資料來源。

 下表說明可用的值： 

| 值 | 意義                                |
|-------|----------------------------------------|
| 0     | 已停用。 這是預設值。 |
| 1     | 啟用                                |


設定會立即生效。

## <a name="example"></a>範例

下列範例會啟用此設定。

```sql
sp_configure 'show advanced options', 1;
GO
RECONFIGURE;
GO
sp_configure 'allow polybase export', 0;
GO
RECONFIGURE;
GO
```

## <a name="next-steps"></a>後續步驟

 [匯出資料](../../relational-databases/polybase/polybase-configure-hadoop.md#exporting-data)