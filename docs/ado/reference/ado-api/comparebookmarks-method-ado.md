---
title: CompareBookmarks 方法 (ADO) |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 85ca76678c0d3e75a106164626c4e3c3a81bd7e9
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63315980"
---
# <a name="comparebookmarks-method-ado"></a>CompareBookmarks 方法 (ADO)
比較兩個書籤，並傳回它們相對值的指示。  
  
## <a name="syntax"></a>語法  
  
```  
  
result = recordset.CompareBookmarks(Bookmark1, Bookmark2)  
```  
  
## <a name="return-value"></a>傳回值  
 傳回[CompareEnum](../../../ado/reference/ado-api/compareenum.md)值，指出他們的書籤所表示的兩筆記錄的相對的資料列位置。  
  
#### <a name="parameters"></a>參數  
 *Bookmark1*  
 第一個資料列的書籤。  
  
 *Bookmark2*  
 第二個資料列的書籤。  
  
## <a name="remarks"></a>備註  
 書籤必須套用至相同[Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)物件，或**資料錄集**物件及其[複製](../../../ado/reference/ado-api/clone-method-ado.md)。 您無法可靠地比較來自不同的書籤**資料錄集**物件，即使它們已建立從相同的原始碼或命令。 也可以比較的書籤**資料錄集**其基礎的提供者不支援比較的物件。  
  
 書籤可唯一識別中的資料列**資料錄集**物件。 使用[書籤](../../../ado/reference/ado-api/bookmark-property-ado.md)要取得其書籤的目前資料列的屬性。  
  
 由於書籤的資料類型是每個提供者特有的 ADO 會公開為**Variant**。 例如，SQL Server 的書籤都屬於型別 DBTYPE_R8 (**Double**)。 ADO 會公開做為這個型別**Variant**使用的子型別**Double**。  
  
 當比較的書籤，ADO 就不會嘗試任何類型的強制型轉。 值會直接傳遞給提供者發生的比較。 如果書籤傳遞給**CompareBookmarks**方法儲存在不同類型的變數，它會產生下列型別不符的錯誤：「 引數屬於錯誤類型、 超出可接受的範圍，或與彼此衝突。 」  
  
 不是有效或格式不正確的書籤會造成錯誤。  
  
## <a name="applies-to"></a>適用於  
 [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [CompareBookmarks 方法範例 (VB)](../../../ado/reference/ado-api/comparebookmarks-method-example-vb.md)   
 [CompareBookmarks 方法範例 （VC + +）](../../../ado/reference/ado-api/comparebookmarks-method-example-vc.md)   
 [Bookmark 屬性 (ADO)](../../../ado/reference/ado-api/bookmark-property-ado.md)
