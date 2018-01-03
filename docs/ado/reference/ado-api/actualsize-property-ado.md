---
title: "ActualSize 屬性 (ADO) |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords: Field20::ActualSize
helpviewer_keywords: ActualSize property [ADO]
ms.assetid: 722803d0-cef5-4d4c-b79d-3f2f58052229
caps.latest.revision: "13"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: fc354dcc4fb2d669fd93419fac32a66eb4beb331
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="actualsize-property-ado"></a>ActualSize 屬性 (ADO)
表示欄位的實際長度。s 值以位元組為單位。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 傳回**長**值。  
  
## <a name="remarks"></a>備註  
 使用**ActualSize**屬性傳回的實際長度[欄位](../../../ado/reference/ado-api/field-object.md)物件的值。 針對所有欄位， **ActualSize**屬性是唯讀的。 如果 ADO 無法判斷長度的**欄位**物件的值**ActualSize**屬性會傳回**adUnknown**。  
  
 **ActualSize**和[DefinedSize](../../../ado/reference/ado-api/definedsize-property.md)屬性都不同，如下列範例所示。 A**欄位**物件宣告類型為**adVarChar**並傳回最大長度為 50 個字元**DefinedSize**屬性值為 50，但**ActualSize**它所傳回的屬性值是目前記錄的欄位中儲存之資料的長度。 **欄位**與**DefinedSize**大於 255 個位元組會被視為可變長度資料行。  
  
## <a name="applies-to"></a>適用於  
 [Field 物件](../../../ado/reference/ado-api/field-object.md)  
  
## <a name="see-also"></a>請參閱  
 [ActualSize 和 DefinedSize 屬性範例 (VB)](../../../ado/reference/ado-api/actualsize-and-definedsize-properties-example-vb.md)   
 [ActualSize 和 DefinedSize 屬性範例 （VC + +）](../../../ado/reference/ado-api/actualsize-and-definedsize-properties-example-vc.md)   
 [DefinedSize 屬性](../../../ado/reference/ado-api/definedsize-property.md)
