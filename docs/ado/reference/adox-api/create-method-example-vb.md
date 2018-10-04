---
title: Create 方法範例 (VB) |Microsoft Docs
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
- Create method [ADOX], Visual Basic example
ms.assetid: d7ea0244-596a-404e-8f30-71cadab8d8fc
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7532cc78f05271b6a3b3db8f6e74040b9ac50535
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47601937"
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
 [Catalog 物件 (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md)   
 [Create 方法 (ADOX)](../../../ado/reference/adox-api/create-method-adox.md)
