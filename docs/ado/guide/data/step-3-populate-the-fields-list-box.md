---
title: 步驟 3： 擴展欄位的清單方塊 |Microsoft 文件
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 315c32dc-aeb1-4629-b30e-87b44e8f84d1
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: db988df4840e089564b056694bf8186694075fe1
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="step-3-populate-the-fields-list-box"></a>步驟 3： 擴展欄位的清單方塊
若要填入欄位 清單方塊中，插入下列程式碼的 Click 事件處理常式`lstMain`:  
  
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
  
 此程式碼會宣告並具現化本機記錄和資料錄集物件，`rec`和`rs`分別。  
  
 在所選取的資源對應的資料列`lstMain`成為目前資料列`grs`。 然後會清除詳細資料清單方塊和`rec`開啟與目前資料列`grs`做為來源。  
  
 如果資源是集合的記錄時，所指定[RecordType](../../../ado/reference/ado-api/recordtype-property-ado.md)，本機資料錄集`rs`rec 的子系上開啟。然後`lstDetails`填滿資料的資料列的值`rs`。  
  
 如果資源至少有一個簡單的資料錄，`recFields`呼叫。 如需有關`recFields`，請參閱下一個步驟。  
  
 如果資源是結構化文件，被不實作任何程式碼。  
  
## <a name="see-also"></a>另請參閱  
 [網際網路發佈案例](../../../ado/guide/data/internet-publishing-scenario.md)   
 [步驟 2： 初始化主清單方塊](../../../ado/guide/data/step-2-initialize-the-main-list-box.md)   
 [步驟 4：填入 [詳細資料] 文字方塊](../../../ado/guide/data/step-4-populate-the-details-text-box.md)
