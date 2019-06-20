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
manager: jroth
ms.openlocfilehash: 17f279af526a9e1f5b2c8deff4b4092e7949c5ea
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66707271"
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
