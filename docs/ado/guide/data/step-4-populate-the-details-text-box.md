---
title: "步驟 4： 填入 [詳細資料] 文字方塊中 |Microsoft 文件"
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
ms.assetid: cb4273e2-c907-4a86-a621-3bf110088228
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 78f0c3e899400e1bf56a9b00ce1521a23b638189
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/09/2018
---
# <a name="step-4-populate-the-details-text-box"></a>步驟 4： 填入 [詳細資料] 文字方塊中
若要填入 [詳細資料] 文字方塊中，建立新的副程式，名為**recFields**並插入下列程式碼：  
  
```  
Sub recFields(r As Record, l As ListBox, t As TextBox)  
    Dim f As Field  
    Dim s As Stream  
    Set s = New Stream  
    Dim str As String  
  
    For Each f In r.Fields  
        l.AddItem f.Name & ": " & f.Value  
    Next  
    t.Text = ""  
    If r!RESOURCE_CONTENTCLASS = "text/plain" Then  
        s.Open r, adModeRead, adOpenStreamFromRecord  
        str = s.ReadText(1)  
        s.Position = 0  
        If Asc(Mid(str, 1, 1)) = 63 Then '//63 = "?"  
            s.Charset = "ascii"  
            s.Type = adTypeText  
        End If  
        t.Text = s.ReadText(adReadAll)  
    End If  
End Sub  
```  
  
 此程式碼會填入`lstDetails`與欄位和簡單記錄傳遞給值`recFields`。 如果資源是文字檔案，從資源記錄開啟的文字資料流。 程式碼會判斷是否為 ASCII 字元集，和複製到資料流內容`txtDetails`。  
  
## <a name="see-also"></a>另請參閱  
 [網際網路發佈案例](../../../ado/guide/data/internet-publishing-scenario.md)   
 [步驟 3：填入 [欄位] 清單方塊](../../../ado/guide/data/step-3-populate-the-fields-list-box.md)
