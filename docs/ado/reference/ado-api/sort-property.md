---
description: Sort 屬性
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
ms.openlocfilehash: a7cfeeb8d91420ec25cd6dd196b260ad8222c086
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88777417"
---
# <a name="sort-property"></a>Sort 屬性
指出一或多個功能變數名稱（ [記錄集](./recordset-object-ado.md) 的排序依據），以及每個欄位是否以遞增或遞減順序排序。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回 **字串** 值，這個值表示要在 **記錄集中** 排序的功能變數名稱。 每個名稱都是以逗號分隔，並選擇性地在後面加上空白和關鍵字 **ASC**，這會以遞增順序排序欄位，或 **DESC**，以遞減順序排序欄位。 依預設，如果未指定關鍵字，則會以遞增順序排序欄位。  
  
## <a name="remarks"></a>備註  
 此屬性需要將 [CursorLocation](./cursorlocation-property-ado.md) 屬性設定為 **adUseClient**。 如果索引不存在，就會為 **Sort** 屬性中指定的每個欄位建立暫存索引。  
  
 排序作業很有效率，因為資料不會實際重新排列，而是以索引所指定的順序來存取。  
  
 當**sort**屬性的值是空字串以外的任何值時，**排序**屬性順序的優先順序會高於在用來開啟**記錄集**的 SQL 語句中所指定的 order **BY**子句中所指定的順序。  
  
 在存取**Sort**屬性之前，不需要先開啟**記錄集**。這可以在**記錄集**物件具現化之後隨時進行設定。  
  
 將 [ **排序** ] 屬性設定為空字串，會將資料列重設為其原始順序，並刪除暫存索引。 不會刪除現有的索引。  
  
 假設 **記錄集** 包含名為 *firstName*、 *middleInitial*和 *lastName*的三個欄位。 將 **Sort** 屬性設定為字串 " `lastName DESC, firstName ASC` "，這會依姓氏的遞減順序排序 **記錄集** ，然後依名字以遞增順序排序。 會忽略中間的初始。  
  
 沒有欄位可以命名為 "ASC" 或 "DESC"，因為這些名稱與關鍵字 **ASC** 和 **DESC**相衝突。 您可以在傳回**記錄集**的查詢中使用**AS**關鍵字，建立具有衝突名稱之欄位的別名。  
  
## <a name="applies-to"></a>套用至  
 [Recordset 物件 (ADO)](./recordset-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [ (VB) 的 Sort 屬性範例 ](./sort-property-example-vb.md)   
 [Sort 屬性範例 (VC + +) ](./sort-property-example-vc.md)   
 [優化屬性-動態 (ADO) ](./optimize-property-dynamic-ado.md)   
 [SortColumn 屬性 (RDS) ](../rds-api/sortcolumn-property-rds.md)   
 [SortDirection 屬性 (RDS)](../rds-api/sortdirection-property-rds.md)