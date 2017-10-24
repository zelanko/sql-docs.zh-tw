---
title: "排序屬性 |Microsoft 文件"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
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
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 16bba12bdcf95e8e71cab6dcb8404b7b3b1916e7
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="sort-property"></a>排序內容
表示在其上的一個或多個欄位名稱[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)已排序，以及每個欄位是否以遞增或遞減順序排序。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回**字串**名稱中的值，指出欄位**資料錄集**用來排序。 每個名稱會以逗號區隔，且選擇性地後面空白和關鍵字， **ASC**，其排序按遞增順序中的欄位或**DESC**，其排序的欄位，以遞減的順序。 根據預設，如果未不指定任何關鍵字，則欄位會依遞增順序。  
  
## <a name="remarks"></a>備註  
 此屬性需要[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)屬性設定為**adUseClient**。 將會建立暫存索引，每個欄位中指定**排序**屬性，如果索引不存在。  
  
 因為資料不實際重新排列，但只需存取指定的索引順序，排序作業會有效率。  
  
 當值**排序**屬性不是空字串，**排序**屬性順序的優先順序高於中指定的順序**ORDER BY**子句用來開啟 SQL 陳述式中包含**資料錄集**。  
  
 **資料錄集**並沒有存取之前開啟**排序**屬性; 它可以設定在任何時間之後**資料錄集**物件具現化。  
  
 設定**排序**屬性設為空字串將會重設為其原始順序的資料列，並刪除暫存索引。 將不會刪除現有的索引。  
  
 假設**資料錄集**包含名為三個欄位*firstName*， *middleInitial*，和*lastName*。 設定**排序**屬性為字串，"`lastName DESC, firstName ASC`」，將順序**資料錄集**按照姓氏的遞減順序，然後再按照名字的遞增順序。 中間名首字母會被忽略。  
  
 沒有欄位可以命名為"ASC"或"DESC"因為這些名稱衝突和關鍵字**ASC**和**DESC**。 您也可以使用具有衝突的名稱建立欄位的別名**AS**關鍵字，查詢中傳回**資料錄集**。  
  
## <a name="applies-to"></a>適用於  
 [資料錄集物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [排序屬性範例 (VB)](../../../ado/reference/ado-api/sort-property-example-vb.md)   
 [排序屬性範例 （VC + +）](../../../ado/reference/ado-api/sort-property-example-vc.md)   
 [最佳化屬性動態 (ADO)](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md)   
 [SortColumn 屬性 (RDS)](../../../ado/reference/rds-api/sortcolumn-property-rds.md)   
 [SortDirection 屬性 (RDS)](../../../ado/reference/rds-api/sortdirection-property-rds.md)

