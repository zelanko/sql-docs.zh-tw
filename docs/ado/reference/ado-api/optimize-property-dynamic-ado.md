---
title: 最佳化屬性動態 (ADO) |Microsoft 文件
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Optimize property [ADO]
ms.assetid: a491c4ce-2b04-4c84-be83-3846bde8d16b
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8bebc49795ff10a29cb3b367c98e9471bc7a2eaa
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/11/2018
ms.locfileid: "35280024"
---
# <a name="optimize-property-dynamic-ado"></a>最佳化屬性動態 (ADO)
指定是否應該在建立索引[欄位](../../../ado/reference/ado-api/field-object.md)。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回**布林**值，指出是否應該建立索引。  
  
## <a name="remarks"></a>備註  
 索引可以提升效能的尋找或排序中的值的作業[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)。 索引是內部 ADO;您無法明確地存取，或在您的應用程式中使用它。  
  
 若要建立索引的欄位上，設定**最佳化**屬性**True**。 若要刪除索引，請將此屬性設定為**False**。  
  
 **最佳化**動態屬性附加至[欄位](../../../ado/reference/ado-api/field-object.md)物件[屬性](../../../ado/reference/ado-api/properties-collection-ado.md)集合時[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)屬性設定為**adUseClient**。  
  
## <a name="usage"></a>使用方式  
  
```  
Dim rs As New Recordset  
Dim fld As Field  
rs.CursorLocation = adUseClient      'Enable index creation  
rs.Fields.Append "Field1", adChar, 35, adFldIsNullable  
rs.Open  
Set fld = rs.Fields(0)  
fld.Properties("Optimize") = True    'Create an index  
fld.Properties("Optimize") = False   'Delete an index  
```  
  
## <a name="applies-to"></a>適用於  
 [Field 物件](../../../ado/reference/ado-api/field-object.md)  
  
## <a name="see-also"></a>另請參閱  
 [最佳化屬性範例 (VB)](../../../ado/reference/ado-api/optimize-property-example-vb.md)   
 [最佳化屬性範例 （VC + +）](../../../ado/reference/ado-api/optimize-property-example-vc.md)   
 [篩選屬性](../../../ado/reference/ado-api/filter-property.md)   
 [Find 方法 (ADO)](../../../ado/reference/ado-api/find-method-ado.md)   
 [Sort 屬性](../../../ado/reference/ado-api/sort-property.md)
