---
title: 排序屬性 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 092eb49216874a59e4bcba09431fcc01dc3679a4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66711155"
---
# <a name="sort-property"></a>Sort 屬性
表示在其上的一或多個欄位名稱[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)已排序，以及每個欄位是否以遞增或遞減順序排序。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回**字串**中的值，指出欄位名稱**資料錄集**用來排序。 每個名稱以逗號分隔，且選擇性地後面空白和關鍵字**ASC**，其排序的欄位以遞增順序，或**DESC**，其排序的欄位，以遞減順序。 根據預設，如果未不指定任何關鍵字，則欄位會按照遞增順序。  
  
## <a name="remarks"></a>備註  
 此屬性需要[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)屬性設為**adUseClient**。 暫存索引將會建立每個欄位中指定**排序**如果索引不存在的屬性。  
  
 因為資料不實際重新排列，但只會存取由索引所指定的順序，排序作業會有效率。  
  
 時的值**排序**屬性是空字串，以外的任何**排序**屬性順序的優先順序高於中指定的順序**ORDER BY**子句用來開啟 SQL 陳述式中包含**資料錄集**。  
  
 **資料錄集**不必存取之前開啟**排序**屬性，它可以設定之後隨時**資料錄集**物件具現化。  
  
 設定**排序**屬性設為空的字串將會重設為其原始順序的資料列，並刪除暫存的索引。 不會刪除現有的索引。  
  
 假設**Recordset**包含名為的三個欄位*firstName*， *middleInitial*，以及*lastName*。 設定**排序**屬性設為字串，字串"`lastName DESC, firstName ASC`"，將順序**資料錄集**按照姓氏的遞減順序，則依遞增順序的第一個名稱。 中間名首字母會被忽略。  
  
 沒有任何欄位可以命名為"ASC"或"DESC"因為這些名稱衝突，以關鍵字**ASC**並**DESC**。 您也可以使用具有衝突的名稱建立一個欄位的別名**AS**中傳回的查詢關鍵字**資料錄集**。  
  
## <a name="applies-to"></a>適用於  
 [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [Sort 屬性範例 (VB)](../../../ado/reference/ado-api/sort-property-example-vb.md)   
 [Sort 屬性範例 （VC + +）](../../../ado/reference/ado-api/sort-property-example-vc.md)   
 [Optimize 動態屬性 (ADO)](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md)   
 [SortColumn 屬性 (RDS)](../../../ado/reference/rds-api/sortcolumn-property-rds.md)   
 [SortDirection 屬性 (RDS)](../../../ado/reference/rds-api/sortdirection-property-rds.md)
