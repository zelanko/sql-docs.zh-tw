---
title: "書籤屬性 (ADO) |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Recordset15::Bookmark
helpviewer_keywords:
- Bookmark property [ADO]
ms.assetid: 481dcc93-487b-490e-ac58-a1e9b2ebfd43
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3c6076acd2bde7e82bf142bad76093d582106877
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/09/2018
---
# <a name="bookmark-property-ado"></a>書籤 屬性 (ADO)
指出目前的記錄中的唯一識別書籤[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件或設定目前資料錄**資料錄集**有效書籤所識別的記錄中的物件。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回**Variant**評估為有效的書籤的運算式。  
  
## <a name="remarks"></a>備註  
 使用**書籤**儲存目前記錄的位置並隨時返回至該記錄的屬性。 只在可用的書籤**資料錄集**支援書籤功能的物件。  
  
 當您開啟**資料錄集**物件，其記錄的每個都有唯一的書籤。 若要儲存目前的資料錄的書籤，來指定的值**書籤**變數的屬性。 若要快速回到該記錄移動到不同記錄之後，任何時候，設定**資料錄集**物件的**書籤**屬性設為該變數的值。  
  
 使用者可能無法檢視書籤的值。 此外，使用者不應預期是直接比較的書籤。 兩個參考同一筆記錄的書籤可能有不同的值。  
  
 如果您使用[複製](../../../ado/reference/ado-api/clone-method-ado.md)方法來建立一份**資料錄集**物件**書籤**原始和重複的屬性設定**資料錄集**物件相同，且您可以交換使用。 不過，您無法使用從不同的書籤**資料錄集**物件交替使用，即使它們已建立從相同來源或命令。  
  
> [!NOTE]
>  **遠端資料服務使用量**使用用戶端時**資料錄集**物件**書籤**屬性一律為可用。  
  
## <a name="applies-to"></a>適用於  
 [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [BOF、 EOF 和書籤屬性範例 (VB)](../../../ado/reference/ado-api/bof-eof-and-bookmark-properties-example-vb.md)   
 [BOF、 EOF 和書籤屬性範例 （VC + +）](../../../ado/reference/ado-api/bof-eof-and-bookmark-properties-example-vc.md)   
 [Supports 方法](../../../ado/reference/ado-api/supports-method.md)
