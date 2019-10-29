---
title: 比較 GUID 和 uniqueidentifier 值
description: 示範如何在 SQL Server 和 .NET 中使用 GUID 和 uniqueidentifier 值。
ms.date: 09/30/2019
dev_langs:
- csharp
ms.assetid: aababd75-2335-43e3-ace8-4b7ae84191a8
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: 8a4c5fcc63c2d2ddb8414227ea049e78db1cba10
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: zh-TW
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452288"
---
# <a name="comparing-guid-and-uniqueidentifier-values"></a>比較 GUID 和 uniqueidentifier 值

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[下載 ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

SQL Server 中的全域唯一識別碼（GUID）資料類型是以 `uniqueidentifier` 資料類型表示，它會儲存16位元組的二進位值。 GUID 是二進位數字，主要當成識別項使用，在許多電腦位於許多站台上的網路中，該識別項必須是唯一的。 Guid 可以藉由呼叫 Transact-sql NEWID 函式來產生，並保證在整個世界中都是唯一的。 如需詳細資訊，請參閱[uniqueidentifier （transact-sql）](../../../t-sql/data-types/uniqueidentifier-transact-sql.md)。  
  
## <a name="working-with-sqlguid-values"></a>使用 SqlGuid 值  
因為 Guid 值很長且不明顯，所以不會對使用者有意義。 如果隨機產生的 Guid 會用於索引鍵值，而且您插入大量資料列，您會在索引中取得隨機的 i/o，這可能會對效能產生負面影響。 相較于其他資料類型，Guid 也相當大。 一般來說，我們建議僅針對不適用其他資料類型的非常窄案例，使用 Guid。  
  
### <a name="comparing-guid-values"></a>比較 GUID 值  
比較運算子可以搭配使用 `uniqueidentifier` 值。 不過排序並不是比較兩值的位元模式加以實作的。 `uniqueidentifier` 值允許的運算只有比較 (=、<>、\<、>、\<=、>=)，以及檢查其是否為 NULL (IS NULL 及 IS NOT NULL)。 不允許其他算術運算子。  
  
<xref:System.Guid> 和 <xref:System.Data.SqlTypes.SqlGuid> 都有 `CompareTo` 的方法，可比較不同的 GUID 值。 不過，`System.Guid.CompareTo` 和 `SqlTypes.SqlGuid.CompareTo` 會以不同的方式執行。 <xref:System.Data.SqlTypes.SqlGuid> 使用 SQL Server 行為來執行 `CompareTo`，在值的最後六個位元組中是最重要的。 <xref:System.Guid> 會評估所有的16個位元組。 下列範例示範這項行為差異。 程式碼的第一個區段會顯示未排序的 <xref:System.Guid> 值，而程式碼的第二個區段會顯示已排序的 <xref:System.Guid> 值。 第三個區段會顯示已排序的 <xref:System.Data.SqlTypes.SqlGuid> 值。 輸出會顯示在程式代碼清單下方。  
  
[!code-csharp[DataWorks SqlGuid#1](~/../sqlclient/doc/samples/SqlGuid.cs#1)]
  
這個範例會產生下列結果。  
  
```console
Unsorted Guids:  
3aaaaaaa-bbbb-cccc-dddd-2eeeeeeeeeee  
2aaaaaaa-bbbb-cccc-dddd-1eeeeeeeeeee  
1aaaaaaa-bbbb-cccc-dddd-3eeeeeeeeeee  
  
Sorted Guids:  
1aaaaaaa-bbbb-cccc-dddd-3eeeeeeeeeee  
2aaaaaaa-bbbb-cccc-dddd-1eeeeeeeeeee  
3aaaaaaa-bbbb-cccc-dddd-2eeeeeeeeeee  
  
Sorted SqlGuids:  
2aaaaaaa-bbbb-cccc-dddd-1eeeeeeeeeee  
3aaaaaaa-bbbb-cccc-dddd-2eeeeeeeeeee  
1aaaaaaa-bbbb-cccc-dddd-3eeeeeeeeeee  
```  
  
## <a name="next-steps"></a>後續步驟
- [SQL Server 資料類型和 ADO.NET](sql-server-data-types.md)
