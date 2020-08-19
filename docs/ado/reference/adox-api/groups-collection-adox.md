---
description: Groups 集合 (ADOX)
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 70c32ba5e4726aca7d6ad8b37c7df082d25b94b0
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88439990"
---
# <a name="groups-collection-adox"></a>Groups 集合 (ADOX)
包含目錄或使用者的所有儲存的 [群組](../../../ado/reference/adox-api/group-object-adox.md) 物件。  
  
## <a name="remarks"></a>備註  
 [目錄](../../../ado/reference/adox-api/catalog-object-adox.md)的**Groups**集合代表所有目錄的群組帳戶。 [使用者](../../../ado/reference/adox-api/user-object-adox.md)的**群組**集合只代表使用者所屬的群組。  
  
 **群組**集合的[APPEND](../../../ado/reference/adox-api/append-method-adox-groups.md)方法對於 ADOX 而言是唯一的。 您可以：  
  
-   使用 **Append** 方法將新的安全性群組新增至集合。  
  
 其餘的屬性和方法是 ADO 集合的標準。 您可以：  
  
-   使用 [Item](../../../ado/reference/ado-api/item-property-ado.md) 屬性存取集合中的群組。  
  
-   傳回集合中包含 [Count](../../../ado/reference/ado-api/count-property-ado.md) 屬性的群組數目。  
  
-   使用 [Delete](../../../ado/reference/adox-api/delete-method-adox-collections.md) 方法，從集合中移除群組。  
  
-   使用 [Refresh](../../../ado/reference/ado-api/refresh-method-ado.md) 方法更新集合中的物件，以反映目前的資料庫架構。  
  
> [!NOTE]
>  將**群組**物件附加至**使用者**物件的**群組**集合之前，**類別目錄****的群組集合中**必須已經[有同名的](../../../ado/reference/adox-api/name-property-adox.md)**群組**物件。  
  
 本節包含下列主題。  
  
-   [Groups 集合屬性、方法和事件](../../../ado/reference/adox-api/groups-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [ (ADOX) 的目錄物件 ](../../../ado/reference/adox-api/catalog-object-adox.md)   
 [Group 物件 (ADOX)](../../../ado/reference/adox-api/group-object-adox.md)
