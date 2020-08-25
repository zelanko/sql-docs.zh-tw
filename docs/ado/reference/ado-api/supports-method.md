---
description: Supports 方法
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
author: rothja
ms.author: jroth
ms.openlocfilehash: ea56dc34cc2c69c7bb9ef30433a6c7c75f26c552
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88777117"
---
# <a name="supports-method"></a>Supports 方法
判斷指定的 [記錄集](./recordset-object-ado.md) 物件是否支援特定的功能類型。  
  
## <a name="syntax"></a>語法  
  
```  
  
boolean = recordset.Supports(CursorOptions )  
```  
  
## <a name="return-value"></a>傳回值  
 傳回 **布林** 值，指出提供者是否支援 *CursorOptions* 引數所識別的所有功能。  
  
#### <a name="parameters"></a>參數  
 *CursorOptions*  
 包含一或多個[CursorOptionEnum](./cursoroptionenum.md)值的**長**運算式。  
  
## <a name="remarks"></a>備註  
 使用 **支援** 方法來判斷 **記錄集** 物件所支援的功能類型。 如果 **記錄集** 物件支援其對應常數位于 *CursorOptions*中的功能，則 **支援** 的方法會傳回 **True**。 否則，它會傳回 **False**。  
  
> [!NOTE]
>  雖然 **支援** 方法可能會針對指定的功能傳回 **True** ，但並不保證提供者可以在所有情況下提供此功能。 Support **方法只** 會傳回提供者是否可支援指定的功能（假設符合特定條件）。 例如， **支援** 方法可能表示 **記錄集** 物件支援更新，即使資料指標是以多個資料表聯結為基礎，但某些資料行無法更新。  
  
## <a name="applies-to"></a>套用至  
 [Recordset 物件 (ADO)](./recordset-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [支援 (VB 的方法範例) ](./supports-method-example-vb.md)   
 [支援 (VC + +) 的方法範例 ](./supports-method-example-vc.md)   
 [CursorType 屬性 (ADO)](./cursortype-property-ado.md)