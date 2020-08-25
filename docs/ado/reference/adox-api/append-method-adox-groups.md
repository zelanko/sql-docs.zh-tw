---
description: Append 方法 (ADOX Groups)
title: 將方法 (ADOX 群組附加) |Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 14900e34ef93f2ad738779b0cf7478372ab59179
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88771477"
---
# <a name="append-method-adox-groups"></a>Append 方法 (ADOX Groups)
將新的 [群組](./group-object-adox.md) 物件加入至 [群組](./groups-collection-adox.md) 集合。  
  
## <a name="syntax"></a>語法  
  
```  
  
Groups.Append Group  
```  
  
#### <a name="parameters"></a>參數  
 *群組*  
 要附加的 **群組** 物件，或是要建立和附加的組名。  
  
## <a name="remarks"></a>備註  
 [目錄](./catalog-object-adox.md)的**Groups**集合代表所有目錄的群組帳戶。 [使用者](./user-object-adox.md)的**群組**集合只代表使用者所屬的群組。  
  
 如果提供者不支援建立群組，就會發生錯誤。  
  
> [!NOTE]
>  將**群組**物件附加至**使用者**物件的**群組**集合之前，**類別目錄****的群組集合中**必須已經[有同名的](./name-property-adox.md)**群組**物件。  
  
## <a name="applies-to"></a>套用至  
 [Groups 集合 (ADOX)](./groups-collection-adox.md)  
  
## <a name="see-also"></a>另請參閱  
 [群組和使用者附加、ChangePassword 方法範例 (VB) ](./groups-and-users-append-changepassword-methods-example-vb.md)   
 [將方法附加至 ADOX 資料行 () ](./append-method-adox-columns.md)   
 [附加方法 (ADOX 索引) ](./append-method-adox-indexes.md)   
 [附加方法 (ADOX 索引鍵) ](./append-method-adox-keys.md)   
 [Append 方法 (ADOX 程式) ](./append-method-adox-procedures.md)   
 [附加方法 (ADOX 資料表) ](./append-method-adox-tables.md)   
 [ (ADOX 使用者的 Append 方法) ](./append-method-adox-users.md)   
 [Append 方法 (ADOX Views)](./append-method-adox-views.md)