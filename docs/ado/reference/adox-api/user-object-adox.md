---
title: User 物件（ADOX） |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: cf454e28e7a823eb643b5bbd92b0396fac15a028
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67964970"
---
# <a name="user-object-adox"></a>User 物件 (ADOX)
代表在受保護資料庫中具有存取權限的使用者帳戶。  
  
## <a name="remarks"></a>備註  
 [目錄](../../../ado/reference/adox-api/catalog-object-adox.md)的[users](../../../ado/reference/adox-api/users-collection-adox.md)集合代表所有目錄的使用者。 [群組](../../../ado/reference/adox-api/group-object-adox.md)的**users**集合只代表特定群組的使用者。  
  
 透過**使用者**物件的屬性、集合和方法，您可以：  
  
-   使用[Name](../../../ado/reference/adox-api/name-property-adox.md)屬性來識別使用者。  
  
-   使用[ChangePassword](../../../ado/reference/adox-api/changepassword-method-adox.md)方法來變更使用者的密碼。  
  
-   使用[GetPermissions](../../../ado/reference/adox-api/getpermissions-method-adox.md)和[SetPermissions](../../../ado/reference/adox-api/setpermissions-method-adox.md)方法，判斷使用者是否具有讀取、寫入或刪除許可權。  
  
-   存取使用者所屬[群組集合的群組。](../../../ado/reference/adox-api/groups-collection-adox.md)  
  
-   使用[properties](../../../ado/reference/ado-api/properties-collection-ado.md)集合存取提供者特定的屬性。  
  
-   判斷使用者的[ParentCatalog](../../../ado/reference/adox-api/parentcatalog-property-adox.md) 。  
  
 本章節包含下列主題。  
  
-   [User 物件屬性、方法和事件](../../../ado/reference/adox-api/user-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [GetPermissions 和 SetPermissions 方法範例（VB）](../../../ado/reference/adox-api/getpermissions-and-setpermissions-methods-example-vb.md)   
 [Groups 集合（ADOX）](../../../ado/reference/adox-api/groups-collection-adox.md)   
 [Users 集合 (ADOX)](../../../ado/reference/adox-api/users-collection-adox.md)
