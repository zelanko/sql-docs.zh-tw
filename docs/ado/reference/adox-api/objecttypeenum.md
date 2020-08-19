---
description: ObjectTypeEnum
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 22b2c36ab87079c7bc984606a36397a98ea67af7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88439750"
---
# <a name="objecttypeenum"></a>ObjectTypeEnum
指定要設定許可權或擁有權的資料庫物件類型。  
  
|常數|值|描述|  
|--------------|-----------|-----------------|  
|**adPermObjColumn**|2|物件是資料行。|  
|**adPermObjDatabase**|3|物件是資料庫。|  
|**adPermObjProcedure**|4|物件是程式。|  
|**adPermObjProviderSpecific**|-1|物件是提供者所定義的類型。 如果 *ObjectType* 參數是 **adPermObjProviderSpecific** ，而且未提供 *ObjectTypeId* ，就會發生錯誤。|  
|**adPermObjTable**|1|物件是資料表。|  
|**adPermObjView**|5|物件是一個視圖。|  
  
## <a name="applies-to"></a>套用至  

:::row:::
    :::column:::
        [GetObjectOwner 方法 (ADOX)](../../../ado/reference/adox-api/getobjectowner-method-adox.md)  
        [GetPermissions 方法 (ADOX)](../../../ado/reference/adox-api/getpermissions-method-adox.md)  
    :::column-end:::
    :::column:::
        [SetObjectOwner 方法](../../../ado/reference/adox-api/setobjectowner-method.md)  
        [SetPermissions 方法 (ADOX)](../../../ado/reference/adox-api/setpermissions-method-adox.md)  
    :::column-end:::
:::row-end:::
