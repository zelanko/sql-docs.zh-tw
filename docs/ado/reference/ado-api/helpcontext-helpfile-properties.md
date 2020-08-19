---
description: HelpContext、HelpFile 屬性
title: HelpCoNtext，內容説明的屬性 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Error::GetHelpContext
- Error::GetHelpFile
- Error::get_HelpFile
- Error::get_HelpContext
- Error::HelpContext
- Error::HelpFile
helpviewer_keywords:
- HelpContext property [ADO]
- HelpFile property [ADO]
ms.assetid: 2b9ef441-993c-44d4-8f87-fac0979dac1d
author: rothja
ms.author: jroth
ms.openlocfilehash: 628d3c0d01cc1b62304627fb310705b093976f8c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88443480"
---
# <a name="helpcontext-helpfile-properties"></a>HelpContext、HelpFile 屬性
指出與 [錯誤](../../../ado/reference/ado-api/error-object.md) 物件相關聯的說明檔和主題。  
  
## <a name="return-values"></a>傳回值  
  
-   **HelpContextID**比傳回說明檔中主題的內容識別碼，做為**完整**值。  
  
-   **説明** 傳回 **字串** 值，此值會評估為說明檔的完整解析路徑。  
  
## <a name="remarks"></a>備註  
 如果在 [協助工具 **] 屬性中** 指定說明檔， **HelpCoNtext** 屬性會用來自動顯示它所識別的說明主題。 如果沒有可用的相關說明主題， **HelpCoNtext** 屬性會傳回零， **而 [輔助** 功能] 屬性會傳回長度為零的字串 ( "" ) 。  
  
## <a name="applies-to"></a>套用至  
 [Error 物件](../../../ado/reference/ado-api/error-object.md)  
  
## <a name="see-also"></a>另請參閱  
 [Description、HelpCoNtext、NativeError、Number、Source 和 SQLState 屬性範例 (VB) ](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vb.md)   
 [ (VC + +) 的 Description、HelpCoNtext、説明、NativeError、Number、Source 和 SQLState 屬性範例 ](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vc.md)   
 [Description 屬性](../../../ado/reference/ado-api/description-property.md)   
 [Number 屬性 (ADO) ](../../../ado/reference/ado-api/number-property-ado.md)   
 [Source 屬性 (ADO Error)](../../../ado/reference/ado-api/source-property-ado-error.md)
