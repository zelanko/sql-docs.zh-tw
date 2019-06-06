---
title: 控制變更資料錄集的基底資料表 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Unique Table property [ADO]
- Unique Schema property [ADO]
- Unique Catalog property [ADO]
ms.assetid: d0e775d8-e353-46a1-ad10-ed4cc240dfaa
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 9f653af8294002bf73b98bd4adc096fac8ba1658
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/05/2019
ms.locfileid: "66710491"
---
# <a name="unique-table-unique-schema-unique-catalog-properties-dynamic-ado"></a>唯一資料表、 唯一的結構描述，唯一目錄動態屬性 (ADO)
可讓您以緊密控制特定的基底資料表中的修改[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)，而形成多個基底資料表的聯結作業。  
  
-   **唯一資料表**指定基底資料表的更新、 插入和刪除允許的名稱。  
  
-   **唯一的結構描述**指定*結構描述*，或資料表的擁有者的名稱。  
  
-   **唯一的型錄**指定*目錄*，或包含資料表之資料庫的名稱。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回**字串**是資料表、 結構描述或目錄名稱的值。  
  
## <a name="remarks"></a>備註  
 它的目錄、 結構描述和資料表名稱可唯一識別所需的基底資料表。 當**唯一資料表**屬性設定，值**唯一的結構描述**或**唯一目錄**屬性用來尋找基底資料表。 它是主要，但並非必要，該其中之一或兩者**唯一的結構描述**和**唯一目錄**之前，先設定屬性**唯一資料表**屬性設定。  
  
 主索引鍵**唯一資料表**整個的主索引鍵會被視為**資料錄集**。 這是需要主索引鍵的任何方法中使用的索引鍵。  
  
 雖然**唯一資料表**設定，則[刪除](../../../ado/reference/ado-api/delete-method-ado-recordset.md)方法會影響已命名的資料表。 [AddNew](../../../ado/reference/ado-api/addnew-method-ado.md)，[重新同步處理](../../../ado/reference/ado-api/resync-method.md)， [Update](../../../ado/reference/ado-api/update-method.md)，以及[UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)方法會影響任何適當的基底資料表**資料錄集**。  
  
 **唯一資料表**進行任何自訂的重新同步處理之前，必須指定。 如果**唯一資料表**未指定，[重新同步處理命令](../../../ado/reference/ado-api/resync-command-property-dynamic-ado.md)屬性會有任何作用。  
  
 如果找不到唯一的基底資料表，就會產生執行階段錯誤。  
  
 這些動態屬性會附加至**Recordset**物件[屬性](../../../ado/reference/ado-api/properties-collection-ado.md)集合時[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)屬性設定為**adUseClient**。  
  
## <a name="applies-to"></a>適用於  
 [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
