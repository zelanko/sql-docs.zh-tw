---
description: Catalog ActiveConnection 屬性範例 (VB)
title: 目錄 ActiveConnection 屬性範例 (VB) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- ActiveConnection property [ADOX], Visual Basic example
ms.assetid: bb3274b1-764d-43a7-a49f-ef55680ecd26
author: rothja
ms.author: jroth
ms.openlocfilehash: 4895f1ec08a0f10c93335fc36954f3a9098ffce4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88440410"
---
# <a name="catalog-activeconnection-property-example-vb"></a>Catalog ActiveConnection 屬性範例 (VB)
將 [ActiveConnection](../../../ado/reference/adox-api/activeconnection-property-adox.md) 屬性設定為有效的開啟連接會「開啟」目錄。 從開啟的目錄，您可以存取包含在該目錄內的架構物件。  
  
```  
' BeginOpenConnectionVB  
Sub Main()  
    On Error GoTo OpenConnectionError  
  
    Dim cnn As New ADODB.Connection  
    Dim cat As New ADOX.Catalog  
  
    cnn.Open "Provider='Microsoft.Jet.OLEDB.4.0';" & _  
        "Data Source= 'Northwind.mdb';"  
    Set cat.ActiveConnection = cnn  
    Debug.Print cat.Tables(0).Type  
  
    'Clean up  
    cnn.Close  
    Set cat = Nothing  
    Set cnn = Nothing  
    Exit Sub  
  
OpenConnectionError:  
  
    Set cat = Nothing  
  
    If Not cnn Is Nothing Then  
        If cnn.State = adStateOpen Then cnn.Close  
    End If  
    Set cnn = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
' EndOpenConnectionVB  
```  
  
 將 **ActiveConnection** 屬性設定為有效的連接字串也會「開啟」目錄。  
  
```  
Attribute VB_Name = "Catalog"  
```  
  
## <a name="see-also"></a>另請參閱  
 [ActiveConnection 屬性 (ADOX) ](../../../ado/reference/adox-api/activeconnection-property-adox.md)   
 [ (ADOX) 的目錄物件 ](../../../ado/reference/adox-api/catalog-object-adox.md)   
 [資料表物件 (ADOX) ](../../../ado/reference/adox-api/table-object-adox.md)   
 [資料表集合 (ADOX) ](../../../ado/reference/adox-api/tables-collection-adox.md)   
 [Type 屬性 (Table) (ADOX)](../../../ado/reference/adox-api/type-property-table-adox.md)
