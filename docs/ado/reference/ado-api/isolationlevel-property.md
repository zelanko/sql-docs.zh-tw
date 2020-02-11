---
title: IsolationLevel 屬性 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection15::IsolationLevel
helpviewer_keywords:
- IsolationLevel property
ms.assetid: ea84e4b2-fbf2-4eef-b9ce-796b22e21800
author: MightyPen
ms.author: genemi
ms.openlocfilehash: dc360bc91e977228a6f9139089a7bfa87d912e1f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67918445"
---
# <a name="isolationlevel-property"></a>IsolationLevel 屬性
表示[連接](../../../ado/reference/ado-api/connection-object-ado.md)物件的隔離層級。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回[IsolationLevelEnum](../../../ado/reference/ado-api/isolationlevelenum.md)值。 預設值為**adXactReadCommitted**。  
  
## <a name="remarks"></a>備註  
 使用**IsolationLevel**屬性來設定**連接**物件的隔離等級。 在下一次呼叫[BeginTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md)方法之前，設定不會生效。 如果您要求的隔離層級無法使用，提供者可能會傳回下一個較高層級的隔離，而不會更新**IsolationLevel**屬性。  
  
 **IsolationLevel**屬性為讀取/寫入。  
  
> [!NOTE]
>  **遠端資料服務使用量**在用戶端**連接**物件上使用時， **IsolationLevel**屬性只能設定為**adXactUnspecified**。 因為使用者在用戶端快取上使用已中斷連線的**記錄集**物件，所以可能會有多使用者的問題。 比方說，當兩個不同的使用者嘗試更新相同的記錄時，遠端資料服務只會允許更新記錄的使用者先「獲勝」。 第二個使用者的更新要求將會失敗，併發生錯誤。  
  
## <a name="applies-to"></a>套用至  
 [Connection 物件 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [IsolationLevel 和 Mode 屬性範例（VB）](../../../ado/reference/ado-api/isolationlevel-and-mode-properties-example-vb.md)   
 [IsolationLevel 和 Mode 屬性範例（VC + +）](../../../ado/reference/ado-api/isolationlevel-and-mode-properties-example-vc.md)   
