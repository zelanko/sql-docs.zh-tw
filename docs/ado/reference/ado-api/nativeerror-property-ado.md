---
title: "NativeError 屬性 (ADO) |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Error::GetNativeError
- Error::get_NativeError
- Error::NativeError
helpviewer_keywords: NativeError property [ADO]
ms.assetid: b9b47e57-18a4-4186-aef5-5bd18d7b1d74
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e6d98280027ac307ca04a988052b189cf3365f8e
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="nativeerror-property-ado"></a>NativeError 屬性 (ADO)
指出提供者特有的錯誤程式碼給定[錯誤](../../../ado/reference/ado-api/error-object.md)物件。  
  
## <a name="return-value"></a>傳回值  
 傳回**長**值，指出錯誤的程式碼。  
  
## <a name="remarks"></a>備註  
 使用**NativeError**屬性，以擷取特定的資料庫特定錯誤資訊**錯誤**物件。 比方說，當使用 OLE db 的 Microsoft ODBC 提供者與 Microsoft SQL Server 資料庫，來自 SQL Server 的原生錯誤碼通過 ODBC 和 ODBC 提供者於 ADO **NativeError**屬性。  
  
## <a name="applies-to"></a>適用於  
 [Error 物件](../../../ado/reference/ado-api/error-object.md)  
  
## <a name="see-also"></a>請參閱＜  
 [描述、 HelpContext、 說明檔案、 NativeError、 數字、 來源和 SQLState 屬性範例 (VB)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vb.md)   
 [描述、 HelpContext、 說明檔案、 NativeError、 數字、 來源和 SQLState 屬性範例 （VC + +）](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vc.md)   
