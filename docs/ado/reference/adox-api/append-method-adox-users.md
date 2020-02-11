---
title: Append 方法（ADOX Users） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Users::raw_Append
- Users::Append
helpviewer_keywords:
- Append method [ADOX]
ms.assetid: b80bc5d5-78ca-4f75-956b-2ac658029cc7
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 99a21cd5dd32af9e84877865cfe7c0fc92f6c087
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67967222"
---
# <a name="append-method-adox-users"></a>Append 方法 (ADOX Users)
將新的[使用者](../../../ado/reference/adox-api/user-object-adox.md)物件加入至[使用者](../../../ado/reference/adox-api/users-collection-adox.md)集合。  
  
## <a name="syntax"></a>語法  
  
```  
  
Users.Append User[,Password]  
```  
  
#### <a name="parameters"></a>參數  
 *使用者*  
 **Variant**值，其中包含要附加的**使用者**物件，或要建立和附加的使用者名稱。  
  
 *密碼*  
 選擇性。 包含使用者密碼的**字串**值。 *Password*參數會對應至**使用者**物件的[ChangePassword](../../../ado/reference/adox-api/changepassword-method-adox.md)方法所指定的值。  
  
## <a name="remarks"></a>備註  
 [目錄](../../../ado/reference/adox-api/catalog-object-adox.md)的**users**集合代表所有目錄的使用者。 [群組](../../../ado/reference/adox-api/group-object-adox.md)的**users**集合只代表擁有特定群組成員資格的使用者。  
  
 如果提供者不支援建立使用者，將會發生錯誤。  
  
> [!NOTE]
>  將**使用者**物件附加至**群組**物件的**users**集合之前，與要附加的**使用者物件**[名稱](../../../ado/reference/adox-api/name-property-adox.md)必須已經存在於**目錄**的**使用者**集合中。  
  
## <a name="applies-to"></a>套用至  
 [Users 集合 (ADOX)](../../../ado/reference/adox-api/users-collection-adox.md)  
  
## <a name="see-also"></a>另請參閱  
 [Groups 和 Users Append、ChangePassword 方法範例（VB）](../../../ado/reference/adox-api/groups-and-users-append-changepassword-methods-example-vb.md)   
 [Append 方法（ADOX Columns）](../../../ado/reference/adox-api/append-method-adox-columns.md)   
 [Append 方法（ADOX Groups）](../../../ado/reference/adox-api/append-method-adox-groups.md)   
 [Append 方法（ADOX 索引）](../../../ado/reference/adox-api/append-method-adox-indexes.md)   
 [Append 方法（ADOX Keys）](../../../ado/reference/adox-api/append-method-adox-keys.md)   
 [Append 方法（ADOX 程式）](../../../ado/reference/adox-api/append-method-adox-procedures.md)   
 [Append 方法（ADOX Tables）](../../../ado/reference/adox-api/append-method-adox-tables.md)   
 [Append 方法 (ADOX Views)](../../../ado/reference/adox-api/append-method-adox-views.md)
