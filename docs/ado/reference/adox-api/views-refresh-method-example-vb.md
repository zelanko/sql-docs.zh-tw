---
title: "檢視重新整理方法範例 (VB) |Microsoft 文件"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- Refresh method [ADOX]
ms.assetid: cdad2d66-6ade-40dc-9e74-e40cfa9bc127
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b6e526091804e36790f79a051399ff69e479df4a
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="views-refresh-method-example-vb"></a>檢視重新整理方法範例 (VB)
下列程式碼會示範如何重新整理[檢視](../../../ado/reference/adox-api/views-collection-adox.md)集合[目錄](../../../ado/reference/adox-api/catalog-object-adox.md)。 這必要之前[檢視](../../../ado/reference/adox-api/view-object-adox.md)物件從**目錄**可以存取。  
  
```  
' BeginViewsRefreshVB  
Sub Main()  
    On Error GoTo ProcedureViewsRefreshError  
  
    Dim cat As New ADOX.Catalog  
  
    ' Open the catalog.  
    cat.ActiveConnection = "Provider='Microsoft.Jet.OLEDB.4.0';" & _  
        "Data Source='Northwind.mdb';"  
  
    ' Refresh the Procedures collection.  
    cat.Views.Refresh  
  
    'Clean up  
    Set cat = Nothing  
    Exit Sub  
  
ProcedureViewsRefreshError:  
  
    If Not cat Is Nothing Then  
        Set cat = Nothing  
    End If  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
' EndViewsRefreshVB  
```  
  
## <a name="see-also"></a>另請參閱  
 [重新整理方法 (ADO)](../../../ado/reference/ado-api/refresh-method-ado.md)   
 [檢視集合 (ADOX)](../../../ado/reference/adox-api/views-collection-adox.md)

