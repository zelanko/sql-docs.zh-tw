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
author: rothja
ms.author: jroth
ms.openlocfilehash: 2ecedd516891e2f99a800da452573717f211ff60
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82760794"
---
# <a name="step-3-populate-the-fields-list-box"></a>步驟 3：填入 [欄位] 清單方塊
若要填入 [欄位] 清單方塊，請將下列程式碼插入到的 Click 事件處理常式中 `lstMain` ：  
  
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
  
 此程式碼會分別宣告和具現化本機記錄和記錄集物件 `rec` `rs` 。  
  
 對應到中所選資源的資料列 `lstMain` 會成為的目前資料列 `grs` 。 然後會清除 [詳細資料] 清單方塊，並以 `rec` 目前的資料列開啟 `grs` 做為來源。  
  
 如果資源是[RecordType](../../../ado/reference/ado-api/recordtype-property-ado.md)所指定的集合記錄，則會在 rec 的子系上開啟本機記錄集 `rs` 。然後 `lstDetails` 填入的資料列中的值 `rs` 。  
  
 如果資源是簡單的記錄， `recFields` 則會呼叫。 如需的詳細資訊 `recFields` ，請參閱下一個步驟。  
  
 如果資源是結構化檔，則不會執行任何程式碼。  
  
## <a name="see-also"></a>另請參閱  
 [網際網路發佈案例](../../../ado/guide/data/internet-publishing-scenario.md)   
 [步驟2：初始化主要清單方塊](../../../ado/guide/data/step-2-initialize-the-main-list-box.md)   
 [步驟 4：填入 [詳細資料] 文字方塊](../../../ado/guide/data/step-4-populate-the-details-text-box.md)
