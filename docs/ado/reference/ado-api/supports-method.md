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
manager: craigg
ms.openlocfilehash: 97c0e4660c14845ddfb59ce4f5f509a0954d98f0
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63268157"
---
# <a name="supports-method"></a>Supports 方法
判斷指定[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件支援特定類型的功能。  
  
## <a name="syntax"></a>語法  
  
```  
  
boolean = recordset.Supports(CursorOptions )  
```  
  
## <a name="return-value"></a>傳回值  
 傳回**布林**值，指出是否所有的功能，由識別*CursorOptions*提供者所支援的引數。  
  
#### <a name="parameters"></a>參數  
 *CursorOptions*  
 A**長**運算式，其中包含一或多個[CursorOptionEnum](../../../ado/reference/ado-api/cursoroptionenum.md)值。  
  
## <a name="remarks"></a>備註  
 使用**支援**方法，以判斷哪些類型的功能**資料錄集**物件支援。 如果**Recordset**物件支援的功能，其對應的常數位於*CursorOptions*，則**支援**方法會傳回**True**. 否則，它會傳回**False**。  
  
> [!NOTE]
>  雖然**支援**方法可能會傳回 **，則為 True**針對指定的功能，它並不保證，提供者可以提供此功能在所有情況下。 **支援**方法只會傳回是否提供者可支援指定的功能，假設某些條件成立。 例如，**支援**方法可能表示**資料錄集**物件支援的更新，即使資料指標以多個資料表聯結，其中的某些資料行不是可更新為基礎。  
  
## <a name="applies-to"></a>適用於  
 [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [Supports 方法範例 (VB)](../../../ado/reference/ado-api/supports-method-example-vb.md)   
 [Supports 方法範例 （VC + +）](../../../ado/reference/ado-api/supports-method-example-vc.md)   
 [CursorType 屬性 (ADO)](../../../ado/reference/ado-api/cursortype-property-ado.md)
