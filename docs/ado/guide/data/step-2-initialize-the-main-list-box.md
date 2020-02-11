---
title: 步驟2：初始化主要清單方塊 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: a1454493-1c86-46c2-ada8-d3c6fcdaf3c1
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8ad89d806f8a6774cb0fe2de056e30fd274a517c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67924089"
---
# <a name="step-2-initialize-the-main-list-box"></a>步驟 2：初始化 [主要] 清單方塊
若要宣告全域記錄和記錄集物件，請將下列程式碼插入 Form1 的（一般）（宣告）：  
  
```  
Option Explicit  
Dim grec As Record  
Dim grs As Recordset  
```  
  
 此程式碼會針對稍後將在此案例中使用的記錄和記錄集物件，宣告全域物件參考。  
  
## <a name="to-connect-to-a-url-and-populate-lstmain"></a>連接到 URL 並填入 lstMain  
 將下列程式碼插入 Form1 的表單載入事件處理常式：  
  
```  
Private Sub Form_Load()  
    Set grec = New Record  
    Set grs = New Recordset  
    grec.Open "", "URL=https://servername/foldername/", , _  
        adOpenIfExists Or adCreateCollection  
    Set grs = grec.GetChildren  
    While Not grs.EOF  
        lstMain.AddItem grs(0)  
        grs.MoveNext  
    Wend  
End Sub  
```  
  
 此程式碼會具現化全域記錄和記錄集物件。 記錄物件`grec`是以指定為 ACTIVECONNECTION 的 URL 開啟。 如果 URL 存在，則會開啟;如果尚未存在，則會建立它。 請注意，您應該將<https://servername/foldername/>"" 取代為您環境中的有效 URL。  
  
 記錄集物件`grs`會在記錄的子系上開啟`grec`。 然後`lstMain`會使用發佈至 URL 的資源檔名來填入。  
  
## <a name="see-also"></a>另請參閱  
 [網際網路發佈案例](../../../ado/guide/data/internet-publishing-scenario.md)   
 [步驟1：設定 Visual Basic 專案](../../../ado/guide/data/step-1-set-up-the-visual-basic-project.md)   
 [步驟 3：填入 [欄位] 清單方塊](../../../ado/guide/data/step-3-populate-the-fields-list-box.md)
