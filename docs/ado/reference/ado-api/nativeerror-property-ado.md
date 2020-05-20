---
title: NativeError 屬性（ADO） |Microsoft Docs
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
ms.openlocfilehash: 2b9bd2228b38af302d96cd3794cc00674449fcac
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82762399"
---
# <a name="nativeerror-property-ado"></a>NativeError 屬性 (ADO)
指出給定[錯誤](../../../ado/reference/ado-api/error-object.md)物件的提供者特定錯誤碼。  
  
## <a name="return-value"></a>傳回值  
 傳回指出錯誤碼的**長**數值。  
  
## <a name="remarks"></a>備註  
 您可以使用**NativeError**屬性來抓取特定**錯誤**物件的資料庫特定錯誤資訊。 例如，搭配 Microsoft SQL Server 資料庫使用 OLE DB 的 Microsoft ODBC 提供者時，源自 SQL Server 的原生錯誤碼會透過 ODBC 和 ODBC 提供者傳遞至 ADO **NativeError**屬性。  
  
## <a name="applies-to"></a>套用至  
 [Error 物件](../../../ado/reference/ado-api/error-object.md)  
  
## <a name="see-also"></a>另請參閱  
 [Description、HelpCoNtext、內容説明、NativeError、Number、Source 和 SQLState 屬性範例（VB）](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vb.md)   
 [Description、HelpCoNtext、內容説明、NativeError、Number、Source 和 SQLState 屬性範例（VC + +）](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vc.md)   
