---
title: 型別屬性 （資料行） (ADOX) |Microsoft 文件
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
- _Column::Type
- _Column::GetType
- _Column::get_Type
- _Column::put_Type
- _Column::PutType
helpviewer_keywords:
- Type property [ADOX]
ms.assetid: 5c6718b6-f728-478a-8afb-5d17b0a91d1f
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 58343ded9e02a6ba3903e39382aef7061595e1b0
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/18/2018
---
# <a name="type-property-column-adox"></a>型別屬性 （資料行） (ADOX)
指出資料行的資料類型。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回**長**值可以是其中一個， [DataTypeEnum](../../../ado/reference/ado-api/datatypeenum.md)常數。 預設值是**adVarWChar**。  
  
## <a name="remarks"></a>備註  
 這個屬性是讀取/寫入，直到[資料行](../../../ado/reference/adox-api/column-object-adox.md)物件會附加至集合或另一個物件，其後它是唯讀的。  
  
## <a name="applies-to"></a>適用於  
 [Column 物件 (ADOX)](../../../ado/reference/adox-api/column-object-adox.md)  
  
## <a name="see-also"></a>另請參閱  
 [ParentCatalog 屬性範例 (VB)](../../../ado/reference/adox-api/parentcatalog-property-example-vb.md)   
 [型別屬性 (Key) (ADOX)](../../../ado/reference/adox-api/type-property-key-adox.md)   
 [Type 屬性 (Table) (ADOX)](../../../ado/reference/adox-api/type-property-table-adox.md)
