---
description: Bookmark 屬性 (ADO)
title: " (ADO) 的書簽屬性 |Microsoft Docs"
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: 755397c0cf1b16243cdfa2d7777af487b7629b6e
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88975769"
---
# <a name="bookmark-property-ado"></a>Bookmark 屬性 (ADO)
指出可唯一識別 [記錄集](./recordset-object-ado.md) 物件中目前記錄的書簽，或將 **記錄集** 物件中的目前記錄設定為有效書簽所識別的記錄。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回評估為有效書簽的 **Variant** 運算式。  
  
## <a name="remarks"></a>備註  
 您可以使用 [ **書簽** ] 屬性來儲存目前記錄的位置，並隨時返回該記錄。 書簽只適用于支援書簽功能的 **記錄集** 物件。  
  
 當您開啟 **記錄集** 物件時，每一個記錄都會有唯一的書簽。 若要儲存目前記錄的書簽，請將 [ **書簽** ] 屬性的值指派給變數。 若要在移至不同的記錄之後隨時快速返回該記錄，請將 **記錄集** 物件的 [ **書簽** ] 屬性設定為該變數的值。  
  
 使用者可能無法查看書簽的值。 此外，使用者不應該預期書簽可直接進行比較，因為兩個參考相同記錄的書簽可能會有不同的值。  
  
 如果您使用[Clone](./clone-method-ado.md)方法來建立**記錄集**物件的複本，則原始和重複**記錄集**物件的 [**書簽**] 屬性設定都相同，而且您可以交換使用它們。 不過，您無法從不同的 **記錄集** 物件交替使用書簽，即使它們是從相同的來源或命令所建立。  
  
> [!NOTE]
>  **遠端資料服務使用量** 在用戶端 **記錄集** 物件上使用時，[ **書簽** ] 屬性一律為可用。  
  
## <a name="applies-to"></a>套用至  
 [Recordset 物件 (ADO)](./recordset-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [BOF、EOF 和 Bookmark 屬性範例 (VB) ](./bof-eof-and-bookmark-properties-example-vb.md)   
 [ (VC + +) 的 BOF、EOF 和 Bookmark 屬性範例 ](./bof-eof-and-bookmark-properties-example-vc.md)   
 [Supports 方法](./supports-method.md)