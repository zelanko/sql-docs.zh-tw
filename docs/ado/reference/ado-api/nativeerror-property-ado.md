---
title: NativeError 屬性 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Error::GetNativeError
- Error::get_NativeError
- Error::NativeError
helpviewer_keywords:
- NativeError property [ADO]
ms.assetid: b9b47e57-18a4-4186-aef5-5bd18d7b1d74
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2f6ee8724454a8871f6642f5d812584ccffd9385
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63242385"
---
# <a name="nativeerror-property-ado"></a>NativeError 屬性 (ADO)
指出提供者特有的錯誤程式碼給定[錯誤](../../../ado/reference/ado-api/error-object.md)物件。  
  
## <a name="return-value"></a>傳回值  
 傳回**長**值，指出錯誤的程式碼。  
  
## <a name="remarks"></a>備註  
 使用**NativeError**屬性，以擷取特定的資料庫特定錯誤資訊**錯誤**物件。 比方說，當用於 OLE DB 的 Microsoft ODBC 提供者與 Microsoft SQL Server 資料庫，源自於 SQL Server 的原生錯誤碼通過 ODBC 和 ODBC 提供者的 ado **NativeError**屬性。  
  
## <a name="applies-to"></a>適用於  
 [Error 物件](../../../ado/reference/ado-api/error-object.md)  
  
## <a name="see-also"></a>另請參閱  
 [描述、 HelpContext、 HelpFile、 NativeError、 數目、 來源和 SQLState 屬性範例 (VB)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vb.md)   
 [描述、 HelpContext、 HelpFile、 NativeError、 數目、 來源和 SQLState 屬性範例 （VC + +）](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vc.md)   
