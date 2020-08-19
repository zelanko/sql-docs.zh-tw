---
description: Source 屬性 (ADO Error)
title: Source 屬性 (ADO Error) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Error::get_Source
- Error::Source
- Error::GetSource
helpviewer_keywords:
- Source property [ADO Error]
ms.assetid: 4044ba15-f013-4c4c-9fe1-b4410fe9a778
author: rothja
ms.author: jroth
ms.openlocfilehash: fa7fc5c5098b6e429960e5d72702111abab55ac2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88442050"
---
# <a name="source-property-ado-error"></a>Source 屬性 (ADO Error)
指出原本產生錯誤的物件或應用程式的名稱。  
  
## <a name="return-value"></a>傳回值  
 傳回 **字串** 值，指出物件或應用程式的名稱。  
  
## <a name="remarks"></a>備註  
 使用[Error](../../../ado/reference/ado-api/error-object.md)物件的**Source**屬性來判斷原本產生錯誤的物件或應用程式的名稱。 這可能是物件的類別名稱或程式設計識別碼。 如果是 ADO 中的錯誤，屬性值將會是 **ADODB。**_Objectname_，其中 *objectname* 是觸發錯誤的物件名稱。 若為 ADOX 和 ADO MD，此值會是**ADOX。**_ObjectName_和**ADOMD。** 分別為_ObjectName_。  
  
 根據**error**物件之**Source**、 [Number](../../../ado/reference/ado-api/number-property-ado.md)和[Description](../../../ado/reference/ado-api/description-property.md)屬性的錯誤檔，您可以撰寫程式碼來適當地處理錯誤。  
  
 **錯誤**物件的**Source**屬性是唯讀的。  
  
## <a name="applies-to"></a>套用至  
 [Error 物件](../../../ado/reference/ado-api/error-object.md)  
  
## <a name="see-also"></a>另請參閱  
 [Description、HelpCoNtext、NativeError、Number、Source 和 SQLState 屬性範例 (VB) ](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vb.md)   
 [ (VC + +) 的 Description、HelpCoNtext、説明、NativeError、Number、Source 和 SQLState 屬性範例 ](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vc.md)   
 [Description 屬性](../../../ado/reference/ado-api/description-property.md)   
 [HelpCoNtext，內容説明屬性](../../../ado/reference/ado-api/helpcontext-helpfile-properties.md)   
 [Number 屬性 (ADO) ](../../../ado/reference/ado-api/number-property-ado.md)   
 [來源屬性 (ADO 記錄) ](../../../ado/reference/ado-api/source-property-ado-record.md)   
 [Source 屬性 (ADO Recordset)](../../../ado/reference/ado-api/source-property-ado-recordset.md)
