---
title: Append 方法 (ADOX Users) |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: e56391357e7a11c47efdf0ffaf3c9ae9704d5db3
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63206237"
---
# <a name="append-method-adox-users"></a>Append 方法 (ADOX Users)
加入新[使用者](../../../ado/reference/adox-api/user-object-adox.md)物件[使用者](../../../ado/reference/adox-api/users-collection-adox.md)集合。  
  
## <a name="syntax"></a>語法  
  
```  
  
Users.Append User[,Password]  
```  
  
#### <a name="parameters"></a>參數  
 *使用者*  
 A **Variant**值，包含**使用者**来附加的物件或建立並附加至使用者的名稱。  
  
 *密碼*  
 選擇性。 A**字串**值，其中包含使用者的密碼。 *密碼*參數會對應至所指定的值[ChangePassword](../../../ado/reference/adox-api/changepassword-method-adox.md)方法**使用者**物件。  
  
## <a name="remarks"></a>備註  
 **使用者**的集合[目錄](../../../ado/reference/adox-api/catalog-object-adox.md)代表所有目錄使用者。 **使用者**收集[群組](../../../ado/reference/adox-api/group-object-adox.md)代表具有特定群組中的成員資格的使用者。  
  
 如果提供者不支援建立使用者，會發生錯誤。  
  
> [!NOTE]
>  附加之前**使用者**物件**使用者**集合**群組**物件**使用者**物件具有相同[名稱](../../../ado/reference/adox-api/name-property-adox.md)為要附加的一個必須已存在於**使用者**的集合**目錄**。  
  
## <a name="applies-to"></a>適用於  
 [Users 集合 (ADOX)](../../../ado/reference/adox-api/users-collection-adox.md)  
  
## <a name="see-also"></a>另請參閱  
 [群組和 Users Append、 ChangePassword 方法範例 (VB)](../../../ado/reference/adox-api/groups-and-users-append-changepassword-methods-example-vb.md)   
 [Append 方法 (ADOX Columns)](../../../ado/reference/adox-api/append-method-adox-columns.md)   
 [Append 方法 (ADOX Groups)](../../../ado/reference/adox-api/append-method-adox-groups.md)   
 [Append 方法 (ADOX Indexes)](../../../ado/reference/adox-api/append-method-adox-indexes.md)   
 [Append 方法 (ADOX Keys)](../../../ado/reference/adox-api/append-method-adox-keys.md)   
 [Append 方法 (ADOX Procedures)](../../../ado/reference/adox-api/append-method-adox-procedures.md)   
 [Append 方法 (ADOX Tables)](../../../ado/reference/adox-api/append-method-adox-tables.md)   
 [Append 方法 (ADOX Views)](../../../ado/reference/adox-api/append-method-adox-views.md)
