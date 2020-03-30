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
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: 22d27f9a80765aacdfab25c568e8e2635f1779cc
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "78897024"
---
# <a name="comparing-guid-and-uniqueidentifier-values"></a>比較 GUID 和 uniqueidentifier 值

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

SQL Server 中的全域唯一識別碼 (GUID) 資料類型會以 `uniqueidentifier` 資料類型來表示，它會儲存 16 位元組的二進位值。 GUID 是二進位數字，主要當成識別項使用，在許多電腦位於許多站台上的網路中，該識別項必須是唯一的。 GUID 可藉由呼叫 Transact-SQL NEWID 函數來產生，並保證在全世界都是唯一的。 如需詳細資訊，請參閱 [uniqueidentifier (Transact-SQL)](../../../t-sql/data-types/uniqueidentifier-transact-sql.md)。  
  
## <a name="working-with-sqlguid-values"></a>使用 SqlGuid 值  
由於 GUID 值很長且難理解，因此它們對使用者而言不具任何意義。 如果會針對索引鍵值使用隨機產生的 GUID，而且您插入了大量資料列，則您會在索引中取得隨機的 I/O，這可能會對效能產生負面影響。 相較於其他資料類型，GUID 也相對較大。 一般來說，我們建議僅針對範圍非常侷限且不適用其他資料類型的案例使用 GUID。  
  
### <a name="comparing-guid-values"></a>比較 GUID 值  
比較運算子可以搭配使用 `uniqueidentifier` 值。 不過排序並不是比較兩值的位元模式加以實作的。 `uniqueidentifier` 值允許的運算只有比較 (=、<>、\<、>、\<=、>=)，以及檢查其是否為 NULL (IS NULL 及 IS NOT NULL)。 不允許其他算術運算子。  
  
<xref:System.Guid> 和 <xref:System.Data.SqlTypes.SqlGuid> 都具有 `CompareTo` 方法，可用來比較不同的 GUID 值。 不過，`System.Guid.CompareTo` 和 `SqlTypes.SqlGuid.CompareTo` 的實作方式不同。 <xref:System.Data.SqlTypes.SqlGuid> 會使用 SQL Server 行為來實作 `CompareTo`，值的最後六個位元組最重要。 <xref:System.Guid> 會評估所有的 16 個位元組。 下列範例示範這項行為差異。 程式碼的第一個區段會顯示未排序的 <xref:System.Guid> 值，而程式碼的第二個區段會顯示已排序的 <xref:System.Guid> 值。 第三個區段則會顯示已排序的 <xref:System.Data.SqlTypes.SqlGuid> 值。 輸出會顯示於程式碼清單下方。  
  
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
