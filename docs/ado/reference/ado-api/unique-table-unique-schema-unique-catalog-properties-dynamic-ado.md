---
title: 控制記錄集基表的變更（ADO） |Microsoft Docs
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
ms.openlocfilehash: 1b70920cd223223d5efb14925a6808168ca9cc16
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67911671"
---
# <a name="unique-table-unique-schema-unique-catalog-properties-dynamic-ado"></a>唯一的資料表、唯一的架構、唯一的目錄屬性-動態（ADO）
可讓您在多個基表上，針對聯結作業所形成的[記錄集](../../../ado/reference/ado-api/recordset-object-ado.md)內的特定基表，進一步控制其修改。  
  
-   **唯一資料表**指定允許更新、插入和刪除的基表名稱。  
  
-   [**唯一架構**] 指定資料表的*架構*或擁有者的名稱。  
  
-   **唯一目錄**：指定*目錄*，或包含資料表的資料庫名稱。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回**字串**值，這是資料表、架構或目錄的名稱。  
  
## <a name="remarks"></a>備註  
 所需的基表是以其目錄、架構和資料表名稱來唯一識別。 設定**Unique table**屬性時，會使用 [**唯一架構**] 或 [**唯一目錄**] 屬性的值來尋找基表。 這是預期的，但並非必要，必須在設定**Unique Table**屬性之前，設定**唯一的架構**和**唯一的目錄**屬性。  
  
 **唯一資料表**的主要索引鍵會被視為整個**記錄集**的主鍵。 這是用於任何需要主鍵之方法的索引鍵。  
  
 當設定**Unique 資料表**時， [Delete](../../../ado/reference/ado-api/delete-method-ado-recordset.md)方法只會影響已命名的資料表。 [AddNew](../../../ado/reference/ado-api/addnew-method-ado.md)、 [Resync](../../../ado/reference/ado-api/resync-method.md)、 [Update](../../../ado/reference/ado-api/update-method.md)和[UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)方法會影響**記錄集**的任何適當基礎基表。  
  
 在執行任何自訂重新同步處理之前，必須先指定**唯一資料表**。 如果尚未指定**唯一資料表**，[重新[同步命令](../../../ado/reference/ado-api/resync-command-property-dynamic-ado.md)] 屬性將不會有任何作用。  
  
 如果找不到唯一的基表，就會產生執行階段錯誤。  
  
 當[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)屬性設定為**adUseClient**時，這些動態屬性都會附加至**記錄集**物件[屬性](../../../ado/reference/ado-api/properties-collection-ado.md)集合。  
  
## <a name="applies-to"></a>套用至  
 [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
