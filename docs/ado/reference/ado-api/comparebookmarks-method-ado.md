---
title: CompareBookmarks 方法（ADO） |Microsoft Docs
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
ms.openlocfilehash: 0d737c2f031fa3ba630eabb7e52dff0e056c3390
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "67919592"
---
# <a name="comparebookmarks-method-ado"></a>CompareBookmarks 方法 (ADO)
比較兩個書簽，並傳回其相對值的指示。  
  
## <a name="syntax"></a>語法  
  
```  
  
result = recordset.CompareBookmarks(Bookmark1, Bookmark2)  
```  
  
## <a name="return-value"></a>傳回值  
 傳回[CompareEnum](../../../ado/reference/ado-api/compareenum.md)值，指出由其書簽表示之兩筆記錄的相對資料列位置。  
  
#### <a name="parameters"></a>參數  
 *Bookmark1*  
 第一個資料列的書簽。  
  
 *Bookmark2*  
 第二列的書簽。  
  
## <a name="remarks"></a>備註  
 書簽必須套用至相同的[記錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件，或**記錄集**物件及其[複製](../../../ado/reference/ado-api/clone-method-ado.md)。 您無法可靠地比較來自不同**記錄集**物件的書簽，即使它們是從相同的來源或命令所建立。 您也不能比較其基礎提供者不支援比較之**記錄集**物件的書簽。  
  
 書簽可唯一識別**記錄集**物件中的資料列。 使用目前資料列的 [[書簽](../../../ado/reference/ado-api/bookmark-property-ado.md)] 屬性來取得其書簽。  
  
 由於書簽的資料類型是每個提供者特有的，因此 ADO 會將它公開為**Variant**。 例如，SQL Server 書簽的類型為 DBTYPE_R8 （**Double**）。 ADO 會以**Double**的子類型，將此型別公開為**Variant** 。  
  
 比較書簽時，ADO 不會嘗試任何類型的強制型轉。 這些值只會傳遞給發生比較的提供者。 如果傳遞至**CompareBookmarks**方法的書簽儲存在不同類型的變數中，它可能會產生下列類型不符的錯誤：「引數的類型錯誤、不在可接受的範圍內，或彼此衝突」。  
  
 無效或格式不正確的書簽將會造成錯誤。  
  
## <a name="applies-to"></a>套用至  
 [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [CompareBookmarks 方法範例（VB）](../../../ado/reference/ado-api/comparebookmarks-method-example-vb.md)   
 [CompareBookmarks 方法範例（VC + +）](../../../ado/reference/ado-api/comparebookmarks-method-example-vc.md)   
 [Bookmark 屬性 (ADO)](../../../ado/reference/ado-api/bookmark-property-ado.md)
