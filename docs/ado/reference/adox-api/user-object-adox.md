---
title: "使用者物件 (ADOX) |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords: User
helpviewer_keywords: User object [ADOX]
ms.assetid: f68e32ce-ef7c-407d-bdb5-d280947ae0e2
caps.latest.revision: "12"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a34d35adf84e32738733184430160613ef8eca45
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="user-object-adox"></a>使用者物件 (ADOX)
代表有受保護的資料庫內的存取權限的使用者帳戶。  
  
## <a name="remarks"></a>備註  
 [使用者](../../../ado/reference/adox-api/users-collection-adox.md)集合[目錄](../../../ado/reference/adox-api/catalog-object-adox.md)代表所有類別目錄的使用者。 **使用者**集合[群組](../../../ado/reference/adox-api/group-object-adox.md)表示特定群組的使用者。  
  
 包含屬性、 集合，而且方法**使用者**物件，您可以：  
  
-   識別具有使用者[名稱](../../../ado/reference/adox-api/name-property-adox.md)屬性。  
  
-   變更之使用者的密碼[ChangePassword](../../../ado/reference/adox-api/changepassword-method-adox.md)方法。  
  
-   判斷是否在使用者具有讀取、 寫入或刪除權限與[GetPermissions](../../../ado/reference/adox-api/getpermissions-method-adox.md)和[SetPermissions](../../../ado/reference/adox-api/setpermissions-method-adox.md)方法。  
  
-   存取與使用者所屬的群組[群組](../../../ado/reference/adox-api/groups-collection-adox.md)集合。  
  
-   存取提供者特有的屬性，與[屬性](../../../ado/reference/ado-api/properties-collection-ado.md)集合。  
  
-   判斷[ParentCatalog](../../../ado/reference/adox-api/parentcatalog-property-adox.md)使用者。  
  
 本章節包含下列主題。  
  
-   [User 物件屬性、方法和事件](../../../ado/reference/adox-api/user-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>請參閱＜  
 [GetPermissions 和 SetPermissions 方法範例 (VB)](../../../ado/reference/adox-api/getpermissions-and-setpermissions-methods-example-vb.md)   
 [群組集合 (ADOX)](../../../ado/reference/adox-api/groups-collection-adox.md)   
 [Users 集合 (ADOX)](../../../ado/reference/adox-api/users-collection-adox.md)
