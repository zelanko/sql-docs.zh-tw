---
title: 步驟 3：填入 [欄位] 清單方塊 |Microsoft Docs
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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67924055"
---
# <a name="step-3-populate-the-fields-list-box"></a>步驟 3：填入 [欄位] 清單方塊
若要填入的欄位 清單方塊中，插入下列程式碼的 Click 事件處理常式`lstMain`:  
  
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
  
 此程式碼會宣告並具現化區域的記錄和資料錄集物件`rec`和`rs`分別。  
  
 對應到資源中選取的資料列`lstMain`由目前資料列`grs`。 然後在詳細資料清單方塊已清除並`rec`開啟與目前資料列`grs`做為來源。  
  
 如果資源是集合的記錄時，所指定[RecordType](../../../ado/reference/ado-api/recordtype-property-ado.md)，本機的資料錄集`rs`rec 的子系上開啟。然後`lstDetails`中的資料列的值會填入`rs`。  
  
 如果資源是簡單的記錄，`recFields`呼叫。 如需詳細資訊`recFields`，請參閱下一個步驟。  
  
 如果資源是結構化文件，被不實作任何程式碼。  
  
## <a name="see-also"></a>另請參閱  
 [網際網路發佈案例](../../../ado/guide/data/internet-publishing-scenario.md)   
 [步驟 2：初始化 [主要] 清單方塊](../../../ado/guide/data/step-2-initialize-the-main-list-box.md)   
 [步驟 4：填入詳細資料 文字方塊](../../../ado/guide/data/step-4-populate-the-details-text-box.md)
