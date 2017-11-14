---
title: "使用者集合 (ADOX) |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Group::Users
- Users
- Catalog::Users
helpviewer_keywords:
- Users collection [ADOX]
ms.assetid: 0a30fa74-6f10-4410-bd70-882e7c43cd46
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b9c19df96e66927c6dc5092cd0584f071a3d3b40
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="users-collection-adox"></a>使用者集合 (ADOX)
包含所有儲存[使用者](../../../ado/reference/adox-api/user-object-adox.md)物件[目錄](../../../ado/reference/adox-api/catalog-object-adox.md)或[群組](../../../ado/reference/adox-api/group-object-adox.md)。  
  
## <a name="remarks"></a>備註  
 **使用者**集合[目錄](../../../ado/reference/adox-api/catalog-object-adox.md)代表所有類別目錄的使用者。 **使用者**集合[群組](../../../ado/reference/adox-api/group-object-adox.md)代表具有特定群組中的成員資格的使用者。  
  
 [附加](../../../ado/reference/adox-api/append-method-adox-users.md)方法**使用者**集合都是唯一的 ADOX。 您可以：  
  
-   新使用者加入至集合，使用**附加**方法。  
  
 是標準，以 ADO 集合其餘的屬性和方法。 您可以：  
  
-   存取集合中具有使用者[項目](../../../ado/reference/ado-api/item-property-ado.md)屬性。  
  
-   傳回與集合中包含的使用者數目[計數](../../../ado/reference/ado-api/count-property-ado.md)屬性。  
  
-   從集合中移除使用者[刪除](../../../ado/reference/adox-api/delete-method-adox-collections.md)方法。  
  
-   更新以反映目前的資料庫結構描述集合中的物件[重新整理](../../../ado/reference/ado-api/refresh-method-ado.md)方法。  
  
> [!NOTE]
>  附加之前**使用者**物件**使用者**集合**群組**物件**使用者**物件具有相同[名稱](../../../ado/reference/adox-api/name-property-adox.md)為附加至其中一個必須已存在於**使用者**集合**目錄**。  
  
 本章節包含下列主題。  
  
-   [使用者集合的屬性、 方法和事件](../../../ado/reference/adox-api/users-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [GetPermissions 和 SetPermissions 方法範例 (VB)](../../../ado/reference/adox-api/getpermissions-and-setpermissions-methods-example-vb.md)   
 [目錄物件 (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md)   
 [使用者物件 (ADOX)](../../../ado/reference/adox-api/user-object-adox.md)

