---
description: Type 屬性 (Column) (ADOX)
title: 類型屬性 (資料行)  (ADOX) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
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
author: rothja
ms.author: jroth
ms.openlocfilehash: dffb08de42e3c38a9c0a28e8cad33af95f0d8926
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88983169"
---
# <a name="type-property-column-adox"></a>Type 屬性 (Column) (ADOX)
表示資料行的資料類型。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回可以是其中一個[DataTypeEnum](../ado-api/datatypeenum.md)常數的**Long**值。 預設值為 **adVarWChar**。  
  
## <a name="remarks"></a>備註  
 這個屬性是讀取/寫入，直到將資料 [行](./column-object-adox.md) 物件附加至集合或另一個物件之後，之後才是唯讀的。  
  
## <a name="applies-to"></a>套用至  
 [Column 物件 (ADOX)](./column-object-adox.md)  
  
## <a name="see-also"></a>另請參閱  
 [ (VB) 的 ParentCatalog 屬性範例 ](./parentcatalog-property-example-vb.md)   
 [類型屬性 (索引鍵)  (ADOX) ](./type-property-key-adox.md)   
 [Type 屬性 (Table) (ADOX)](./type-property-table-adox.md)