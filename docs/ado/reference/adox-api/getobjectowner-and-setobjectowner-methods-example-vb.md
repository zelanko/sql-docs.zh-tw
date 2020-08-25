---
description: GetObjectOwner 和 SetObjectOwner 方法範例 (VB)
title: GetObjectOwner 和 SetObjectOwner 方法範例 (VB) |Microsoft Docs
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
- SetObjectOwner method [ADOX], Visual Basic example
- GetObjectOwner method [ADOX], Visual Basic example
ms.assetid: e44ec3d4-42ae-447d-aaed-bdea53cb0cca
author: rothja
ms.author: jroth
ms.openlocfilehash: dc9a111b3315c7737229ec0240e5ee4ed6e406b9
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88770547"
---
# <a name="getobjectowner-and-setobjectowner-methods-example-vb"></a>GetObjectOwner 和 SetObjectOwner 方法範例 (VB)
此範例示範 [GetObjectOwner](./getobjectowner-method-adox.md) 和 [SetObjectOwner](./setobjectowner-method.md) 方法。 這段程式碼假設有群群組帳戶處理 (請參閱 [群組和使用者附加、ChangePassword 方法範例 (VB) ](./groups-and-users-append-changepassword-methods-example-vb.md) ，以瞭解如何將此群組新增至系統) 。 Category 資料表的擁有者設定為 Accounting。  
  
```  
' BeginOwnersVB  
Sub OwnersX()  
  
    Dim tblLoop As New ADOX.Table  
    Dim cat As New ADOX.Catalog  
    Dim strOwner As String  
  
    ' Open the Catalog.  
    cat.ActiveConnection = "Provider=Microsoft.Jet.OLEDB.4.0;" & _  
        "Data Source=c:\Program Files\" & _  
        "Microsoft Office\Office\Samples\Northwind.mdb;" & _  
        "jet oledb:system database=" & _  
        "c:\Program Files\Microsoft Office\Office\system.mdw"  
  
    ' Print the original owner of Categories  
    strOwner = cat.GetObjectOwner("Categories", adPermObjTable)  
    Debug.Print "Owner of Categories: " & strOwner  
  
    ' Set the owner of Categories to Accounting  
    cat.SetObjectOwner "Categories", adPermObjTable, "Accounting"  
  
    ' List the owners of all tables and columns in the catalog.  
    For Each tblLoop In cat.Tables  
        Debug.Print "Table: " & tblLoop.Name  
        Debug.Print "   Owner: " & _  
            cat.GetObjectOwner(tblLoop.Name, adPermObjTable)  
    Next tblLoop  
  
    ' Restore the original owner of Categories  
    cat.SetObjectOwner "Categories", adPermObjTable, strOwner  
  
End Sub  
' EndOwnersVB  
```  
  
## <a name="see-also"></a>另請參閱  
 [ (ADOX) 的目錄物件 ](./catalog-object-adox.md)   
 [GetObjectOwner 方法 (ADOX) ](./getobjectowner-method-adox.md)   
 [SetObjectOwner 方法](./setobjectowner-method.md)