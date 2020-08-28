---
description: Users 集合 (ADOX)
title: 使用者集合 (ADOX) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: a1f511e637696e5b14905bcccba50cb13737d6e7
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88983029"
---
# <a name="users-collection-adox"></a>Users 集合 (ADOX)
包含[目錄](./catalog-object-adox.md)或[群組](./group-object-adox.md)的所有儲存的[使用者](./user-object-adox.md)物件。  
  
## <a name="remarks"></a>備註  
 [目錄](./catalog-object-adox.md)的**users**集合代表所有目錄的使用者。 [群組](./group-object-adox.md)的**users**集合只代表具有特定群組成員資格的使用者。  
  
 **使用者**集合的[APPEND](./append-method-adox-users.md)方法對於 ADOX 而言是唯一的。 您可以：  
  
-   使用 **Append** 方法將新的使用者加入至集合。  
  
 其餘的屬性和方法是 ADO 集合的標準。 您可以：  
  
-   使用 [Item](../ado-api/item-property-ado.md) 屬性存取集合中的使用者。  
  
-   傳回集合中包含 [Count](../ado-api/count-property-ado.md) 屬性的使用者數目。  
  
-   使用 [Delete](./delete-method-adox-collections.md) 方法將使用者從集合中移除。  
  
-   使用 [Refresh](../ado-api/refresh-method-ado.md) 方法更新集合中的物件，以反映目前資料庫的架構。  
  
> [!NOTE]
>  將**使用者**物件附加至**群組**物件的**Users**集合之前，**類別目錄**的**users**集合中必須已經有一個**使用者**物件與要附加之名稱相同的[名稱](./name-property-adox.md)。  
  
 本節包含下列主題。  
  
-   [Users 集合屬性、方法和事件](./users-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [GetPermissions 和 SetPermissions 方法範例 (VB) ](./getpermissions-and-setpermissions-methods-example-vb.md)   
 [ (ADOX) 的目錄物件 ](./catalog-object-adox.md)   
 [User 物件 (ADOX)](./user-object-adox.md)