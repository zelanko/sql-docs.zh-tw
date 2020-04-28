---
title: Connection Close 方法、Table Type 屬性範例（VB） |Microsoft Docs
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
- Close method [ADOX], Visual Basic example
- Type property [ADOX], Visual Basic example
ms.assetid: f88e7a3b-19ed-46e2-b2ce-3b611d9b8166
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4559a8d46852f37f2e828ce8f4abbd0e40845744
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "67966700"
---
# <a name="connection-close-method-table-type-property-example-vb"></a>Connection Close 方法、Table Type 屬性範例 (VB)
將[ActiveConnection](../../../ado/reference/adox-api/activeconnection-property-adox.md)屬性設定為 [**無**] 時，應該會關閉與目錄的連接。 相關聯的集合將會是空的。 從目錄中的架構物件建立的任何物件將會孤立。 已快取之物件上的任何屬性仍然可以使用，但嘗試讀取要求提供者呼叫的屬性將會失敗。  
  
```  
' BeginCloseConnectionVB  
Sub Main()  
    On Error GoTo CloseConnectionByNothingError  
  
    Dim cnn As New ADODB.Connection  
    Dim cat As New ADOX.Catalog  
    Dim tbl As ADOX.Table  
  
    cnn.Open "Provider='Microsoft.Jet.OLEDB.4.0';" & _  
        "Data Source= 'Northwind.mdb';"  
    Set cat.ActiveConnection = cnn  
    Set tbl = cat.Tables(0)  
    Debug.Print tbl.Type    ' Cache tbl.Type info  
    Set cat.ActiveConnection = Nothing  
    Debug.Print tbl.Type    ' tbl is orphaned  
    ' Previous line will succeed if this info was cached.  
    Debug.Print tbl.Columns(0).DefinedSize  
    ' Previous line will fail if this info has not been cached.  
  
    'Clean up.  
    cnn.Close  
    Set cat = Nothing  
    Set cnn = Nothing  
    Exit Sub  
  
CloseConnectionByNothingError:  
    Set cat = Nothing  
  
    If Not cnn Is Nothing Then  
        If cnn.State = adStateOpen Then cnn.Close  
    End If  
    Set cnn = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
' EndCloseConnectionVB  
```  
  
 關閉用來開啟目錄的[連接](../../../ado/reference/ado-api/connection-object-ado.md)物件，其效果應該與將**ActiveConnection**屬性設定為 [**無**] 相同。  
  
```  
Attribute VB_Name = "Connection"  
```  
  
## <a name="see-also"></a>另請參閱  
 [ActiveConnection 屬性（ADOX）](../../../ado/reference/adox-api/activeconnection-property-adox.md)   
 [Catalog 物件（ADOX）](../../../ado/reference/adox-api/catalog-object-adox.md)   
 [Column 物件（ADOX）](../../../ado/reference/adox-api/column-object-adox.md)   
 [Columns 集合（ADOX）](../../../ado/reference/adox-api/columns-collection-adox.md)   
 [Table 物件（ADOX）](../../../ado/reference/adox-api/table-object-adox.md)   
 [Tables 集合（ADOX）](../../../ado/reference/adox-api/tables-collection-adox.md)   
 [Type 屬性 (Table) (ADOX)](../../../ado/reference/adox-api/type-property-table-adox.md)
