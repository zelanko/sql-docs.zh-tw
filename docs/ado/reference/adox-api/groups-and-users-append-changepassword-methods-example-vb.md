---
description: Groups 和 Users Append、ChangePassword 方法範例 (VB)
title: 群組和使用者附加、ChangePassword 方法範例 (VB) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- ChangePassword method [ADOX], Visual Basic example
- Append method [ADOX], Visual Basic example
ms.assetid: c9426757-9cdd-4a95-b506-d3d011569109
author: rothja
ms.author: jroth
ms.openlocfilehash: 824cf44560335152ac6079c4ff61f2177368447c
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88984379"
---
# <a name="groups-and-users-append-changepassword-methods-example-vb"></a>Groups 和 Users Append、ChangePassword 方法範例 (VB)
此範例示範[群組](./groups-collection-adox.md)的[附加](./append-method-adox-groups.md)方法，以及[使用者](./users-collection-adox.md)的[附加](./append-method-adox-users.md)方法，方法是將新的[群組](./group-object-adox.md)和新的[使用者](./user-object-adox.md)加入系統中。 新**群組**會附加至新**使用者**的**群組**集合。 因此，新的 **使用者** 會加入至 **群組**。 此外， [ChangePassword](./changepassword-method-adox.md) 方法是用來指定 **使用者** 密碼。  
  
> [!NOTE]
>  如果您要連接到支援 Windows 驗證的資料來源提供者，您應該在連接字串中指定 **Trusted_Connection = yes** 或 **整合式安全性 = SSPI** ，而不是使用者識別碼和密碼資訊。  
  
```  
' BeginGroupVB  
Sub Main()  
    On Error GoTo GroupXError  
  
    Dim cat As ADOX.Catalog  
    Dim usrNew As ADOX.User  
    Dim usrLoop As ADOX.User  
    Dim grpLoop As ADOX.Group  
  
    Set cat = New ADOX.Catalog  
  
    cat.ActiveConnection = "Provider='Microsoft.Jet.OLEDB.4.0';" & _  
        "Data Source='Northwind.mdb';" & _  
        "jet oledb:system database=" & _  
        "'system.mdw'"  
  
    With cat  
        'Create and append new group with a string.  
        .Groups.Append "Accounting"  
  
        ' Create and append new user with an object.  
        Set usrNew = New ADOX.User  
        usrNew.Name = "Pat Smith"  
        usrNew.ChangePassword "", "Password1"  
        .Users.Append usrNew  
  
        ' Make the user Pat Smith a member of the  
        ' Accounting group by creating and adding the  
        ' appropriate Group object to the user's Groups  
        ' collection. The same is accomplished if a User  
        ' object representing Pat Smith is created and  
        ' appended to the Accounting group Users collection  
        usrNew.Groups.Append "Accounting"  
  
        ' Enumerate all User objects in the  
        ' catalog's Users collection.  
        For Each usrLoop In .Users  
            Debug.Print "  " & usrLoop.Name  
            Debug.Print "    Belongs to these groups:"  
            ' Enumerate all Group objects in each User  
            ' object's Groups collection.  
            If usrLoop.Groups.Count <> 0 Then  
                For Each grpLoop In usrLoop.Groups  
                    Debug.Print "    " & grpLoop.Name  
                Next grpLoop  
            Else  
                Debug.Print "    [None]"  
            End If  
        Next usrLoop  
  
        ' Enumerate all Group objects in the default  
        ' workspace's Groups collection.  
        For Each grpLoop In .Groups  
            Debug.Print "  " & grpLoop.Name  
            Debug.Print "    Has as its members:"  
            ' Enumerate all User objects in each Group  
            ' object's Users collection.  
            If grpLoop.Users.Count <> 0 Then  
                For Each usrLoop In grpLoop.Users  
                    Debug.Print "    " & usrLoop.Name  
                Next usrLoop  
            Else  
                Debug.Print "    [None]"  
            End If  
        Next grpLoop  
  
        ' Delete new User and Group objects because this  
        ' is only a demonstration.  
        ' These two line are commented out because the sub "OwnersX" uses  
        ' the group "Accounting".  
'        .Users.Delete "Pat Smith"  
'        .Groups.Delete "Accounting"  
  
    End With  
  
    'Clean up  
    Set cat.ActiveConnection = Nothing  
    Set cat = Nothing  
    Set usrNew = Nothing  
    Exit Sub  
  
GroupXError:  
  
    Set cat = Nothing  
    Set usrNew = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
' EndGroupVB  
```  
  
## <a name="see-also"></a>另請參閱  
 [將方法附加至 ADOX 群組 () ](./append-method-adox-groups.md)   
 [ (ADOX 使用者的 Append 方法) ](./append-method-adox-users.md)   
 [ (ADOX) 的目錄物件 ](./catalog-object-adox.md)   
 [ChangePassword 方法 (ADOX) ](./changepassword-method-adox.md)   
 [群組物件 (ADOX) ](./group-object-adox.md)   
 [群組集合 (ADOX) ](./groups-collection-adox.md)   
 [使用者物件 (ADOX) ](./user-object-adox.md)   
 [Users 集合 (ADOX)](./users-collection-adox.md)