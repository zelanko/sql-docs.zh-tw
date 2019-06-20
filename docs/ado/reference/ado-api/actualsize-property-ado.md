---
title: ActualSize 屬性 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 03/20/2018
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Field20::ActualSize
helpviewer_keywords:
- ActualSize property [ADO]
ms.assetid: 722803d0-cef5-4d4c-b79d-3f2f58052229
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: b864f480542c7ff649bf9b830ba445517dafb91b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66698898"
---
# <a name="actualsize-property-ado"></a>ActualSize 屬性 (ADO)
表示欄位的值，以位元組為單位的實際長度。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 傳回**長**值。  
  
## <a name="remarks"></a>備註  
 使用**ActualSize**屬性傳回的實際長度[欄位](../../../ado/reference/ado-api/field-object.md)物件的值。 所有欄位，如**ActualSize**屬性是唯讀的。 如果 ADO 無法判斷長度**欄位**物件的值**ActualSize**屬性會傳回**adUnknown**。  
  
 **ActualSize**並[DefinedSize](../../../ado/reference/ado-api/definedsize-property.md)屬性都不同，如下列範例所示。 A**欄位**物件的宣告型別**adVarChar** ，並傳回最大長度為 50 個字元**DefinedSize**屬性值為 50，但是**ActualSize**它所傳回的屬性值是目前記錄的欄位中儲存之資料的長度。 **欄位**具有**DefinedSize**大於 255 個位元組會被視為可變長度資料行。  
  
## <a name="applies-to"></a>適用於  
 [Field 物件](../../../ado/reference/ado-api/field-object.md)  
  
## <a name="see-also"></a>另請參閱  
 [ActualSize 和 DefinedSize 屬性範例 (VB)](../../../ado/reference/ado-api/actualsize-and-definedsize-properties-example-vb.md)   
 [ActualSize 和 DefinedSize 屬性範例 （VC + +）](../../../ado/reference/ado-api/actualsize-and-definedsize-properties-example-vc.md)   
 [DefinedSize 屬性](../../../ado/reference/ado-api/definedsize-property.md)
