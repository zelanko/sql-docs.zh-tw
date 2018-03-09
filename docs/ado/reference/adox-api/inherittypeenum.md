---
title: InheritTypeEnum | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- InheritTypeEnum
helpviewer_keywords:
- InheritTypeEnum enumeration [ADOX]
ms.assetid: c2f6ce79-c4b3-4d40-ac95-21025208f991
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: de2281f5badafc7c2140347ab96dfb7251f98ed2
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/09/2018
---
# <a name="inherittypeenum"></a>InheritTypeEnum
指定如何物件都會繼承的權限集與[SetPermissions](../../../ado/reference/adox-api/setpermissions-method-adox.md)。  
  
|常數|Value|Description|  
|--------------|-----------|-----------------|  
|**adInheritBoth**|3|物件和其他容器，包含主要物件所繼承的項目。|  
|**adInheritContainers**|2|主要物件所含的其他容器繼承項目。|  
|**adInheritNone**|0|預設值。 沒有繼承關係，就會發生。|  
|**adInheritNoPropagate**|4|**AdInheritObjects**和**adInheritContainers**旗標不會傳播至繼承的項目。|  
|**adInheritObjects**|1|容器中的非容器物件繼承的權限。|  
  
## <a name="applies-to"></a>適用於  
 [SetPermissions 方法 (ADOX)](../../../ado/reference/adox-api/setpermissions-method-adox.md)
