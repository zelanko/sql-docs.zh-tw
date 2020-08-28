---
description: Views 集合、CommandText 屬性範例 (VB)
title: Views 集合、CommandText 屬性範例 (VB) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- CommandText property [ADOX]
- Views collection [ADOX], Visual Basic example
ms.assetid: a05a0190-352d-44ff-9488-0c94e9fb656e
author: rothja
ms.author: jroth
ms.openlocfilehash: da3685ba69f34fce5a97d0621917883f0e16e6b1
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88982859"
---
# <a name="views-collection-commandtext-property-example-vb"></a>Views 集合、CommandText 屬性範例 (VB)
下列程式碼示範如何使用 [Command](./command-property-adox.md) 屬性來更新視圖的文字。  
  
```  
' BeginViewsCollectionVB  
Sub Main()  
    On Error GoTo ViewTextError  
  
    Dim cnn As New ADODB.Connection  
    Dim cat As New ADOX.Catalog  
    Dim cmd As New ADODB.Command  
  
    ' Open the connection.  
    cnn.Open _  
        "Provider='Microsoft.Jet.OLEDB.4.0';" & _  
        "Data Source='Northwind.mdb';"  
  
    ' Open the catalog.  
    Set cat.ActiveConnection = cnn  
  
    ' Get the command.  
    Set cmd = cat.Views("AllCustomers").Command  
  
    ' Update the CommandText of the command.  
    cmd.CommandText = _  
    "Select CustomerId, CompanyName, ContactName From Customers"  
  
    ' Update the view.  
    Set cat.Views("AllCustomers").Command = cmd  
  
    'Clean up.  
    cnn.Close  
    Set cat = Nothing  
    Set cmd = Nothing  
    Set cnn = Nothing  
    Exit Sub  
  
ViewTextError:  
  
    Set cat = Nothing  
    Set cmd = Nothing  
  
    If Not cnn Is Nothing Then  
        If cnn.State = adStateOpen Then cnn.Close  
    End If  
    Set cnn = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
' EndViewsCollectionVB  
```  
  
## <a name="see-also"></a>另請參閱  
 [ActiveConnection 屬性 (ADOX) ](./activeconnection-property-adox.md)   
 [ (ADOX) 的目錄物件 ](./catalog-object-adox.md)   
 [命令屬性 (ADOX) ](./command-property-adox.md)   
 [View Object (ADOX) ](./view-object-adox.md)   
 [Views 集合 (ADOX)](./views-collection-adox.md)