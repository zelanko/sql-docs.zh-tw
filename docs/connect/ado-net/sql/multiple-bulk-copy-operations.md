---
title: 多項大量複製作業
description: 描述如何使用 SqlBulkCopy 類別，在 SQL Server 的執行個體中執行資料的多個大量複製作業。
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: 5ad12f94-7459-4a93-a421-4160d1a90715
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-kaywon
ms.openlocfilehash: a0a1f24970801698eedc8971f0db54bd08589945
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/08/2020
ms.locfileid: "80924300"
---
# <a name="multiple-bulk-copy-operations"></a>多項大量複製作業

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

您可以使用 <xref:Microsoft.Data.SqlClient.SqlBulkCopy> 類別的單一執行個體，執行多項大量複製作業。 如果複製作業在複本 (例如目的地資料表名稱) 之間變更，您必須在後續呼叫任何 **WriteToServer** 方法之前加以更新，如下列範例所示。 除非已明確地變更，所有屬性值與之前指定執行個體上的大量複製作業維持相同。  
  
> [!NOTE]
>  比起對每項作業使用個別的執行個體，使用 <xref:Microsoft.Data.SqlClient.SqlBulkCopy> 的相同執行個體來執行多項大量複製作業通常更有效率。  
  
如果您使用相同的 <xref:Microsoft.Data.SqlClient.SqlBulkCopy> 物件執行數項大量複製作業，並未限制來源或目標資訊在每項作業中是否相等或不同。 不過，當您每次寫入到伺服器時，必須確定資料行關聯資訊已正確設定。  

## <a name="example"></a>範例

> [!IMPORTANT]
>  除非您已如[大量複製範例設定](bulk-copy-example-setup.md)中所述建立工作資料表，否則此範例不會執行。 這個程式碼僅是為了示範使用 **SqlBulkCopy** 的語法而提供。 如果來源和目的地資料表位於相同的 SQL Server 執行個體，則使用 Transact-SQL `INSERT … SELECT` 陳述式來複製資料會更方便且快速。  
  
[!code-csharp[DataWorks SqlBulkCopy_._ColumnMappingOrdersDetails#1](~/../sqlclient/doc/samples/SqlBulkCopy_ColumnMappingOrdersDetails.cs#1)]
  
## <a name="next-steps"></a>後續步驟
- [SQL Server 中的大量複製作業](bulk-copy-operations-sql-server.md)
