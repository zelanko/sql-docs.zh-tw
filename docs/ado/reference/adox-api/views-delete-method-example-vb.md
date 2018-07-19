---
title: 檢視刪除方法的範例 (VB) |Microsoft 文件
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- Delete method [ADOX]
ms.assetid: 17df2a83-4166-4df8-8c17-0a33aaac8582
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 44f4fc8e6b20daf215a9ef16bd1bc86dd49946f7
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/11/2018
ms.locfileid: "35287308"
---
# <a name="views-delete-method-example-vb"></a>檢視刪除方法的範例 (VB)
下列程式碼示範如何使用[刪除](../../../ado/reference/adox-api/delete-method-adox-collections.md)從類別目錄中刪除檢視的方法。  
  
```  
' BeginDeleteViewVB  
Sub Main()  
    On Error GoTo DeleteViewError  
  
    Dim cat As New ADOX.Catalog  
  
    ' Open the catalog  
    cat.ActiveConnection = "Provider='Microsoft.Jet.OLEDB.4.0';" & _  
        "Data Source='Northwind.mdb';"  
  
    'Delete the View  
    cat.Views.Delete "AllCustomers"  
  
    'Clean up  
    Set cat.ActiveConnection = Nothing  
    Set cat = Nothing  
    Exit Sub  
  
DeleteViewError:  
    Set cat = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
' EndDeleteViewVB  
```  
  
## <a name="see-also"></a>另請參閱  
 [Delete 方法 （ADOX 集合）](../../../ado/reference/adox-api/delete-method-adox-collections.md)   
 [Views 集合 (ADOX)](../../../ado/reference/adox-api/views-collection-adox.md)
