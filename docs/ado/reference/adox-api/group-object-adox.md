---
title: Group 物件（ADOX） |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b4b3de5f445ddd09bf7d069b0b93d82c6f8de978
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "67966219"
---
# <a name="group-object-adox"></a>Group 物件 (ADOX)
代表在安全資料庫中具有存取權限的群組帳戶。  
  
## <a name="remarks"></a>備註  
 [目錄](../../../ado/reference/adox-api/catalog-object-adox.md)的[Groups](../../../ado/reference/adox-api/groups-collection-adox.md)集合代表所有目錄的群組帳戶。 [使用者](../../../ado/reference/adox-api/user-object-adox.md)的**Groups**集合只代表使用者所屬的群組。  
  
 使用**群組**物件的屬性、集合和方法，您可以：  
  
-   識別具有[Name](../../../ado/reference/adox-api/name-property-adox.md)屬性的群組。  
  
-   使用[GetPermissions](../../../ado/reference/adox-api/getpermissions-method-adox.md)和[SetPermissions](../../../ado/reference/adox-api/setpermissions-method-adox.md)方法，判斷群組是否具有讀取、寫入或刪除許可權。  
  
-   存取具有[使用者](../../../ado/reference/adox-api/users-collection-adox.md)集合之群組成員資格的使用者帳戶。  
  
-   使用[properties](../../../ado/reference/ado-api/properties-collection-ado.md)集合存取提供者特定的屬性。  
  
 本章節包含下列主題。  
  
-   [Group 物件屬性、方法和事件](../../../ado/reference/adox-api/group-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [Groups 集合（ADOX）](../../../ado/reference/adox-api/groups-collection-adox.md)   
 [Users 集合 (ADOX)](../../../ado/reference/adox-api/users-collection-adox.md)
