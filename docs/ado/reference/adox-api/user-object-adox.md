---
title: "使用者物件 (ADOX) |Microsoft 文件"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- User
helpviewer_keywords:
- User object [ADOX]
ms.assetid: f68e32ce-ef7c-407d-bdb5-d280947ae0e2
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 3565b06fa33ddf0990b89724639d9538da37e9b6
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

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
  
-   [使用者物件屬性、 方法和事件](../../../ado/reference/adox-api/user-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [GetPermissions 和 SetPermissions 方法範例 (VB)](../../../ado/reference/adox-api/getpermissions-and-setpermissions-methods-example-vb.md)   
 [群組集合 (ADOX)](../../../ado/reference/adox-api/groups-collection-adox.md)   
 [使用者集合 (ADOX)](../../../ado/reference/adox-api/users-collection-adox.md)
