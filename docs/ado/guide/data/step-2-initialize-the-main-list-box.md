---
description: 步驟 2：初始化 [主要] 清單方塊
title: 步驟2：初始化主要清單方塊 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: a1454493-1c86-46c2-ada8-d3c6fcdaf3c1
author: rothja
ms.author: jroth
ms.openlocfilehash: f746b454b18de7d88ca4c42d049eb058f671ba8e
ms.sourcegitcommit: 291ae8f6b72fd355f8f24ce5300339306293ea7e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2020
ms.locfileid: "88512294"
---
# <a name="step-2-initialize-the-main-list-box"></a>步驟 2：初始化 [主要] 清單方塊
若要宣告全域記錄和記錄集物件，請將下列程式碼插入至 Form1 的 (一般)  (宣告) ：  
  
```  
Option Explicit  
Dim grec As Record  
Dim grs As Recordset  
```  
  
 此程式碼會針對稍後在此案例中使用的記錄和記錄集物件，宣告全域物件參考。  
  
## <a name="to-connect-to-a-url-and-populate-lstmain"></a>若要連接到 URL 並填入 lstMain  
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
  
 此程式碼會具現化全域記錄和記錄集物件。 記錄物件會以 `grec` 指定為 ActiveConnection 的 URL 開啟。 如果 URL 存在，則會開啟;如果它不存在，則會加以建立。 請注意，您應該將取代 `https://servername/foldername/` 為您環境中的有效 URL。  
  
 記錄集物件 `grs` 是在記錄的子系上開啟 `grec` 。 然後 `lstMain` ，會填入發行至 URL 之資源的檔案名。  
  
## <a name="see-also"></a>另請參閱  
 [網際網路發佈案例](../../../ado/guide/data/internet-publishing-scenario.md)   
 [步驟1：設定 Visual Basic 專案](../../../ado/guide/data/step-1-set-up-the-visual-basic-project.md)   
 [步驟 3：填入 [欄位] 清單方塊](../../../ado/guide/data/step-3-populate-the-fields-list-box.md)
