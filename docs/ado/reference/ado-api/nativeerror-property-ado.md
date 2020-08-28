---
description: NativeError 屬性 (ADO)
title: " (ADO) 的 NativeError 屬性 |Microsoft Docs"
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: 4acc35688367b9508c80c015999aa302a387a55c
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88990469"
---
# <a name="nativeerror-property-ado"></a>NativeError 屬性 (ADO)
表示指定 [錯誤](./error-object.md) 物件的提供者特定錯誤碼。  
  
## <a name="return-value"></a>傳回值  
 傳回指出錯誤碼的 **Long** 值。  
  
## <a name="remarks"></a>備註  
 您可以使用 **NativeError** 屬性來取得特定 **錯誤** 物件的資料庫特定錯誤資訊。 例如，搭配使用 Microsoft ODBC Provider for OLE DB 與 Microsoft SQL Server 資料庫時，源自 SQL Server 的原生錯誤碼會透過 ODBC 和 ODBC 提供者傳遞至 ADO **NativeError** 屬性。  
  
## <a name="applies-to"></a>套用至  
 [Error 物件](./error-object.md)  
  
## <a name="see-also"></a>另請參閱  
 [Description、HelpCoNtext、NativeError、Number、Source 和 SQLState 屬性範例 (VB) ](./description-helpcontext-helpfile-nativeerror-number-source-example-vb.md)   
 [ (VC + +) 的 Description、HelpCoNtext、説明、NativeError、Number、Source 和 SQLState 屬性範例 ](./description-helpcontext-helpfile-nativeerror-number-source-example-vc.md)