---
description: Connection Close 方法、Table Type 屬性範例 (VB)
title: Connection Close 方法、Table Type 屬性範例 (VB) |Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: a77ff78be14566f472af277459b2bdaa52aad748
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88440230"
---
# <a name="connection-close-method-table-type-property-example-vb"></a>Connection Close 方法、Table Type 屬性範例 (VB)
將 [ActiveConnection](../../../ado/reference/adox-api/activeconnection-property-adox.md) 屬性設定為 **Nothing** 時，應該會關閉與目錄的連接。 相關聯的集合將會是空的。 從目錄中的架構物件建立的任何物件都將會是孤立的。 這些已快取之物件上的任何屬性仍可供使用，但嘗試讀取需要對提供者呼叫的屬性將會失敗。  
  
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
  
 關閉用來開啟目錄的 [連接](../../../ado/reference/ado-api/connection-object-ado.md) 物件，其效果與將 **ActiveConnection** 屬性設定為 **Nothing**一樣。  
  
```  
Attribute VB_Name = "Connection"  
```  
  
## <a name="see-also"></a>另請參閱  
 [ActiveConnection 屬性 (ADOX) ](../../../ado/reference/adox-api/activeconnection-property-adox.md)   
 [ (ADOX) 的目錄物件 ](../../../ado/reference/adox-api/catalog-object-adox.md)   
 [資料行物件 (ADOX) ](../../../ado/reference/adox-api/column-object-adox.md)   
 [資料行集合 (ADOX) ](../../../ado/reference/adox-api/columns-collection-adox.md)   
 [資料表物件 (ADOX) ](../../../ado/reference/adox-api/table-object-adox.md)   
 [資料表集合 (ADOX) ](../../../ado/reference/adox-api/tables-collection-adox.md)   
 [Type 屬性 (Table) (ADOX)](../../../ado/reference/adox-api/type-property-table-adox.md)
