---
title: 使用者物件 (ADOX) |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 3acdea5ae284b2e9a0ac9c28fe8430a11de8fbd4
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63281583"
---
# <a name="user-object-adox"></a>User 物件 (ADOX)
代表可受保護的資料庫內的存取權限的使用者帳戶。  
  
## <a name="remarks"></a>備註  
 [使用者](../../../ado/reference/adox-api/users-collection-adox.md)的集合[目錄](../../../ado/reference/adox-api/catalog-object-adox.md)代表所有目錄使用者。 **使用者**收集[群組](../../../ado/reference/adox-api/group-object-adox.md)代表特定群組的使用者。  
  
 使用屬性、 集合和方法**使用者**物件時，您可以：  
  
-   識別與使用者[名稱](../../../ado/reference/adox-api/name-property-adox.md)屬性。  
  
-   變更使用者的密碼[ChangePassword](../../../ado/reference/adox-api/changepassword-method-adox.md)方法。  
  
-   判斷是否可將具有讀取、 寫入或刪除權限[GetPermissions](../../../ado/reference/adox-api/getpermissions-method-adox.md)並[SetPermissions](../../../ado/reference/adox-api/setpermissions-method-adox.md)方法。  
  
-   存取與使用者所屬群組[群組](../../../ado/reference/adox-api/groups-collection-adox.md)集合。  
  
-   存取提供者特有的屬性，與[屬性](../../../ado/reference/ado-api/properties-collection-ado.md)集合。  
  
-   判斷[ParentCatalog](../../../ado/reference/adox-api/parentcatalog-property-adox.md)使用者。  
  
 本章節包含下列主題。  
  
-   [User 物件屬性、方法和事件](../../../ado/reference/adox-api/user-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [GetPermissions 和 SetPermissions 方法範例 (VB)](../../../ado/reference/adox-api/getpermissions-and-setpermissions-methods-example-vb.md)   
 [群組集合 (ADOX)](../../../ado/reference/adox-api/groups-collection-adox.md)   
 [Users 集合 (ADOX)](../../../ado/reference/adox-api/users-collection-adox.md)
