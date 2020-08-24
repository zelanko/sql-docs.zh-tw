---
description: Group 物件 (ADOX)
title: 群組物件 (ADOX) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Group
helpviewer_keywords:
- group object [ADOX]
ms.assetid: 55ef0ade-68ea-4da5-8aa5-4cd27d1f6d1e
author: rothja
ms.author: jroth
ms.openlocfilehash: 0442ca3bd785269fed49dc86d982971a8feec4ea
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88770417"
---
# <a name="group-object-adox"></a>Group 物件 (ADOX)
代表在安全資料庫中具有存取權限的群組帳戶。  
  
## <a name="remarks"></a>備註  
 [目錄](./catalog-object-adox.md)的[Groups](./groups-collection-adox.md)集合代表所有目錄的群組帳戶。 [使用者](./user-object-adox.md)的**群組**集合只代表使用者所屬的群組。  
  
 使用 **群組** 物件的屬性、集合和方法，您可以：  
  
-   使用 [Name](./name-property-adox.md) 屬性來識別群組。  
  
-   判斷群組是否具有 [GetPermissions](./getpermissions-method-adox.md) 和 [SetPermissions](./setpermissions-method-adox.md) 方法的讀取、寫入或刪除許可權。  
  
-   存取群組中具有 [使用者](./users-collection-adox.md) 集合之成員資格的使用者帳戶。  
  
-   存取具有 [屬性](../ado-api/properties-collection-ado.md) 集合的提供者特定屬性。  
  
 本節包含下列主題。  
  
-   [Group 物件屬性、方法和事件](./group-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [群組集合 (ADOX) ](./groups-collection-adox.md)   
 [Users 集合 (ADOX)](./users-collection-adox.md)