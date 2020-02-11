---
title: Delete 方法（ADOX 集合） |Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67966439"
---
# <a name="delete-method-adox-collections"></a>Delete 方法 (ADOX Collections)
從集合中移除物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
Collection.Delete Name  
```  
  
#### <a name="parameters"></a>參數  
 *名稱*  
 **Variant** ，指定要刪除之物件的名稱或序數位置（索引）。  
  
## <a name="remarks"></a>備註  
 如果該*名稱*不存在於集合中，就會發生錯誤。  
  
 對於[資料表](../../../ado/reference/adox-api/tables-collection-adox.md)和[使用者](../../../ado/reference/adox-api/users-collection-adox.md)集合，如果提供者不支援分別刪除資料表或使用者，就會發生錯誤。 針對[程式](../../../ado/reference/adox-api/procedures-collection-adox.md)和[Views](../../../ado/reference/adox-api/views-collection-adox.md)集合，如果提供者不支援持續性命令，**刪除**將會失敗。  
  
## <a name="applies-to"></a>套用至  
  
||||  
|-|-|-|  
|[Columns 集合 (ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md)|[Groups 集合 (ADOX)](../../../ado/reference/adox-api/groups-collection-adox.md)|[Indexes 集合 (ADOX)](../../../ado/reference/adox-api/indexes-collection-adox.md)|  
|[Keys 集合 (ADOX)](../../../ado/reference/adox-api/keys-collection-adox.md)|[Procedures 集合 (ADOX)](../../../ado/reference/adox-api/procedures-collection-adox.md)|[Tables 集合 (ADOX)](../../../ado/reference/adox-api/tables-collection-adox.md)|  
|[Users 集合 (ADOX)](../../../ado/reference/adox-api/users-collection-adox.md)|[Views 集合 (ADOX)](../../../ado/reference/adox-api/views-collection-adox.md)||  
  
## <a name="see-also"></a>另請參閱  
 [程式 Delete 方法範例（VB）](../../../ado/reference/adox-api/procedures-delete-method-example-vb.md)   
 [Views Delete 方法範例 (VB)](../../../ado/reference/adox-api/views-delete-method-example-vb.md)
