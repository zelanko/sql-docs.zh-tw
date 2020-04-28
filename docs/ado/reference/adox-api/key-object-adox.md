---
title: Key 物件（ADOX） |Microsoft Docs
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
ms.openlocfilehash: f7e405cfdde86a4f19590a87035ff574e1d255c9
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "67965901"
---
# <a name="key-object-adox"></a>Key 物件 (ADOX)
表示資料庫資料表中的主要、外或唯一索引鍵欄位。  
  
## <a name="remarks"></a>備註  
 下列程式碼會建立新的**金鑰**：  
  
```  
Dim obj As New Key  
```  
  
 使用索引**鍵**物件的屬性和集合，您可以：  
  
-   使用[Name](../../../ado/reference/adox-api/name-property-adox.md)屬性來識別索引鍵。  
  
-   使用[Type](../../../ado/reference/adox-api/type-property-key-adox.md)屬性判斷索引鍵為 primary、foreign 或 unique。  
  
-   使用資料[行](../../../ado/reference/adox-api/columns-collection-adox.md)集合來存取索引鍵的資料庫資料行。  
  
-   使用[RelatedTable](../../../ado/reference/adox-api/relatedtable-property-adox.md)屬性指定相關資料表的名稱。  
  
-   使用[DeleteRule](../../../ado/reference/adox-api/deleterule-property-adox.md)和[UpdateRule](../../../ado/reference/adox-api/updaterule-property-adox.md)屬性，判斷刪除或更新主鍵時所執行的動作。  
  
 本章節包含下列主題。  
  
-   [Key 物件屬性、方法和事件](../../../ado/reference/adox-api/key-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [Keys Append 方法、Key Type、RelatedColumn、RelatedTable 和 UpdateRule 屬性範例（VB）](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [Columns 集合（ADOX）](../../../ado/reference/adox-api/columns-collection-adox.md)   
 [Keys 集合 (ADOX)](../../../ado/reference/adox-api/keys-collection-adox.md)
