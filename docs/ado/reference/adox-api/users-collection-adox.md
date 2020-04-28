---
title: Users 集合（ADOX） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Group::Users
- Users
- Catalog::Users
helpviewer_keywords:
- Users collection [ADOX]
ms.assetid: 0a30fa74-6f10-4410-bd70-882e7c43cd46
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2a6146a942e572e28692ceaafd77d6958cdab9dc
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "67964956"
---
# <a name="users-collection-adox"></a>Users 集合 (ADOX)
包含[目錄](../../../ado/reference/adox-api/catalog-object-adox.md)或[群組](../../../ado/reference/adox-api/group-object-adox.md)的所有預存[使用者](../../../ado/reference/adox-api/user-object-adox.md)物件。  
  
## <a name="remarks"></a>備註  
 [目錄](../../../ado/reference/adox-api/catalog-object-adox.md)的**users**集合代表所有目錄的使用者。 [群組](../../../ado/reference/adox-api/group-object-adox.md)的**users**集合只代表擁有特定群組成員資格的使用者。  
  
 **使用者**集合的[APPEND](../../../ado/reference/adox-api/append-method-adox-users.md)方法對於 ADOX 而言是唯一的。 您可以：  
  
-   使用**Append**方法，將新的使用者新增至集合。  
  
 其餘的屬性和方法都是 ADO 集合的標準。 您可以：  
  
-   使用[Item](../../../ado/reference/ado-api/item-property-ado.md)屬性存取集合中的使用者。  
  
-   使用[Count](../../../ado/reference/ado-api/count-property-ado.md)屬性傳回包含在集合中的使用者數目。  
  
-   使用[Delete](../../../ado/reference/adox-api/delete-method-adox-collections.md)方法從集合中移除使用者。  
  
-   更新集合中的物件，以使用[Refresh](../../../ado/reference/ado-api/refresh-method-ado.md)方法來反映目前資料庫的架構。  
  
> [!NOTE]
>  將**使用者**物件附加至**群組**物件的**users**集合之前，與要附加的**使用者物件**[名稱](../../../ado/reference/adox-api/name-property-adox.md)必須已經存在於**目錄**的**使用者**集合中。  
  
 本章節包含下列主題。  
  
-   [Users 集合屬性、方法和事件](../../../ado/reference/adox-api/users-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [GetPermissions 和 SetPermissions 方法範例（VB）](../../../ado/reference/adox-api/getpermissions-and-setpermissions-methods-example-vb.md)   
 [Catalog 物件（ADOX）](../../../ado/reference/adox-api/catalog-object-adox.md)   
 [User 物件 (ADOX)](../../../ado/reference/adox-api/user-object-adox.md)
