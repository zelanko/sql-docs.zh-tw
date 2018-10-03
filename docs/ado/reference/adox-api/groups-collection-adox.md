---
title: 群組集合 (ADOX) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Groups
- User::Groups
- Catalog::Groups
helpviewer_keywords:
- Groups collection [ADOX]
ms.assetid: 09aa7b0a-69d5-4564-80a7-20ad8189670f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e6b8aea077af67c882830220da9ce24b802e25e5
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47801428"
---
# <a name="groups-collection-adox"></a>Groups 集合 (ADOX)
包含所有預存[群組](../../../ado/reference/adox-api/group-object-adox.md)目錄或使用者的物件。  
  
## <a name="remarks"></a>備註  
 **群組**的集合[目錄](../../../ado/reference/adox-api/catalog-object-adox.md)代表所有類別目錄的群組帳戶。 **群組**收集[使用者](../../../ado/reference/adox-api/user-object-adox.md)表示只將使用者所屬的群組。  
  
 [Append](../../../ado/reference/adox-api/append-method-adox-groups.md)方法**群組**集合都是唯一的 ADOX。 您可以：  
  
-   將新的安全性群組新增至集合**Append**方法。  
  
 其餘的屬性和方法是標準的 ADO 集合。 您可以：  
  
-   存取集合中的群組[項目](../../../ado/reference/ado-api/item-property-ado.md)屬性。  
  
-   傳回與集合中包含的群組數目[計數](../../../ado/reference/ado-api/count-property-ado.md)屬性。  
  
-   從集合中移除群組[刪除](../../../ado/reference/adox-api/delete-method-adox-collections.md)方法。  
  
-   更新以反映與目前的資料庫結構描述集合中的物件[重新整理](../../../ado/reference/ado-api/refresh-method-ado.md)方法。  
  
> [!NOTE]
>  附加之前**群組**物件**群組**集合**使用者**物件**群組**物件具有相同[名稱](../../../ado/reference/adox-api/name-property-adox.md)為要附加的一個必須已存在於**群組**的集合**目錄**。  
  
 本章節包含下列主題。  
  
-   [Groups 集合屬性、方法和事件](../../../ado/reference/adox-api/groups-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [Catalog 物件 (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md)   
 [Group 物件 (ADOX)](../../../ado/reference/adox-api/group-object-adox.md)
