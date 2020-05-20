---
title: Sort 屬性 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::get_Sort
- Recordset15::put_Sort
- Recordset15::PutSort
- Recordset15::GetSort
- Recordset15::Sort
helpviewer_keywords:
- DESC [ADO]
- ASC [ADO]
- Sort property [ADO]
ms.assetid: 3683ffa0-6f93-4906-9533-ef6942f24f39
author: rothja
ms.author: jroth
ms.openlocfilehash: 3dc6f7799e28fff65a1b6e60329ba9fb94d84824
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82759834"
---
# <a name="sort-property"></a>Sort 屬性
表示排序[記錄集](../../../ado/reference/ado-api/recordset-object-ado.md)的一或多個功能變數名稱，以及每個欄位是否以遞增或遞減順序排序。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回**字串**值，表示要排序之**記錄集中**的功能變數名稱。 每個名稱都以逗號分隔，並選擇性地加上空白和關鍵字**ASC**，這會以遞增順序排序欄位，或使用**DESC**排序欄位，這會以遞減的順序排序欄位。 根據預設，如果未指定關鍵字，則會以遞增順序排序欄位。  
  
## <a name="remarks"></a>備註  
 此屬性需要將[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)屬性設定為**adUseClient**。 如果索引不存在，就會為**Sort**屬性中指定的每個欄位建立暫存索引。  
  
 排序作業很有效率，因為資料不會實體地重新排列，而是以索引所指定的順序來存取。  
  
 當**sort**屬性的值是空字串以外的任何專案時，**排序**屬性順序的優先順序會高於用來開啟**記錄集**之 SQL 語句所包含的**order BY**子句中所指定的順序。  
  
 在存取**Sort**屬性之前，不需要開啟**記錄集**。它可以在具現化**Recordset**物件後的任何時間設定。  
  
 將**排序**屬性設定為空字串，會將資料列重設為其原始順序，並刪除暫存索引。 將不會刪除現有的索引。  
  
 假設**記錄集**包含三個名*為 firstName*、 *middleInitial*和*lastName*的欄位。 將**Sort**屬性設定為字串 " `lastName DESC, firstName ASC` "，這會依姓氏以遞減順序排序**記錄集**，然後依名字以遞增順序排列。 會忽略中間的初始。  
  
 欄位不能命名為 "ASC" 或 "DESC"，因為這些名稱會與關鍵字**ASC**和**DESC**衝突。 您可以在傳回**記錄集**的查詢中，使用**AS**關鍵字來建立具有衝突名稱之欄位的別名。  
  
## <a name="applies-to"></a>套用至  
 [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [Sort 屬性範例（VB）](../../../ado/reference/ado-api/sort-property-example-vb.md)   
 [Sort 屬性範例（VC + +）](../../../ado/reference/ado-api/sort-property-example-vc.md)   
 [優化屬性-動態（ADO）](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md)   
 [SortColumn 屬性（RDS）](../../../ado/reference/rds-api/sortcolumn-property-rds.md)   
 [SortDirection 屬性 (RDS)](../../../ado/reference/rds-api/sortdirection-property-rds.md)
