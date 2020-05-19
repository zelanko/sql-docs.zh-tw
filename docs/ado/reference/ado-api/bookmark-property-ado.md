---
title: Bookmark 屬性（ADO） |Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 6b1c27eb728c3cd368b4d2acc10609785c06514a
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82748613"
---
# <a name="bookmark-property-ado"></a>Bookmark 屬性 (ADO)
表示可唯一識別[記錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件中目前記錄的書簽，或將**記錄集**物件中的目前記錄設定為有效書簽所識別的記錄。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回評估為有效書簽的**Variant**運算式。  
  
## <a name="remarks"></a>備註  
 使用 [**書簽**] 屬性可儲存目前記錄的位置，並在任何時間返回該記錄。 書簽僅適用于支援書簽功能的**記錄集**物件。  
  
 當您開啟**記錄集**物件時，它的每個記錄都有唯一的書簽。 若要儲存目前記錄的書簽，請將 [**書簽**] 屬性的值指派給變數。 若要在移至不同的記錄之後隨時快速地返回該記錄，請將**記錄集**物件的 [**書簽**] 屬性設定為該變數的值。  
  
 使用者可能無法查看書簽的值。 此外，使用者不應該預期書簽可以直接比較，因為兩個參考相同記錄的書簽可能會有不同的值。  
  
 如果您使用[Clone](../../../ado/reference/ado-api/clone-method-ado.md)方法來建立**記錄集**物件的複本，則原始和重複**記錄集**物件的**書簽**屬性設定會相同，而且您可以交換使用它們。 不過，您無法從不同的**記錄集**物件中交替使用書簽，即使它們是從相同的來源或命令所建立。  
  
> [!NOTE]
>  **遠端資料服務使用量**在用戶端**記錄集**物件上使用時，[**書簽**] 屬性一律可以使用。  
  
## <a name="applies-to"></a>套用至  
 [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [BOF、EOF 和 Bookmark 屬性範例（VB）](../../../ado/reference/ado-api/bof-eof-and-bookmark-properties-example-vb.md)   
 [BOF、EOF 和 Bookmark 屬性範例（VC + +）](../../../ado/reference/ado-api/bof-eof-and-bookmark-properties-example-vc.md)   
 [Supports 方法](../../../ado/reference/ado-api/supports-method.md)
