---
title: 步驟 2： 初始化主清單方塊 |Microsoft 文件
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: a1454493-1c86-46c2-ada8-d3c6fcdaf3c1
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e8272c721c2717df494db5ead86716900f44c46e
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/18/2018
---
# <a name="step-2-initialize-the-main-list-box"></a>步驟 2： 初始化主清單方塊
若要宣告全域記錄和資料錄集物件，將下列程式碼插入 （一般） （宣告） form1:  
  
```  
Option Explicit  
Dim grec As Record  
Dim grs As Recordset  
```  
  
 此程式碼會宣告將稍後在此案例中使用的記錄和資料錄集物件的全域物件參考。  
  
## <a name="to-connect-to-a-url-and-populate-lstmain"></a>連接到 URL，並填入 lstMain  
 將下列程式碼插入表單 Load 事件處理常式 form1:  
  
```  
Private Sub Form_Load()  
    Set grec = New Record  
    Set grs = New Recordset  
    grec.Open "", "URL=http://servername/foldername/", , _  
        adOpenIfExists Or adCreateCollection  
    Set grs = grec.GetChildren  
    While Not grs.EOF  
        lstMain.AddItem grs(0)  
        grs.MoveNext  
    Wend  
End Sub  
```  
  
 此程式碼會具現化的全域記錄和資料錄集物件。 記錄物件`grec`，開啟具有指定為 ActiveConnection 的 URL。 如果 URL 存在，會將它開啟。如果已經存在，它會建立它。 請注意，您應該取代"http://servername/foldername/」 具有有效的 URL 從您的環境。  
  
 資料錄集物件， `grs`，開啟資料錄的子系`grec`。 然後`lstMain`會填入已發行的 url 資源的檔案名稱。  
  
## <a name="see-also"></a>另請參閱  
 [網際網路發佈案例](../../../ado/guide/data/internet-publishing-scenario.md)   
 [步驟 1： 設定 Visual Basic 專案](../../../ado/guide/data/step-1-set-up-the-visual-basic-project.md)   
 [步驟 3：填入 [欄位] 清單方塊](../../../ado/guide/data/step-3-populate-the-fields-list-box.md)
