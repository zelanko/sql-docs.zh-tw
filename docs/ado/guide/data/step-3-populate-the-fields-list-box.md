---
description: 步驟 3：填入 [欄位] 清單方塊
title: 步驟3：填入 [欄位] 清單方塊 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 315c32dc-aeb1-4629-b30e-87b44e8f84d1
author: rothja
ms.author: jroth
ms.openlocfilehash: acb2572accc19937f7f4ad278fc01aa0e5760a8a
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88979519"
---
# <a name="step-3-populate-the-fields-list-box"></a>步驟 3：填入 [欄位] 清單方塊
若要填入 [欄位] 清單方塊，請在的 Click 事件處理常式中插入下列程式碼 `lstMain` ：  
  
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
  
 此程式碼會分別宣告和具現化本機記錄和記錄集物件，以及 `rec` `rs` 。  
  
 對應到中所選取之資源的資料列 `lstMain` ，會成為目前的資料列 `grs` 。 接著會清除 [詳細資料] 清單方塊，並以目前的資料 `rec` 列 `grs` 做為來源來開啟。  
  
 如果資源是集合記錄，如 [RecordType](../../../ado/reference/ado-api/recordtype-property-ado.md)所指定，本機記錄集會 `rs` 在 rec 的子系上開啟。然後 `lstDetails` ，會填入的資料列中的值 `rs` 。  
  
 如果資源是簡單的記錄， `recFields` 則會呼叫。 如需的詳細資訊 `recFields` ，請參閱下一個步驟。  
  
 如果資源是結構化檔，則不會執行任何程式碼。  
  
## <a name="see-also"></a>另請參閱  
 [網際網路發佈案例](../../../ado/guide/data/internet-publishing-scenario.md)   
 [步驟2：初始化主要清單方塊](../../../ado/guide/data/step-2-initialize-the-main-list-box.md)   
 [步驟 4：填入 [詳細資料] 文字方塊](../../../ado/guide/data/step-4-populate-the-details-text-box.md)
