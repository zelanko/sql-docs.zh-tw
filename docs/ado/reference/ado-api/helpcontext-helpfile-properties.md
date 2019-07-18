---
title: HelpContext、 HelpFile 屬性 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ba441a52958e423308e648f15dd36e14d6d1d895
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67918471"
---
# <a name="helpcontext-helpfile-properties"></a>HelpContext、HelpFile 屬性
表示說明檔和相關聯的主題[錯誤](../../../ado/reference/ado-api/error-object.md)物件。  
  
## <a name="return-values"></a>傳回值  
  
-   **文字串**傳回的內容識別碼，作為**長**說明檔中主題的值。  
  
-   **HelpFile**會傳回**字串**評估的說明檔的完整解析路徑的值。  
  
## <a name="remarks"></a>備註  
 如果說明檔中指定**HelpFile**屬性， **HelpContext**屬性用來自動顯示 [說明] 主題，它會識別。 如果沒有可用的沒有任何相關的說明主題**HelpContext**屬性會傳回零， **HelpFile**屬性會傳回零長度字串 ("")。  
  
## <a name="applies-to"></a>適用於  
 [Error 物件](../../../ado/reference/ado-api/error-object.md)  
  
## <a name="see-also"></a>另請參閱  
 [描述、 HelpContext、 HelpFile、 NativeError、 數目、 來源和 SQLState 屬性範例 (VB)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vb.md)   
 [描述、 HelpContext、 HelpFile、 NativeError、 數目、 來源和 SQLState 屬性範例 （VC + +）](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vc.md)   
 [Description 屬性](../../../ado/reference/ado-api/description-property.md)   
 [Number 屬性 (ADO)](../../../ado/reference/ado-api/number-property-ado.md)   
 [Source 屬性 (ADO Error)](../../../ado/reference/ado-api/source-property-ado-error.md)
