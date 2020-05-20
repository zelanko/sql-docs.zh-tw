---
title: 優化屬性-動態（ADO） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Optimize property [ADO]
ms.assetid: a491c4ce-2b04-4c84-be83-3846bde8d16b
author: rothja
ms.author: jroth
ms.openlocfilehash: 8d27195b00d1e1867f6bf037cd6c20500ec35e84
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82762081"
---
# <a name="optimize-property-dynamic-ado"></a>Optimize 動態屬性 (ADO)
指定是否應該在[欄位](../../../ado/reference/ado-api/field-object.md)上建立索引。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回**布林**值，指出是否應該建立索引。  
  
## <a name="remarks"></a>備註  
 索引可以改善在[記錄集中](../../../ado/reference/ado-api/recordset-object-ado.md)尋找或排序值之作業的效能。 這是 ADO 內部的索引;您無法在應用程式中明確地存取或使用它。  
  
 若要在欄位上建立索引，請將**Optimize**屬性設定為**True**。 若要刪除索引，請將此屬性設定為**False**。  
  
 當[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)屬性設定為**AdUseClient**時， **Optimize**是附加至[Field](../../../ado/reference/ado-api/field-object.md)物件[屬性](../../../ado/reference/ado-api/properties-collection-ado.md)集合的動態屬性。  
  
## <a name="usage"></a>使用量  
  
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
  
## <a name="applies-to"></a>套用至  
 [Field 物件](../../../ado/reference/ado-api/field-object.md)  
  
## <a name="see-also"></a>另請參閱  
 [Optimize 屬性範例（VB）](../../../ado/reference/ado-api/optimize-property-example-vb.md)   
 [Optimize 屬性範例（VC + +）](../../../ado/reference/ado-api/optimize-property-example-vc.md)   
 [Filter 屬性](../../../ado/reference/ado-api/filter-property.md)   
 [Find 方法（ADO）](../../../ado/reference/ado-api/find-method-ado.md)   
 [Sort 屬性](../../../ado/reference/ado-api/sort-property.md)
