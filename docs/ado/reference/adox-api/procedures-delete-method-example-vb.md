---
description: Procedures Delete 方法範例 (VB)
title: 程式 Delete 方法範例 (VB) |Microsoft Docs
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
- Delete method [ADOX], Visual Basic example
ms.assetid: 94f1ac93-e778-4a40-a85e-94bce5316ac7
author: rothja
ms.author: jroth
ms.openlocfilehash: c3f7d26eded130f22bda4f707f451ddf78c4b3d7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88439610"
---
# <a name="procedures-delete-method-example-vb"></a>Procedures Delete 方法範例 (VB)
下列程式碼示範如何使用 procedure 集合的 [delete](../../../ado/reference/adox-api/delete-method-adox-collections.md) 方法刪除 [程式](../../../ado/reference/adox-api/procedures-collection-adox.md) 。  
  
```  
' BeginDeleteProcedureVB  
Sub Main()  
    On Error GoTo DeleteProcedureError  
  
    Dim cat As New ADOX.Catalog  
  
    ' Open the catalog.  
    cat.ActiveConnection = _  
        "Provider='Microsoft.Jet.OLEDB.4.0';" & _  
        "Data Source='Northwind.mdb';"  
  
    ' Delete the procedure.  
    cat.Procedures.Delete "CustomerById"  
  
    'Clean up.  
    Set cat.ActiveConnection = Nothing  
    Set cat = Nothing  
    Exit Sub  
  
DeleteProcedureError:  
    Set cat = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
' EndDeleteProcedureVB  
```  
  
## <a name="see-also"></a>另請參閱  
 [ActiveConnection 屬性 (ADOX) ](../../../ado/reference/adox-api/activeconnection-property-adox.md)   
 [ (ADOX) 的目錄物件 ](../../../ado/reference/adox-api/catalog-object-adox.md)   
 [ (ADOX 集合的 Delete 方法) ](../../../ado/reference/adox-api/delete-method-adox-collections.md)   
 [Procedure 物件 (ADOX) ](../../../ado/reference/adox-api/procedure-object-adox.md)   
 [Procedures 集合 (ADOX)](../../../ado/reference/adox-api/procedures-collection-adox.md)
