---
title: Users 集合 (ADOX) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Group::Users
- Users
- Catalog::Users
helpviewer_keywords:
- Users collection [ADOX]
ms.assetid: 0a30fa74-6f10-4410-bd70-882e7c43cd46
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2a6146a942e572e28692ceaafd77d6958cdab9dc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67964956"
---
# <a name="users-collection-adox"></a>Users 集合 (ADOX)
包含所有預存[使用者](../../../ado/reference/adox-api/user-object-adox.md)的物件[類別目錄](../../../ado/reference/adox-api/catalog-object-adox.md)或是[群組](../../../ado/reference/adox-api/group-object-adox.md)。  
  
## <a name="remarks"></a>備註  
 **使用者**的集合[目錄](../../../ado/reference/adox-api/catalog-object-adox.md)代表所有目錄使用者。 **使用者**收集[群組](../../../ado/reference/adox-api/group-object-adox.md)代表具有特定群組中的成員資格的使用者。  
  
 [Append](../../../ado/reference/adox-api/append-method-adox-users.md)方法**使用者**集合都是唯一的 ADOX。 您可以：  
  
-   新的使用者加入至集合，使用**Append**方法。  
  
 其餘的屬性和方法是標準的 ADO 集合。 您可以：  
  
-   存取集合中具有使用者[項目](../../../ado/reference/ado-api/item-property-ado.md)屬性。  
  
-   傳回與集合中包含的人數[計數](../../../ado/reference/ado-api/count-property-ado.md)屬性。  
  
-   從集合中移除使用者[刪除](../../../ado/reference/adox-api/delete-method-adox-collections.md)方法。  
  
-   更新以反映目前的資料庫結構描述集合中的物件[重新整理](../../../ado/reference/ado-api/refresh-method-ado.md)方法。  
  
> [!NOTE]
>  附加之前**使用者**物件**使用者**集合**群組**物件**使用者**物件具有相同[名稱](../../../ado/reference/adox-api/name-property-adox.md)為要附加的一個必須已存在於**使用者**的集合**目錄**。  
  
 本章節包含下列主題。  
  
-   [Users 集合屬性、方法和事件](../../../ado/reference/adox-api/users-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [GetPermissions 和 SetPermissions 方法範例 (VB)](../../../ado/reference/adox-api/getpermissions-and-setpermissions-methods-example-vb.md)   
 [Catalog 物件 (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md)   
 [User 物件 (ADOX)](../../../ado/reference/adox-api/user-object-adox.md)
