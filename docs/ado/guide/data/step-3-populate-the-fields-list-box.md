---
title: 步驟3：填入 [欄位] 清單方塊 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 315c32dc-aeb1-4629-b30e-87b44e8f84d1
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9d7f351b90030e755dde8ad13905ef4533eff08e
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "67924055"
---
# <a name="step-3-populate-the-fields-list-box"></a>步驟 3：填入 [欄位] 清單方塊
若要填入 [欄位] 清單方塊，請將下列程式碼插入到的`lstMain`Click 事件處理常式中：  
  
```  
Private Sub lstMain_Click()  
    Dim rec As Record  
    Dim rs As Recordset  
    Set rec = New Record  
    Set rs = New Recordset  
    grs.MoveFirst  
    grs.Move lstMain.ListIndex  
    lstDetails.Clear  
    rec.Open grs  
    Select Case rec.RecordType  
        Case adCollectionRecord:  
            Set rs = rec.GetChildren  
            While Not rs.EOF  
                lstDetails.AddItem rs(0)  
                rs.MoveNext  
            Wend  
        Case adSimpleRecord:  
            recFields rec, lstDetails, txtDetails  
  
        Case adStructDoc:  
    End Select  
  
End Sub  
```  
  
 此程式碼會分別宣告和具現化本機記錄`rec`和`rs`記錄集物件。  
  
 對應到中`lstMain`所選資源的資料列會成為的目前資料`grs`列。 然後會清除 [詳細資料] 清單`rec`框，並以目前的`grs`資料列開啟做為來源。  
  
 如果資源是[RecordType](../../../ado/reference/ado-api/recordtype-property-ado.md)所指定的集合記錄，則會在 rec 的子`rs`系上開啟本機記錄集。然後`lstDetails`填入的資料列中的值`rs`。  
  
 如果資源是簡單的記錄， `recFields`則會呼叫。 如需的詳細`recFields`資訊，請參閱下一個步驟。  
  
 如果資源是結構化檔，則不會執行任何程式碼。  
  
## <a name="see-also"></a>另請參閱  
 [網際網路發佈案例](../../../ado/guide/data/internet-publishing-scenario.md)   
 [步驟2：初始化主要清單方塊](../../../ado/guide/data/step-2-initialize-the-main-list-box.md)   
 [步驟 4：填入 [詳細資料] 文字方塊](../../../ado/guide/data/step-4-populate-the-details-text-box.md)
