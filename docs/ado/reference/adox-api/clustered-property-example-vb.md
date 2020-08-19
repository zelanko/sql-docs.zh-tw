---
description: Clustered 屬性範例 (VB)
title: " (VB) 的叢集屬性範例 |Microsoft Docs"
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
- Clustered property [ADOX], Visual Basic example
ms.assetid: 1cd30769-c8af-43e7-be27-12ed0434daa1
author: rothja
ms.author: jroth
ms.openlocfilehash: 647fe236ad7a616cbce54986f6a3ce3aba0db163
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88440350"
---
# <a name="clustered-property-example-vb"></a>Clustered 屬性範例 (VB)
此範例示範索引[的叢集屬性](../../../ado/reference/adox-api/clustered-property-adox.md)。 [Index](../../../ado/reference/adox-api/index-object-adox.md) 請注意，Microsoft Jet 資料庫不支援叢集索引，因此此範例會針對**Northwind**資料庫中所有**索引的叢集屬性傳回** **False** 。  
  
```  
' BeginClusteredVB  
Sub Main()  
    On Error GoTo ClusteredXError  
  
    Dim cnn As New ADODB.Connection  
    Dim cat As New ADOX.Catalog  
    Dim tblLoop As ADOX.Table  
    Dim idxLoop As ADOX.Index  
    Dim strCnn As String  
  
    strCnn = "Provider='SQLOLEDB';Data Source='MySqlServer';Initial Catalog='pubs';" & _  
        "Integrated Security='SSPI';"  
    ' Connect to the catalog.  
    cnn.Open strCnn  
    cat.ActiveConnection = cnn  
  
    ' Enumerate the tables.  
    For Each tblLoop In cat.Tables  
        'Enumerate the indexes.  
        For Each idxLoop In tblLoop.Indexes  
            Debug.Print tblLoop.Name & " " & _  
                idxLoop.Name & " " & idxLoop.Clustered  
        Next idxLoop  
    Next tblLoop  
  
    'Clean up.  
    cnn.Close  
    Set cat = Nothing  
    Set cnn = Nothing  
    Exit Sub  
  
ClusteredXError:  
  
    Set cat = Nothing  
  
    If Not cnn Is Nothing Then  
        If cnn.State = adStateOpen Then cnn.Close  
    End If  
    Set cnn = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
' EndClusteredVB  
```  
  
## <a name="see-also"></a>另請參閱  
 [ (ADOX) 的目錄物件 ](../../../ado/reference/adox-api/catalog-object-adox.md)   
 [叢集屬性 (ADOX) ](../../../ado/reference/adox-api/clustered-property-adox.md)   
 [ (ADOX) 的索引物件 ](../../../ado/reference/adox-api/index-object-adox.md)   
 [Table 物件 (ADOX)](../../../ado/reference/adox-api/table-object-adox.md)
