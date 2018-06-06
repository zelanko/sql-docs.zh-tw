---
title: ADOX 列舉常數 |Microsoft 文件
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- enumerated constants [ADOX]
ms.assetid: 9d91f511-d46f-44ef-97ef-77bf93836186
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0ba95b08ddaa4a75a8243f6830b0f9ce9637d819
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="adox-enumerated-constants"></a>ADOX 列舉常數
若要協助偵錯，ADOX 列舉常數會列出每個常數的值。 不過，這個值是單純諮詢，，而且可能會從一個版本 ADOX 變更到另一個。 您的程式碼應該僅相依於名稱，而不是實際值、 列舉常數。  
  
 會定義下列的列舉的常數。  
  
|列舉型別|Description|  
|-----------------|-----------------|  
|[ActionEnum](../../../ado/reference/adox-api/actionenum.md)|指定當執行動作的類型**SetPermissions**呼叫。|  
|[AllowNullsEnum](../../../ado/reference/adox-api/allownullsenum.md)|指定具有 null 值的記錄都編製索引。|  
|[ColumnAttributesEnum](../../../ado/reference/adox-api/columnattributesenum.md)|指定的特性**資料行**。|  
|[DataTypeEnum](../../../ado/reference/ado-api/datatypeenum.md)|指定的資料型別**欄位**，**參數**，或**屬性**。|  
|[InheritTypeEnum](../../../ado/reference/adox-api/inherittypeenum.md)|指定如何物件都會繼承的權限集與**SetPermissions**。|  
|[KeyTypeEnum](../../../ado/reference/adox-api/keytypeenum.md)|指定的型別**金鑰**： 主要、 外部索引鍵，或唯一。|  
|[ObjectTypeEnum](../../../ado/reference/adox-api/objecttypeenum.md)|指定要設定權限或擁有權的資料庫物件的類型。|  
|[RightsEnum](../../../ado/reference/adox-api/rightsenum.md)|在物件上指定的權限或群組或使用者權限。|  
|[RuleEnum](../../../ado/reference/adox-api/ruleenum.md)|指定的規則時遵循**金鑰**被刪除。|  
|[SortOrderEnum](../../../ado/reference/adox-api/sortorderenum.md)|指定索引的資料行的排序順序。|  
  
## <a name="see-also"></a>另請參閱  
 [ADOX API 參考](../../../ado/reference/adox-api/adox-api-reference.md)   
 [資料定義語言和安全性的 ADO 延伸模組 (ADOX)](../../../ado/guide/extensions/ado-extensions-for-data-definition-language-and-security-adox.md)
