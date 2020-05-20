---
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
ms.openlocfilehash: 13fb3f0b5bf55ac9acb525183eba6d8645f4de62
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82758714"
---
# <a name="helpcontext-helpfile-properties"></a>HelpContext、HelpFile 屬性
指出與[錯誤](../../../ado/reference/ado-api/error-object.md)物件相關聯的說明檔和主題。  
  
## <a name="return-values"></a>傳回值  
  
-   **HelpContextID**比對針對說明檔中的主題，傳回內容識別碼，做為**完整**的值。  
  
-   **説明**傳回評估為說明檔之完整解析路徑的**字串**值。  
  
## <a name="remarks"></a>備註  
 如果**在 [協助**內容] 屬性中指定說明檔，則會使用**HelpCoNtext**屬性來自動顯示其識別的說明主題。 如果沒有相關的說明主題可供使用， **HelpCoNtext**屬性會傳回零，**而 [提供**內容] 屬性會傳回長度為零的字串（""）。  
  
## <a name="applies-to"></a>套用至  
 [Error 物件](../../../ado/reference/ado-api/error-object.md)  
  
## <a name="see-also"></a>另請參閱  
 [Description、HelpCoNtext、內容説明、NativeError、Number、Source 和 SQLState 屬性範例（VB）](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vb.md)   
 [Description、HelpCoNtext、內容説明、NativeError、Number、Source 和 SQLState 屬性範例（VC + +）](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vc.md)   
 [Description 屬性](../../../ado/reference/ado-api/description-property.md)   
 [Number 屬性（ADO）](../../../ado/reference/ado-api/number-property-ado.md)   
 [Source 屬性 (ADO Error)](../../../ado/reference/ado-api/source-property-ado-error.md)
