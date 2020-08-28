---
description: Optimize 動態屬性 (ADO)
title: 優化屬性-動態 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: 3393bbfbfbaeb50c6a608db92dae42bb29fb3b1d
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88990259"
---
# <a name="optimize-property-dynamic-ado"></a>Optimize 動態屬性 (ADO)
指定是否應該在 [欄位](./field-object.md)上建立索引。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回 **布林** 值，這個值會指出是否應該建立索引。  
  
## <a name="remarks"></a>備註  
 索引可以改善在 [記錄集中](./recordset-object-ado.md)尋找或排序值之作業的效能。 索引是 ADO 的內部索引;您無法在應用程式中明確地存取或使用它。  
  
 若要在欄位上建立索引，請將 [ **優化** ] 屬性設定為 [ **True**]。 若要刪除索引，請將此屬性設定為 **False**。  
  
 當[CursorLocation](./cursorlocation-property-ado.md)屬性設定為**AdUseClient**時， **Optimize**是附加至[Field](./field-object.md)物件[屬性](./properties-collection-ado.md)集合的動態屬性。  
  
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
  
## <a name="applies-to"></a>套用至  
 [Field 物件](./field-object.md)  
  
## <a name="see-also"></a>另請參閱  
 [ (VB) 優化屬性範例 ](./optimize-property-example-vb.md)   
 [ (VC + +) 優化屬性範例 ](./optimize-property-example-vc.md)   
 [篩選屬性](./filter-property.md)   
 [ (ADO) 的 Find 方法 ](./find-method-ado.md)   
 [Sort 屬性](./sort-property.md)