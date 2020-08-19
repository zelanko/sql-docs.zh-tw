---
description: User 物件 (ADOX)
title: " (ADOX) 的使用者物件 |Microsoft Docs"
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
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
ms.openlocfilehash: 3c81caba440367712e5743bc1e224bd3968a2990
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88439390"
---
# <a name="user-object-adox"></a>User 物件 (ADOX)
代表在安全資料庫中具有存取權限的使用者帳戶。  
  
## <a name="remarks"></a>備註  
 [目錄](../../../ado/reference/adox-api/catalog-object-adox.md)的[users](../../../ado/reference/adox-api/users-collection-adox.md)集合代表所有目錄的使用者。 [群組](../../../ado/reference/adox-api/group-object-adox.md)的**users**集合只代表特定群組的使用者。  
  
 使用 **使用者** 物件的屬性、集合和方法時，您可以：  
  
-   使用 [Name](../../../ado/reference/adox-api/name-property-adox.md) 屬性來識別使用者。  
  
-   使用 [ChangePassword](../../../ado/reference/adox-api/changepassword-method-adox.md) 方法變更使用者的密碼。  
  
-   判斷使用者是否具有 [GetPermissions](../../../ado/reference/adox-api/getpermissions-method-adox.md) 和 [SetPermissions](../../../ado/reference/adox-api/setpermissions-method-adox.md) 方法的讀取、寫入或刪除許可權。  
  
-   存取使用者所屬[群組集合的群組。](../../../ado/reference/adox-api/groups-collection-adox.md)  
  
-   存取具有 [屬性](../../../ado/reference/ado-api/properties-collection-ado.md) 集合的提供者特定屬性。  
  
-   判斷使用者的 [ParentCatalog](../../../ado/reference/adox-api/parentcatalog-property-adox.md) 。  
  
 本節包含下列主題。  
  
-   [User 物件屬性、方法和事件](../../../ado/reference/adox-api/user-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [GetPermissions 和 SetPermissions 方法範例 (VB) ](../../../ado/reference/adox-api/getpermissions-and-setpermissions-methods-example-vb.md)   
 [群組集合 (ADOX) ](../../../ado/reference/adox-api/groups-collection-adox.md)   
 [Users 集合 (ADOX)](../../../ado/reference/adox-api/users-collection-adox.md)
