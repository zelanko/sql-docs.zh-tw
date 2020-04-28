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
ms.openlocfilehash: 04c7b1d1cb5d07a300b82d13a7e80158498bbd5f
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "67965659"
---
# <a name="objecttypeenum"></a>ObjectTypeEnum
指定要設定其許可權或擁有權的資料庫物件類型。  
  
|持續性|值|描述|  
|--------------|-----------|-----------------|  
|**adPermObjColumn**|2|物件是資料行。|  
|**adPermObjDatabase**|3|物件是資料庫。|  
|**adPermObjProcedure**|4|物件是一個程式。|  
|**adPermObjProviderSpecific**|-1|物件是提供者所定義的類型。 如果*ObjectType*參數為**adPermObjProviderSpecific** ，且未提供*ObjectTypeId* ，就會發生錯誤。|  
|**adPermObjTable**|1|物件是資料表。|  
|**adPermObjView**|5|物件是一個視圖。|  
  
## <a name="applies-to"></a>套用至  
  
|||  
|-|-|  
|[GetObjectOwner 方法 (ADOX)](../../../ado/reference/adox-api/getobjectowner-method-adox.md)|[GetPermissions 方法 (ADOX)](../../../ado/reference/adox-api/getpermissions-method-adox.md)|  
|[SetObjectOwner 方法](../../../ado/reference/adox-api/setobjectowner-method.md)|[SetPermissions 方法 (ADOX)](../../../ado/reference/adox-api/setpermissions-method-adox.md)|
