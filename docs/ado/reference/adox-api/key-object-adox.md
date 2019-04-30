---
title: 索引鍵物件 (ADOX) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Key
helpviewer_keywords:
- Key object [ADOX]
ms.assetid: 55f116fe-4d56-4892-bffe-0cdd6fc727c9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7365b3ac33f215840a112089523f23e88697a433
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63213431"
---
# <a name="key-object-adox"></a>Key 物件 (ADOX)
表示從資料庫資料表的主要、 外部索引鍵，或唯一索引鍵欄位。  
  
## <a name="remarks"></a>備註  
 下列程式碼會建立新**金鑰**:  
  
```  
Dim obj As New Key  
```  
  
 使用屬性和集合**金鑰**物件時，您可以：  
  
-   識別具有的索引鍵[名稱](../../../ado/reference/adox-api/name-property-adox.md)屬性。  
  
-   判斷索引鍵是否為主要、 外部索引鍵，或使用唯一[型別](../../../ado/reference/adox-api/type-property-key-adox.md)屬性。  
  
-   存取資料庫資料行的金鑰[資料行](../../../ado/reference/adox-api/columns-collection-adox.md)集合。  
  
-   指定與相關聯的資料表名稱[RelatedTable](../../../ado/reference/adox-api/relatedtable-property-adox.md)屬性。  
  
-   判斷在刪除或更新具有主索引鍵上執行的動作[DeleteRule](../../../ado/reference/adox-api/deleterule-property-adox.md)並[UpdateRule](../../../ado/reference/adox-api/updaterule-property-adox.md)屬性。  
  
 本章節包含下列主題。  
  
-   [Key 物件屬性、方法和事件](../../../ado/reference/adox-api/key-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [Keys Append 方法、 索引鍵的型別、 RelatedColumn、 RelatedTable 和 UpdateRule 屬性範例 (VB)](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [資料行集合 (ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md)   
 [Keys 集合 (ADOX)](../../../ado/reference/adox-api/keys-collection-adox.md)
