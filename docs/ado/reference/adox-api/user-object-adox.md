---
description: User 物件 (ADOX)
title: " (ADOX) 的使用者物件 |Microsoft Docs"
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- User
helpviewer_keywords:
- User object [ADOX]
ms.assetid: f68e32ce-ef7c-407d-bdb5-d280947ae0e2
author: rothja
ms.author: jroth
ms.openlocfilehash: 6e83bd40c226f1d5b5948c6475b259c799907866
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88983048"
---
# <a name="user-object-adox"></a>User 物件 (ADOX)
代表在安全資料庫中具有存取權限的使用者帳戶。  
  
## <a name="remarks"></a>備註  
 [目錄](./catalog-object-adox.md)的[users](./users-collection-adox.md)集合代表所有目錄的使用者。 [群組](./group-object-adox.md)的**users**集合只代表特定群組的使用者。  
  
 使用 **使用者** 物件的屬性、集合和方法時，您可以：  
  
-   使用 [Name](./name-property-adox.md) 屬性來識別使用者。  
  
-   使用 [ChangePassword](./changepassword-method-adox.md) 方法變更使用者的密碼。  
  
-   判斷使用者是否具有 [GetPermissions](./getpermissions-method-adox.md) 和 [SetPermissions](./setpermissions-method-adox.md) 方法的讀取、寫入或刪除許可權。  
  
-   存取使用者所屬[群組集合的群組。](./groups-collection-adox.md)  
  
-   存取具有 [屬性](../ado-api/properties-collection-ado.md) 集合的提供者特定屬性。  
  
-   判斷使用者的 [ParentCatalog](./parentcatalog-property-adox.md) 。  
  
 本節包含下列主題。  
  
-   [User 物件屬性、方法和事件](./user-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [GetPermissions 和 SetPermissions 方法範例 (VB) ](./getpermissions-and-setpermissions-methods-example-vb.md)   
 [群組集合 (ADOX) ](./groups-collection-adox.md)   
 [Users 集合 (ADOX)](./users-collection-adox.md)