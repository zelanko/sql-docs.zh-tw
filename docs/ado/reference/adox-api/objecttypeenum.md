---
title: ObjectTypeEnum | Microsoft Docs
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
- ObjectTypeEnum
helpviewer_keywords:
- ObjectTypeEnum enumeration [ADOX]
ms.assetid: 3fdecfca-aa91-4596-ad98-610f1b7f840b
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 10be1fc92c24a074080879fdbcb4ff50892f3840
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/18/2018
---
# <a name="objecttypeenum"></a>ObjectTypeEnum
指定要設定權限或擁有權的資料庫物件的類型。  
  
|常數|Value|Description|  
|--------------|-----------|-----------------|  
|**adPermObjColumn**|2|物件是資料行。|  
|**adPermObjDatabase**|3|此物件為資料庫。|  
|**adPermObjProcedure**|4|此物件為程序。|  
|**adPermObjProviderSpecific**|-1|此物件為提供者所定義的型別。 如果發生錯誤，將*ObjectType*參數是**adPermObjProviderSpecific**和*ObjectTypeId*未提供。|  
|**adPermObjTable**|1|物件是資料表。|  
|**adPermObjView**|5|物件是檢視。|  
  
## <a name="applies-to"></a>適用於  
  
|||  
|-|-|  
|[GetObjectOwner 方法 (ADOX)](../../../ado/reference/adox-api/getobjectowner-method-adox.md)|[GetPermissions 方法 (ADOX)](../../../ado/reference/adox-api/getpermissions-method-adox.md)|  
|[SetObjectOwner 方法](../../../ado/reference/adox-api/setobjectowner-method.md)|[SetPermissions 方法 (ADOX)](../../../ado/reference/adox-api/setpermissions-method-adox.md)|
