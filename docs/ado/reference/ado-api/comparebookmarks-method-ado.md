---
title: "CompareBookmarks 方法 (ADO) |Microsoft 文件"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- CompareBookmarks
- Recordset20::CompareBookmarks
- Recordset20::raw_CompareBookmarks
helpviewer_keywords:
- CompareBookmarks method [ADO]
ms.assetid: d0b64286-2cc4-4a22-8f1d-9aefeebbcbc6
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: f1e19f4800505e3ed481455bc349d65855c6b538
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="comparebookmarks-method-ado"></a>CompareBookmarks 方法 (ADO)
比較兩個書籤，並傳回它們的相對值指示。  
  
## <a name="syntax"></a>語法  
  
```  
  
result = recordset.CompareBookmarks(Bookmark1, Bookmark2)  
```  
  
## <a name="return-value"></a>傳回值  
 傳回[CompareEnum](../../../ado/reference/ado-api/compareenum.md)值，指出其書籤所代表的兩筆記錄的相對的資料列位置。  
  
#### <a name="parameters"></a>參數  
 *Bookmark1*  
 第一個資料列的書籤。  
  
 *Bookmark2*  
 第二個資料列的書籤。  
  
## <a name="remarks"></a>備註  
 書籤必須套用至相同[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件，或**資料錄集**物件及其[複製](../../../ado/reference/ado-api/clone-method-ado.md)。 您無法可靠地比較從不同的書籤**資料錄集**物件，即使它們已建立從相同來源或命令。 也可以比較的書籤**資料錄集**其基礎提供者不支援的比較的物件。  
  
 書籤可唯一識別中的資料列**資料錄集**物件。 使用[書籤](../../../ado/reference/ado-api/bookmark-property-ado.md)要取得的書籤的目前資料列的屬性。  
  
 因為每個提供者特有的書籤的資料類型，ADO 來公開為**Variant**。 例如，SQL Server 的書籤都屬於型別 DBTYPE_R8 (**Double**)。 ADO 會公開此類型為**Variant**的子類型與**Double**。  
  
 當比較的書籤，ADO 不會嘗試任何類型的強制型轉。 值會直接傳遞給提供者發生的比較。 如果書籤傳遞至**CompareBookmarks**方法會儲存在不同類型的變數，它會產生下列的類型不符錯誤: 「 引數屬於錯誤的型別，超出可接受的範圍，或有衝突與每個其他 」。  
  
 不是有效或格式不正確的書籤會造成錯誤。  
  
## <a name="applies-to"></a>適用於  
 [資料錄集物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [CompareBookmarks 方法範例 (VB)](../../../ado/reference/ado-api/comparebookmarks-method-example-vb.md)   
 [CompareBookmarks 方法範例 （VC + +）](../../../ado/reference/ado-api/comparebookmarks-method-example-vc.md)   
 [書籤 屬性 (ADO)](../../../ado/reference/ado-api/bookmark-property-ado.md)

