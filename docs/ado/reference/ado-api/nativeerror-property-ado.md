---
description: NativeError 屬性 (ADO)
title: " (ADO) 的 NativeError 屬性 |Microsoft Docs"
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
author: rothja
ms.author: jroth
ms.openlocfilehash: f26e8ab07a5ac51307d3b3da374e982ea5b6f469
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88443110"
---
# <a name="nativeerror-property-ado"></a>NativeError 屬性 (ADO)
表示指定 [錯誤](../../../ado/reference/ado-api/error-object.md) 物件的提供者特定錯誤碼。  
  
## <a name="return-value"></a>傳回值  
 傳回指出錯誤碼的 **Long** 值。  
  
## <a name="remarks"></a>備註  
 您可以使用 **NativeError** 屬性來取得特定 **錯誤** 物件的資料庫特定錯誤資訊。 例如，搭配使用 Microsoft ODBC Provider for OLE DB 與 Microsoft SQL Server 資料庫時，源自 SQL Server 的原生錯誤碼會透過 ODBC 和 ODBC 提供者傳遞至 ADO **NativeError** 屬性。  
  
## <a name="applies-to"></a>套用至  
 [Error 物件](../../../ado/reference/ado-api/error-object.md)  
  
## <a name="see-also"></a>另請參閱  
 [Description、HelpCoNtext、NativeError、Number、Source 和 SQLState 屬性範例 (VB) ](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vb.md)   
 [ (VC + +) 的 Description、HelpCoNtext、説明、NativeError、Number、Source 和 SQLState 屬性範例 ](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vc.md)   
