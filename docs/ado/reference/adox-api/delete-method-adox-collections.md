---
title: Delete 方法 (ADOX Collections) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Views::Delete
- Groups::Delete
- Indexes::raw_Delete
- Columns::raw_Delete
- Tables::Delete
- Keys::Delete
- Users::Delete
- Users::raw_Delete
- Keys::raw_Delete
- Procedures::raw_Delete
- Views::raw_Delete
- Indexes::Delete
- Procedures::Delete
- Groups::raw_Delete
- Tables::raw_Delete
- Columns::Delete
helpviewer_keywords:
- delete method [ADOX]
ms.assetid: e6b6e3a4-8952-4d79-81f4-51019c338374
author: MightyPen
ms.author: genemi
ms.openlocfilehash: be2aa91cf27d7dc12d3cd0c1e0bf719bd43797ab
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67966439"
---
# <a name="delete-method-adox-collections"></a>Delete 方法 (ADOX Collections)
從集合移除的物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
Collection.Delete Name  
```  
  
#### <a name="parameters"></a>參數  
 *名稱*  
 A **Variant**指定之名稱或序數位置 （索引），要刪除的物件。  
  
## <a name="remarks"></a>備註  
 如果發生錯誤，將*名稱*不存在於集合中。  
  
 針對[資料表](../../../ado/reference/adox-api/tables-collection-adox.md)並[使用者](../../../ado/reference/adox-api/users-collection-adox.md)集合，會發生錯誤，如果提供者不支援刪除的資料表或使用者，分別。 針對[程序](../../../ado/reference/adox-api/procedures-collection-adox.md)並[檢視](../../../ado/reference/adox-api/views-collection-adox.md)集合**刪除**如果提供者不支援保存的命令將會失敗。  
  
## <a name="applies-to"></a>適用於  
  
||||  
|-|-|-|  
|[Columns 集合 (ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md)|[Groups 集合 (ADOX)](../../../ado/reference/adox-api/groups-collection-adox.md)|[Indexes 集合 (ADOX)](../../../ado/reference/adox-api/indexes-collection-adox.md)|  
|[Keys 集合 (ADOX)](../../../ado/reference/adox-api/keys-collection-adox.md)|[Procedures 集合 (ADOX)](../../../ado/reference/adox-api/procedures-collection-adox.md)|[Tables 集合 (ADOX)](../../../ado/reference/adox-api/tables-collection-adox.md)|  
|[Users 集合 (ADOX)](../../../ado/reference/adox-api/users-collection-adox.md)|[Views 集合 (ADOX)](../../../ado/reference/adox-api/views-collection-adox.md)||  
  
## <a name="see-also"></a>另請參閱  
 [Procedures Delete 方法範例 (VB)](../../../ado/reference/adox-api/procedures-delete-method-example-vb.md)   
 [Views Delete 方法範例 (VB)](../../../ado/reference/adox-api/views-delete-method-example-vb.md)
