---
title: "Append 方法 （ADOX 群組） |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Groups::raw_Append
- Groups::Append
helpviewer_keywords:
- Append method [ADOX]
ms.assetid: 56b94fc6-7ef0-4e4a-82a3-033b94c46036
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: ed08c3fc0f871c1e7fb8a5885f44390770d4a7a5
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="append-method-adox-groups"></a>Append 方法 （ADOX 群組）
將新[群組](../../../ado/reference/adox-api/group-object-adox.md)物件[群組](../../../ado/reference/adox-api/groups-collection-adox.md)集合。  
  
## <a name="syntax"></a>語法  
  
```  
  
Groups.Append Group  
```  
  
#### <a name="parameters"></a>參數  
 *群組*  
 **群組**来附加物件或建立並附加至群組的名稱。  
  
## <a name="remarks"></a>備註  
 **群組**集合[目錄](../../../ado/reference/adox-api/catalog-object-adox.md)代表所有類別目錄的群組帳戶。 **群組**集合[使用者](../../../ado/reference/adox-api/user-object-adox.md)代表只有使用者所隸屬的群組。  
  
 如果提供者不支援建立群組時，會發生錯誤。  
  
> [!NOTE]
>  附加之前**群組**物件**群組**集合**使用者**物件**群組**物件具有相同[名稱](../../../ado/reference/adox-api/name-property-adox.md)為附加至其中一個必須已存在於**群組**集合**目錄**。  
  
## <a name="applies-to"></a>適用於  
 [群組集合 (ADOX)](../../../ado/reference/adox-api/groups-collection-adox.md)  
  
## <a name="see-also"></a>另請參閱  
 [群組和使用者附加、 ChangePassword 方法範例 (VB)](../../../ado/reference/adox-api/groups-and-users-append-changepassword-methods-example-vb.md)   
 [Append 方法 （ADOX 資料行）](../../../ado/reference/adox-api/append-method-adox-columns.md)   
 [Append 方法 （ADOX 索引）](../../../ado/reference/adox-api/append-method-adox-indexes.md)   
 [Append 方法 （ADOX 索引鍵）](../../../ado/reference/adox-api/append-method-adox-keys.md)   
 [Append 方法 （ADOX 程序）](../../../ado/reference/adox-api/append-method-adox-procedures.md)   
 [Append 方法 （ADOX 資料表）](../../../ado/reference/adox-api/append-method-adox-tables.md)   
 [Append 方法 （ADOX 使用者）](../../../ado/reference/adox-api/append-method-adox-users.md)   
 [Append 方法 （ADOX 檢視）](../../../ado/reference/adox-api/append-method-adox-views.md)

