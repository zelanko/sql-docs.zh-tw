---
title: Delete 方法 （ADOX 集合） |Microsoft 文件
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
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
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: fae857efe446eeea07db56481f0e1b5a5998fde6
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/18/2018
---
# <a name="delete-method-adox-collections"></a>Delete 方法 （ADOX 集合）
從集合中移除物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
Collection.Delete Name  
```  
  
#### <a name="parameters"></a>參數  
 *名稱*  
 A **Variant**指定之名稱或要刪除之物件的序數位置 （索引）。  
  
## <a name="remarks"></a>備註  
 如果發生錯誤，將*名稱*不存在於集合中。  
  
 如[資料表](../../../ado/reference/adox-api/tables-collection-adox.md)和[使用者](../../../ado/reference/adox-api/users-collection-adox.md)集合，會發生錯誤，如果提供者不支援刪除的資料表或使用者，分別。 如[程序](../../../ado/reference/adox-api/procedures-collection-adox.md)和[檢視](../../../ado/reference/adox-api/views-collection-adox.md)集合**刪除**如果提供者不支援持續性命令將會失敗。  
  
## <a name="applies-to"></a>適用於  
  
||||  
|-|-|-|  
|[Columns 集合 (ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md)|[Groups 集合 (ADOX)](../../../ado/reference/adox-api/groups-collection-adox.md)|[Indexes 集合 (ADOX)](../../../ado/reference/adox-api/indexes-collection-adox.md)|  
|[Keys 集合 (ADOX)](../../../ado/reference/adox-api/keys-collection-adox.md)|[Procedures 集合 (ADOX)](../../../ado/reference/adox-api/procedures-collection-adox.md)|[Tables 集合 (ADOX)](../../../ado/reference/adox-api/tables-collection-adox.md)|  
|[Users 集合 (ADOX)](../../../ado/reference/adox-api/users-collection-adox.md)|[Views 集合 (ADOX)](../../../ado/reference/adox-api/views-collection-adox.md)||  
  
## <a name="see-also"></a>另請參閱  
 [程序刪除方法的範例 (VB)](../../../ado/reference/adox-api/procedures-delete-method-example-vb.md)   
 [Views Delete 方法範例 (VB)](../../../ado/reference/adox-api/views-delete-method-example-vb.md)
