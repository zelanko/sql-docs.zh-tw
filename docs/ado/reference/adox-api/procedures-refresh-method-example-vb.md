---
title: "程序重新整理方法範例 (VB) |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- Refresh method [ADOX], Visual Basic example
ms.assetid: 499679bd-287b-487d-bdfb-3803abffec1c
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d0a9122b1adaa6d5a070bb568605b20a04199d95
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="procedures-refresh-method-example-vb"></a>程序重新整理方法範例 (VB)
下列程式碼會示範如何重新整理[程序](../../../ado/reference/adox-api/procedures-collection-adox.md)集合[目錄](../../../ado/reference/adox-api/catalog-object-adox.md)。 這必要之前[程序](../../../ado/reference/adox-api/procedure-object-adox.md)物件從**目錄**可以存取。  
  
```  
' BeginProceduresRefreshVB  
Sub Main()  
    On Error GoTo ProcedureRefreshError  
  
    Dim cat As New ADOX.Catalog  
  
    ' Open the Catalog  
    cat.ActiveConnection = _  
        "Provider='Microsoft.Jet.OLEDB.4.0';" & _  
        "Data Source='Northwind.mdb';"  
  
    ' Refresh the Procedures collection  
    cat.Procedures.Refresh  
  
    'Clean up  
    Set cat.ActiveConnection = Nothing  
    Set cat = Nothing  
    Exit Sub  
  
ProcedureRefreshError:  
    Set cat = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
' EndProceduresRefreshVB  
```  
  
## <a name="see-also"></a>另請參閱  
 [目錄物件 (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md)   
 [程序集合 (ADOX)](../../../ado/reference/adox-api/procedures-collection-adox.md)   
 [重新整理方法 (ADO)](../../../ado/reference/ado-api/refresh-method-ado.md)

