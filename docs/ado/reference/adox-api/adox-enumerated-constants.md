---
title: ADOX 列舉常數 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- enumerated constants [ADOX]
ms.assetid: 9d91f511-d46f-44ef-97ef-77bf93836186
author: rothja
ms.author: jroth
ms.openlocfilehash: 84a03af49152bc305f62aceb149d904ef0acf9a0
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82764139"
---
# <a name="adox-enumerated-constants"></a>ADOX 列舉常數
為協助進行偵錯工具，ADOX 列舉常數會列出每個常數的值。 不過，此值純粹是諮詢，而且可能會從一個 ADOX 版本變更為另一個。 您的程式碼應該只取決於列舉常數的名稱，而不是實際的值。  
  
 已定義下列列舉常數。  
  
|列舉型別|描述|  
|-----------------|-----------------|  
|[ActionEnum](../../../ado/reference/adox-api/actionenum.md)|指定呼叫**SetPermissions**時所要執行的動作類型。|  
|[AllowNullsEnum](../../../ado/reference/adox-api/allownullsenum.md)|指定是否要為具有 null 值的記錄編制索引。|  
|[ColumnAttributesEnum](../../../ado/reference/adox-api/columnattributesenum.md)|指定資料**行**的特性。|  
|[DataTypeEnum](../../../ado/reference/ado-api/datatypeenum.md)|指定**欄位**、**參數**或**屬性**的資料類型。|  
|[InheritTypeEnum](../../../ado/reference/adox-api/inherittypeenum.md)|指定物件如何繼承使用**SetPermissions**所設定的許可權。|  
|[KeyTypeEnum](../../../ado/reference/adox-api/keytypeenum.md)|指定索引**鍵**的類型： [主要]、[外部] 或 [唯一]。|  
|[ObjectTypeEnum](../../../ado/reference/adox-api/objecttypeenum.md)|指定要設定其許可權或擁有權的資料庫物件類型。|  
|[RightsEnum](../../../ado/reference/adox-api/rightsenum.md)|指定物件上群組或使用者的許可權。|  
|[RuleEnum](../../../ado/reference/adox-api/ruleenum.md)|指定刪除**金鑰**時要遵循的規則。|  
|[SortOrderEnum](../../../ado/reference/adox-api/sortorderenum.md)|指定索引資料行的排序次序。|  
  
## <a name="see-also"></a>另請參閱  
 [ADOX API 參考](../../../ado/reference/adox-api/adox-api-reference.md)   
 [資料定義語言和安全性的 ADO 延伸模組 (ADOX)](../../../ado/guide/extensions/ado-extensions-for-data-definition-language-and-security-adox.md)
