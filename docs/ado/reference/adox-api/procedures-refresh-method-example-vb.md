---
title: 程式 Refresh 方法範例（VB） |Microsoft Docs
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
- Refresh method [ADOX], Visual Basic example
ms.assetid: 499679bd-287b-487d-bdfb-3803abffec1c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9b5201be26bfd9df41c9cb1d8908f59499520878
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67965370"
---
# <a name="procedures-refresh-method-example-vb"></a>Procedures Refresh 方法範例 (VB)
下列程式碼顯示如何重新整理[目錄](../../../ado/reference/adox-api/catalog-object-adox.md)的[程式](../../../ado/reference/adox-api/procedures-collection-adox.md)集合。 您必須先進行[此操作，](../../../ado/reference/adox-api/procedure-object-adox.md)才能存取來自**目錄**的程式物件。  
  
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
 [Catalog 物件（ADOX）](../../../ado/reference/adox-api/catalog-object-adox.md)   
 [程式集合（ADOX）](../../../ado/reference/adox-api/procedures-collection-adox.md)   
 [Refresh 方法 (ADO)](../../../ado/reference/ado-api/refresh-method-ado.md)
