---
title: 支援方法 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::raw_Supports
- Recordset15::Supports
helpviewer_keywords:
- Supports method [ADO]
ms.assetid: 298fc41c-0b55-42fc-b373-c5133b4da6a5
author: MightyPen
ms.author: genemi
ms.openlocfilehash: cce5ab3b735d3c641da4a6234e860d0528f107c2
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "67936709"
---
# <a name="supports-method"></a>Supports 方法
判斷指定的[記錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件是否支援特定類型的功能。  
  
## <a name="syntax"></a>語法  
  
```  
  
boolean = recordset.Supports(CursorOptions )  
```  
  
## <a name="return-value"></a>傳回值  
 傳回**布林**值，指出提供者是否支援*CursorOptions*引數所識別的所有功能。  
  
#### <a name="parameters"></a>參數  
 *CursorOptions*  
 包含一個或多個[CursorOptionEnum](../../../ado/reference/ado-api/cursoroptionenum.md)值的**長**運算式。  
  
## <a name="remarks"></a>備註  
 使用**支援**方法來判斷**記錄集**物件所支援的功能類型。 如果**記錄集**物件支援其對應常數在*CursorOptions*中的功能，**支援**方法會傳回**True**。 否則，它會傳回**False**。  
  
> [!NOTE]
>  雖然針對指定的功能，**支援**方法可能會傳回**True** ，但並不保證提供者可以在所有情況下提供此功能。 **支援**方法只會傳回提供者是否可支援指定的功能（假設符合特定條件）。 例如，**支援**方法可能會指出即使資料指標是以多個資料表聯結為基礎，**記錄集**物件還是支援更新，某些資料行則無法更新。  
  
## <a name="applies-to"></a>套用至  
 [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [支援方法範例（VB）](../../../ado/reference/ado-api/supports-method-example-vb.md)   
 [支援方法範例（VC + +）](../../../ado/reference/ado-api/supports-method-example-vc.md)   
 [CursorType 屬性 (ADO)](../../../ado/reference/ado-api/cursortype-property-ado.md)
