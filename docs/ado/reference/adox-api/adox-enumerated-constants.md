---
description: ADOX 列舉常數
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
ms.openlocfilehash: 553924a51845c7ac49bfb76bab27f75c7d4e4742
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88771607"
---
# <a name="adox-enumerated-constants"></a>ADOX 列舉常數
為了協助進行偵錯工具，ADOX 列舉常數會列出每個常數的值。 不過，此值純粹是諮詢，而且可能會從某個 ADOX 版本變更為另一個。 您的程式碼應該只取決於列舉常數的名稱，而不是實際值。  
  
 已定義下列列舉常數。  
  
|列舉型別|描述|  
|-----------------|-----------------|  
|[ActionEnum](./actionenum.md)|指定呼叫 **SetPermissions** 時要執行的動作類型。|  
|[AllowNullsEnum](./allownullsenum.md)|指定是否為具有 null 值的記錄編制索引。|  
|[ColumnAttributesEnum](./columnattributesenum.md)|指定資料 **行**的特性。|  
|[DataTypeEnum](../ado-api/datatypeenum.md)|指定 **欄位**、 **參數**或 **屬性**的資料類型。|  
|[InheritTypeEnum](./inherittypeenum.md)|指定物件如何繼承使用 **SetPermissions**所設定的許可權。|  
|[KeyTypeEnum](./keytypeenum.md)|指定索引 **鍵**的類型： primary、foreign 或 unique。|  
|[ObjectTypeEnum](./objecttypeenum.md)|指定要設定許可權或擁有權的資料庫物件類型。|  
|[RightsEnum](./rightsenum.md)|指定物件之群組或使用者的許可權或許可權。|  
|[RuleEnum](./ruleenum.md)|指定刪除 **金鑰** 時要遵循的規則。|  
|[SortOrderEnum](./sortorderenum.md)|指定索引資料行的排序次序。|  
  
## <a name="see-also"></a>另請參閱  
 [ADOX API 參考](./adox-object-model.md?view=sql-server-ver15)   
 [資料定義語言和安全性的 ADO 延伸模組 (ADOX)](../../guide/extensions/ado-extensions-for-data-definition-language-and-security-adox.md)