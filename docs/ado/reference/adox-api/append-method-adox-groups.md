---
title: Append 方法（ADOX Groups） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Groups::raw_Append
- Groups::Append
helpviewer_keywords:
- Append method [ADOX]
ms.assetid: 56b94fc6-7ef0-4e4a-82a3-033b94c46036
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8281b8b480289dca2b4976cea61a6d6838fa2779
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "67967313"
---
# <a name="append-method-adox-groups"></a>Append 方法 (ADOX Groups)
將新的[群組](../../../ado/reference/adox-api/group-object-adox.md)物件加入至[群組](../../../ado/reference/adox-api/groups-collection-adox.md)集合。  
  
## <a name="syntax"></a>語法  
  
```  
  
Groups.Append Group  
```  
  
#### <a name="parameters"></a>參數  
 *群組*  
 要附加的**群組**物件，或要建立和附加的組名。  
  
## <a name="remarks"></a>備註  
 [目錄](../../../ado/reference/adox-api/catalog-object-adox.md)的**Groups**集合代表所有目錄的群組帳戶。 [使用者](../../../ado/reference/adox-api/user-object-adox.md)的**Groups**集合只代表使用者所屬的群組。  
  
 如果提供者不支援建立群組，則會發生錯誤。  
  
> [!NOTE]
>  將**群組**物件附加至**使用者**物件的**groups**集合之前，與要附加的**群組物件**[名稱](../../../ado/reference/adox-api/name-property-adox.md)相同，必須已經存在於**目錄**的**群組**集合中。  
  
## <a name="applies-to"></a>套用至  
 [Groups 集合 (ADOX)](../../../ado/reference/adox-api/groups-collection-adox.md)  
  
## <a name="see-also"></a>另請參閱  
 [Groups 和 Users Append、ChangePassword 方法範例（VB）](../../../ado/reference/adox-api/groups-and-users-append-changepassword-methods-example-vb.md)   
 [Append 方法（ADOX Columns）](../../../ado/reference/adox-api/append-method-adox-columns.md)   
 [Append 方法（ADOX 索引）](../../../ado/reference/adox-api/append-method-adox-indexes.md)   
 [Append 方法（ADOX Keys）](../../../ado/reference/adox-api/append-method-adox-keys.md)   
 [Append 方法（ADOX 程式）](../../../ado/reference/adox-api/append-method-adox-procedures.md)   
 [Append 方法（ADOX Tables）](../../../ado/reference/adox-api/append-method-adox-tables.md)   
 [Append 方法（ADOX Users）](../../../ado/reference/adox-api/append-method-adox-users.md)   
 [Append 方法 (ADOX Views)](../../../ado/reference/adox-api/append-method-adox-views.md)
