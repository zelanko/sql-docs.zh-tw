---
title: 大量複製作業的順序提示
description: 描述如何在大量複製作業中使用順序提示。
ms.date: 06/15/2020
dev_langs:
- csharp
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: johnnypham
ms.author: v-jopha
ms.reviewer: ''
ms.openlocfilehash: c7365bdc6da75e04d019ca1a6a87b90dd8d4ec3c
ms.sourcegitcommit: 6b3569977b034554883a94d73d1c4df6e2f74fe2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2020
ms.locfileid: "85110142"
---
# <a name="order-hints-for-bulk-copy-operations"></a>大量複製作業的順序提示

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

比起其他將資料載入 SQL Server 資料表的方法，大量複製作業能提供顯著的效能優勢。 使用順序提示可進一步增強效能。 指定大量複製作業的順序提示，可減少將資料排序插入至資料表 (具有叢集索引) 的時間。

根據預設，大量插入作業會假設傳入的資料未排序。 SQL Server 會先強制此資料的中繼排序，然後再大量載入。 若知道傳入的資料已排序，則可使用順序提示來告知大量複製作業，有關任何作為部分叢集索引的目的地資料行其排序次序。
  
## <a name="adding-order-hints-to-a-bulk-copy-operation"></a>將順序提示新增至大量複製作業  
下列範例會從 **AdventureWorks** 範例資料庫中的來源資料表，將資料大量複製到相同資料庫中的目的地資料表。 建立 SqlBulkCopyColumnOrderHint 物件，以定義目的地資料表中 **ProductNumber** 資料行的排序次序。 然後，將順序提示新增至 SqlBulkCopy 執行個體，以將適當的順序提示引數附加至所產生 `INSERT BULK` 查詢。

[!code-csharp [SqlBulkCopy.ColumnOrderHint#1](~/../sqlclient/doc/samples/SqlBulkCopy_ColumnOrderHint.cs#1)]

## <a name="next-steps"></a>後續步驟
- [SQL Server 中的大量複製作業](bulk-copy-operations-sql-server.md)
