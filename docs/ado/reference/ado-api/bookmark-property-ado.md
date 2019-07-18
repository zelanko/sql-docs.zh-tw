---
title: Bookmark 屬性 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 03/20/2018
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::Bookmark
helpviewer_keywords:
- Bookmark property [ADO]
ms.assetid: 481dcc93-487b-490e-ac58-a1e9b2ebfd43
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 48b1c90b59b220841aa45f618fdfda5ff2db82da
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67920343"
---
# <a name="bookmark-property-ado"></a>Bookmark 屬性 (ADO)
表示唯一識別目前的記錄中的書籤[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件，或設定目前資料錄**資料錄集**物件的有效書籤所識別的記錄。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回**Variant**評估為有效的書籤的運算式。  
  
## <a name="remarks"></a>備註  
 使用**書籤**儲存目前記錄的位置，並隨時返回至該記錄的屬性。 書籤是僅適用於**資料錄集**支援書籤功能的物件。  
  
 當您開啟**資料錄集**物件，其記錄的每個都有唯一的書籤。 若要儲存目前的資料錄的書籤，請將指派的值**書籤**給變數的屬性。 若要快速移至不同的記錄之後隨時返回至該記錄，將**Recordset**物件的**書籤**屬性設為該變數的值。  
  
 使用者可能無法檢視書籤的值。 此外，使用者不應該指望書籤，以相當直接，因為兩個參考同一筆記錄的書籤可能會有不同的值。  
  
 如果您使用[複製品](../../../ado/reference/ado-api/clone-method-ado.md)方法來建立一份**資料錄集**物件**書籤**的原始和重複的屬性設定**資料錄集**物件相同，且您可以交換使用。 不過，您無法使用從不同的書籤**資料錄集**交替，物件，即使它們已建立從相同的原始碼或命令。  
  
> [!NOTE]
>  **遠端資料服務使用量**用戶端上使用時**資料錄集**物件**書籤**屬性一律會是可用。  
  
## <a name="applies-to"></a>適用於  
 [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [BOF、 EOF 和 Bookmark 屬性範例 (VB)](../../../ado/reference/ado-api/bof-eof-and-bookmark-properties-example-vb.md)   
 [BOF、 EOF 和 Bookmark 屬性範例 （VC + +）](../../../ado/reference/ado-api/bof-eof-and-bookmark-properties-example-vc.md)   
 [Supports 方法](../../../ado/reference/ado-api/supports-method.md)
