---
description: GetPermissions 和 SetPermissions 方法範例 (VB)
title: GetPermissions 和 SetPermissions 方法範例 (VB) |Microsoft Docs
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
- SetPermissions method [ADOX], Visual Basic example
- GetPermissions method [ADOX], Visual Basic example
ms.assetid: aa366d98-8c7a-4189-bdd8-1d663b243d33
author: rothja
ms.author: jroth
ms.openlocfilehash: 59984877f4c8d86b9adc18b841b17c92740e8602
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88440050"
---
# <a name="getpermissions-and-setpermissions-methods-example-vb"></a>GetPermissions 和 SetPermissions 方法範例 (VB)
此範例示範 [GetPermissions](../../../ado/reference/adox-api/getpermissions-method-adox.md) 和 [SetPermissions](../../../ado/reference/adox-api/setpermissions-method-adox.md) 方法。 下列程式碼會為系統管理員使用者提供 Orders 資料表的完整存取權。  
  
```  
' BeginGrantPermissionsVB  
Sub GrantPermissions()  
    On Error GoTo GrantPermissionsError  
  
    Dim cnn As New ADODB.Connection  
    Dim cat As New ADOX.Catalog  
    Dim lngPerm As Long  
  
    ' Opens a connection to the northwind database  
    ' using the Microsoft Jet 4.0 provider  
    cnn.Provider = "Microsoft.Jet.OLEDB.4.0"  
    cnn.Open "Data Source='Northwind.mdb';" & _  
        "jet oledb:system database=" & _  
        "'system.mdw'"  
  
    Set cat.ActiveConnection = cnn  
  
    ' Retrieve original permissions  
    lngPerm = cat.Users("admin").GetPermissions("Orders", adPermObjTable)  
    Debug.Print "Original permissions: " & Str(lngPerm)  
  
    ' Revoke all permissions  
    cat.Users("admin").SetPermissions "Orders", adPermObjTable, _  
        adAccessRevoke, adRightFull  
  
    ' Display permissions  
    Debug.Print "Revoked permissions: " & _  
        Str(cat.Users("admin").GetPermissions("Orders", adPermObjTable))  
  
    ' Give the Admin user full rights on the orders object  
    cat.Users("admin").SetPermissions "Orders", adPermObjTable, _  
        adAccessSet, adRightFull  
  
    ' Display permissions  
    Debug.Print "Full permissions: " & _  
        Str(cat.Users("admin").GetPermissions("Orders", adPermObjTable))  
  
    ' Restore original permissions  
    cat.Users("admin").SetPermissions "Orders", adPermObjTable, _  
        adAccessSet, lngPerm  
  
    ' Display permissions  
    Debug.Print "Final permissions: " & _  
        Str(cat.Users("admin").GetPermissions("Orders", adPermObjTable))  
  
    'Clean up  
    cnn.Close  
    Set cat = Nothing  
    Set cnn = Nothing  
    Exit Sub  
  
GrantPermissionsError:  
  
    Set cat = Nothing  
  
    If Not cnn Is Nothing Then  
        If cnn.State = adStateOpen Then cnn.Close  
    End If  
    Set cnn = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
  
End Sub  
' EndGrantPermissionsVB  
```  
  
## <a name="see-also"></a>另請參閱  
 [ (ADOX) 的目錄物件 ](../../../ado/reference/adox-api/catalog-object-adox.md)   
 [GetPermissions 方法 (ADOX) ](../../../ado/reference/adox-api/getpermissions-method-adox.md)   
 [SetPermissions 方法 (ADOX) ](../../../ado/reference/adox-api/setpermissions-method-adox.md)   
 [使用者物件 (ADOX) ](../../../ado/reference/adox-api/user-object-adox.md)   
 [Users 集合 (ADOX)](../../../ado/reference/adox-api/users-collection-adox.md)
