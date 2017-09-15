---
title: "群組集合 (ADOX) |Microsoft 文件"
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
- Groups
- User::Groups
- Catalog::Groups
helpviewer_keywords:
- Groups collection [ADOX]
ms.assetid: 09aa7b0a-69d5-4564-80a7-20ad8189670f
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 3dfb8a9e2f75fb11caf64b06e34016474d7b9fa7
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="groups-collection-adox"></a>群組集合 (ADOX)
包含所有儲存[群組](../../../ado/reference/adox-api/group-object-adox.md)目錄或使用者的物件。  
  
## <a name="remarks"></a>備註  
 **群組**集合[目錄](../../../ado/reference/adox-api/catalog-object-adox.md)代表所有類別目錄的群組帳戶。 **群組**集合[使用者](../../../ado/reference/adox-api/user-object-adox.md)代表只有使用者所隸屬的群組。  
  
 [附加](../../../ado/reference/adox-api/append-method-adox-groups.md)方法**群組**集合都是唯一的 ADOX。 您可以：  
  
-   將新的安全性群組新增至集合，**附加**方法。  
  
 是標準，以 ADO 集合其餘的屬性和方法。 您可以：  
  
-   存取集合中具有群組[項目](../../../ado/reference/ado-api/item-property-ado.md)屬性。  
  
-   傳回與集合中包含的群組數目[計數](../../../ado/reference/ado-api/count-property-ado.md)屬性。  
  
-   從集合中移除群組[刪除](../../../ado/reference/adox-api/delete-method-adox-collections.md)方法。  
  
-   更新以反映目前的資料庫結構描述與集合中的物件[重新整理](../../../ado/reference/ado-api/refresh-method-ado.md)方法。  
  
> [!NOTE]
>  附加之前**群組**物件**群組**集合**使用者**物件**群組**物件具有相同[名稱](../../../ado/reference/adox-api/name-property-adox.md)為附加至其中一個必須已存在於**群組**集合**目錄**。  
  
 本章節包含下列主題。  
  
-   [群組集合的屬性、 方法和事件](../../../ado/reference/adox-api/groups-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [目錄物件 (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md)   
 [群組物件 (ADOX)](../../../ado/reference/adox-api/group-object-adox.md)
