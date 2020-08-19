---
description: Create 方法範例 (VB)
title: " (VB) 建立方法範例 |Microsoft Docs"
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 40a50d983365285ccf0001f46450613bdf78bd87
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88440200"
---
# <a name="create-method-example-vb"></a>Create 方法範例 (VB)
下列程式碼顯示如何使用 [create](../../../ado/reference/adox-api/create-method-adox.md) 方法建立新的 Microsoft Jet 資料庫。  
  
```  
Attribute VB_Name = "Create"  
Option Explicit  
  
' BeginCreateDatabaseVB  
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
 [ (ADOX) 的目錄物件 ](../../../ado/reference/adox-api/catalog-object-adox.md)   
 [Create 方法 (ADOX)](../../../ado/reference/adox-api/create-method-adox.md)
