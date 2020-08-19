---
description: Number 屬性 (ADO)
title: Number 屬性 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Error::Number
- Error::GetNumber
- Error::get_Number
helpviewer_keywords:
- number property [ADO]
ms.assetid: f92323c5-dd11-4a63-a505-d9014a0f067f
author: rothja
ms.author: jroth
ms.openlocfilehash: 448842387c524326e51b104a0850f9ff503d35e7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88443070"
---
# <a name="number-property-ado"></a>Number 屬性 (ADO)
指出可唯一識別 [錯誤](../../../ado/reference/ado-api/error-object.md) 物件的數位。  
  
## <a name="return-value"></a>傳回值  
 傳回可能對應至其中一個[ErrorValueEnum](../../../ado/reference/ado-api/errorvalueenum.md)常數的**Long**值。  
  
## <a name="remarks"></a>備註  
 使用 **Number** 屬性來判斷發生了哪些錯誤。 屬性的值是對應于錯誤條件的唯一數位。  
  
 [Errors](../../../ado/reference/ado-api/errors-collection-ado.md)集合會以十六進位格式傳回 HRESULT (例如，0x80004005) 或 long 值 (例如 2147467259) 。 這些 Hresult 可由基礎元件（例如 OLE DB 或甚至是 OLE 本身）引發。 如需這些數位的詳細資訊，請參閱 OLE DB 程式設計[人員參考](https://msdn.microsoft.com/3c5e2dd5-35e5-4a93-ac3a-3818bb43bbf8)中的[錯誤 (OLE DB) ](https://msdn.microsoft.com/ed74e62d-4948-4eeb-a7c9-fd7ad46af7fd) *。*  
  
## <a name="applies-to"></a>套用至  
 [Error 物件](../../../ado/reference/ado-api/error-object.md)  
  
## <a name="see-also"></a>另請參閱  
 [Description、HelpCoNtext、NativeError、Number、Source 和 SQLState 屬性範例 (VB) ](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vb.md)   
 [ (VC + +) 的 Description、HelpCoNtext、説明、NativeError、Number、Source 和 SQLState 屬性範例 ](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vc.md)   
 [Description 屬性](../../../ado/reference/ado-api/description-property.md)   
 [HelpCoNtext，內容説明屬性](../../../ado/reference/ado-api/helpcontext-helpfile-properties.md)   
 [Source 屬性 (ADO Error)](../../../ado/reference/ado-api/source-property-ado-error.md)
