---
description: Users 集合 (ADOX)
title: 使用者集合 (ADOX) |Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: e69ecbf642982d6465c12e225f45199a0c1b33e0
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88439370"
---
# <a name="users-collection-adox"></a>Users 集合 (ADOX)
包含[目錄](../../../ado/reference/adox-api/catalog-object-adox.md)或[群組](../../../ado/reference/adox-api/group-object-adox.md)的所有儲存的[使用者](../../../ado/reference/adox-api/user-object-adox.md)物件。  
  
## <a name="remarks"></a>備註  
 [目錄](../../../ado/reference/adox-api/catalog-object-adox.md)的**users**集合代表所有目錄的使用者。 [群組](../../../ado/reference/adox-api/group-object-adox.md)的**users**集合只代表具有特定群組成員資格的使用者。  
  
 **使用者**集合的[APPEND](../../../ado/reference/adox-api/append-method-adox-users.md)方法對於 ADOX 而言是唯一的。 您可以：  
  
-   使用 **Append** 方法將新的使用者加入至集合。  
  
 其餘的屬性和方法是 ADO 集合的標準。 您可以：  
  
-   使用 [Item](../../../ado/reference/ado-api/item-property-ado.md) 屬性存取集合中的使用者。  
  
-   傳回集合中包含 [Count](../../../ado/reference/ado-api/count-property-ado.md) 屬性的使用者數目。  
  
-   使用 [Delete](../../../ado/reference/adox-api/delete-method-adox-collections.md) 方法將使用者從集合中移除。  
  
-   使用 [Refresh](../../../ado/reference/ado-api/refresh-method-ado.md) 方法更新集合中的物件，以反映目前資料庫的架構。  
  
> [!NOTE]
>  將**使用者**物件附加至**群組**物件的**Users**集合之前，**類別目錄**的**users**集合中必須已經有一個**使用者**物件與要附加之名稱相同的[名稱](../../../ado/reference/adox-api/name-property-adox.md)。  
  
 本節包含下列主題。  
  
-   [Users 集合屬性、方法和事件](../../../ado/reference/adox-api/users-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [GetPermissions 和 SetPermissions 方法範例 (VB) ](../../../ado/reference/adox-api/getpermissions-and-setpermissions-methods-example-vb.md)   
 [ (ADOX) 的目錄物件 ](../../../ado/reference/adox-api/catalog-object-adox.md)   
 [User 物件 (ADOX)](../../../ado/reference/adox-api/user-object-adox.md)
