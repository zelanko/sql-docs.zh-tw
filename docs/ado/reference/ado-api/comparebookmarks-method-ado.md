---
description: CompareBookmarks 方法 (ADO)
title: " (ADO) 的 CompareBookmarks 方法 |Microsoft Docs"
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- CompareBookmarks
- Recordset20::CompareBookmarks
- Recordset20::raw_CompareBookmarks
helpviewer_keywords:
- CompareBookmarks method [ADO]
ms.assetid: d0b64286-2cc4-4a22-8f1d-9aefeebbcbc6
author: rothja
ms.author: jroth
ms.openlocfilehash: 4729574b92b841da48f7cf6de6f1dcabc369b4a7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88450800"
---
# <a name="comparebookmarks-method-ado"></a>CompareBookmarks 方法 (ADO)
比較兩個書簽，並傳回其相對值的指示。  
  
## <a name="syntax"></a>語法  
  
```  
  
result = recordset.CompareBookmarks(Bookmark1, Bookmark2)  
```  
  
## <a name="return-value"></a>傳回值  
 傳回 [CompareEnum](../../../ado/reference/ado-api/compareenum.md) 值，指出依書簽表示之兩筆記錄的相對資料列位置。  
  
#### <a name="parameters"></a>參數  
 *Bookmark1*  
 第一個資料列的書簽。  
  
 *Bookmark2*  
 第二列的書簽。  
  
## <a name="remarks"></a>備註  
 書簽必須套用至相同的 [記錄集](../../../ado/reference/ado-api/recordset-object-ado.md) 物件，或是 **記錄集** 物件與其 [複製](../../../ado/reference/ado-api/clone-method-ado.md)。 您無法從不同的 **記錄集** 物件中可靠地比較書簽，即使它們是從相同的來源或命令所建立。 您也無法比較其基礎提供者不支援比較之 **記錄集** 物件的書簽。  
  
 書簽可唯一識別 **記錄集** 物件中的資料列。 使用目前資料列的 [ [書簽](../../../ado/reference/ado-api/bookmark-property-ado.md) ] 屬性來取得其書簽。  
  
 因為書簽的資料類型是每個提供者特有的，所以 ADO 會將其公開為 **變數**。 例如，SQL Server 書簽的類型 DBTYPE_R8 (**雙**) 。 ADO 會將此類型公開為具有**Double**子類型的**變數**。  
  
 比較書簽時，ADO 不會嘗試任何類型的強制型轉。 這些值只會傳遞給提供者的比較。 如果傳遞至 **CompareBookmarks** 方法的書簽儲存在不同類型的變數中，它可能會產生下列類型不符的錯誤：「引數的類型不正確、不在可接受的範圍內，或彼此衝突。」  
  
 無效或格式不正確的書簽將會造成錯誤。  
  
## <a name="applies-to"></a>套用至  
 [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [ (VB) 的 CompareBookmarks 方法範例 ](../../../ado/reference/ado-api/comparebookmarks-method-example-vb.md)   
 [CompareBookmarks 方法範例 (VC + +) ](../../../ado/reference/ado-api/comparebookmarks-method-example-vc.md)   
 [Bookmark 屬性 (ADO)](../../../ado/reference/ado-api/bookmark-property-ado.md)
