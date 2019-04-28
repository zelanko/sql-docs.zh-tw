---
title: ObjectTypeEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ObjectTypeEnum
helpviewer_keywords:
- ObjectTypeEnum enumeration [ADOX]
ms.assetid: 3fdecfca-aa91-4596-ad98-610f1b7f840b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ed7273b2fd24690956fa5c5ffe317ad9c00c40ee
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62710274"
---
# <a name="objecttypeenum"></a>ObjectTypeEnum
指定要設定權限或擁有權的資料庫物件的類型。  
  
|常數|值|描述|  
|--------------|-----------|-----------------|  
|**adPermObjColumn**|2|物件是資料行。|  
|**adPermObjDatabase**|3|此物件為 database。|  
|**adPermObjProcedure**|4|此物件為程序。|  
|**adPermObjProviderSpecific**|-1|此物件為提供者所定義的型別。 如果發生錯誤，將*ObjectType*參數是**adPermObjProviderSpecific**並*ObjectTypeId*未提供。|  
|**adPermObjTable**|1|物件是資料表。|  
|**adPermObjView**|5|物件是檢視。|  
  
## <a name="applies-to"></a>適用於  
  
|||  
|-|-|  
|[GetObjectOwner 方法 (ADOX)](../../../ado/reference/adox-api/getobjectowner-method-adox.md)|[GetPermissions 方法 (ADOX)](../../../ado/reference/adox-api/getpermissions-method-adox.md)|  
|[SetObjectOwner 方法](../../../ado/reference/adox-api/setobjectowner-method.md)|[SetPermissions 方法 (ADOX)](../../../ado/reference/adox-api/setpermissions-method-adox.md)|
