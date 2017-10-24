---
title: "群組和使用者附加、 ChangePassword 方法範例 (VB) |Microsoft 文件"
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
- ChangePassword method [ADOX], Visual Basic example
- Append method [ADOX], Visual Basic example
ms.assetid: c9426757-9cdd-4a95-b506-d3d011569109
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 79fb5b6efc94187fb0da48a532a150216a18c5ca
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="groups-and-users-append-changepassword-methods-example-vb"></a>群組和使用者附加、 ChangePassword 方法範例 (VB)
這個範例會示範[附加](../../../ado/reference/adox-api/append-method-adox-groups.md)方法[群組](../../../ado/reference/adox-api/groups-collection-adox.md)，並將[附加](../../../ado/reference/adox-api/append-method-adox-users.md)方法[使用者](../../../ado/reference/adox-api/users-collection-adox.md)藉由新增新[群組](../../../ado/reference/adox-api/group-object-adox.md)和新[使用者](../../../ado/reference/adox-api/user-object-adox.md)系統。 新**群組**附加至**群組**的新集合**使用者**。 因此，新**使用者**加入至**群組**。 此外， [ChangePassword](../../../ado/reference/adox-api/changepassword-method-adox.md)方法用來指定**使用者**密碼。  
  
> [!NOTE]
>  如果您要連接至資料來源提供者支援 Windows 驗證，您應該指定**Trusted_Connection = yes**或**Integrated Security = SSPI**而不是使用者識別碼和密碼連接字串中的資訊。  
  
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
 [Append 方法 （ADOX 群組）](../../../ado/reference/adox-api/append-method-adox-groups.md)   
 [Append 方法 （ADOX 使用者）](../../../ado/reference/adox-api/append-method-adox-users.md)   
 [目錄物件 (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md)   
 [ChangePassword 方法 (ADOX)](../../../ado/reference/adox-api/changepassword-method-adox.md)   
 [群組物件 (ADOX)](../../../ado/reference/adox-api/group-object-adox.md)   
 [群組集合 (ADOX)](../../../ado/reference/adox-api/groups-collection-adox.md)   
 [使用者物件 (ADOX)](../../../ado/reference/adox-api/user-object-adox.md)   
 [使用者集合 (ADOX)](../../../ado/reference/adox-api/users-collection-adox.md)

