---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: afc9955920784af966ef5d793d76ce251df1bc1d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63242670"
---
# <a name="number-property-ado"></a>Number 屬性 (ADO)
表示唯一識別的數字[錯誤](../../../ado/reference/ado-api/error-object.md)物件。  
  
## <a name="return-value"></a>傳回值  
 傳回**長**值，可能會對應到其中一個[ErrorValueEnum](../../../ado/reference/ado-api/errorvalueenum.md)常數。  
  
## <a name="remarks"></a>備註  
 使用**數字**屬性來判斷是否發生錯誤。 屬性的值是對應到錯誤狀況的唯一號碼。  
  
 [錯誤](../../../ado/reference/ado-api/errors-collection-ado.md)集合以十六進位格式 (例如 0x80004005) 或長數值 (例如，2147467259) 會傳回 HRESULT。 這些 Hresult 可能引發基礎元件，例如 OLE DB 或甚至是 OLE 本身。 如需有關這些數字的詳細資訊，請參閱 <<c0> [ 錯誤 (OLE DB)](https://msdn.microsoft.com/ed74e62d-4948-4eeb-a7c9-fd7ad46af7fd)中[OLE DB 程式設計人員參考](https://msdn.microsoft.com/3c5e2dd5-35e5-4a93-ac3a-3818bb43bbf8)*。*  
  
## <a name="applies-to"></a>適用於  
 [Error 物件](../../../ado/reference/ado-api/error-object.md)  
  
## <a name="see-also"></a>另請參閱  
 [描述、 HelpContext、 HelpFile、 NativeError、 數目、 來源和 SQLState 屬性範例 (VB)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vb.md)   
 [描述、 HelpContext、 HelpFile、 NativeError、 數目、 來源和 SQLState 屬性範例 （VC + +）](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vc.md)   
 [Description 屬性](../../../ado/reference/ado-api/description-property.md)   
 [HelpContext、 HelpFile 屬性](../../../ado/reference/ado-api/helpcontext-helpfile-properties.md)   
 [Source 屬性 (ADO Error)](../../../ado/reference/ado-api/source-property-ado-error.md)
