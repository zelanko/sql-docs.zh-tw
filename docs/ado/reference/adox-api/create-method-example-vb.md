---
title: "Create 方法範例 (VB) |Microsoft 文件"
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
- Create method [ADOX], Visual Basic example
ms.assetid: d7ea0244-596a-404e-8f30-71cadab8d8fc
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 5211692bd7bcaf7d2fc008e1c801d8346f5ea432
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="create-method-example-vb"></a>Create 方法範例 (VB)
下列程式碼示範如何建立新的 Microsoft Jet 資料庫與[建立](../../../ado/reference/adox-api/create-method-adox.md)方法。  
  
```  
Attribute VB_Name = "Create"  
Option Explicit  
  
' BeginCreateDatabseVB  
Sub CreateDatabase()  
    On Error GoTo CreateDatabaseError  
  
    Dim cat As New ADOX.Catalog  
    cat.Create "Provider='Microsoft.Jet.OLEDB.4.0';Data Source='new.mdb'"  
  
    'Clean up  
    Set cat = Nothing  
    Exit Sub  
  
CreateDatabaseError:  
    Set cat = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
' EndCreateDatabaseVB  
```  
  
## <a name="see-also"></a>另請參閱  
 [目錄物件 (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md)   
 [建立方法 (ADOX)](../../../ado/reference/adox-api/create-method-adox.md)

