---
title: "InheritTypeEnum |Microsoft 文件"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- InheritTypeEnum
helpviewer_keywords:
- InheritTypeEnum enumeration [ADOX]
ms.assetid: c2f6ce79-c4b3-4d40-ac95-21025208f991
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 36570c508955b82ccd403e9af10895edc1584d9f
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="inherittypeenum"></a>InheritTypeEnum
指定如何物件都會繼承的權限集與[SetPermissions](../../../ado/reference/adox-api/setpermissions-method-adox.md)。  
  
|常數|值|Description|  
|--------------|-----------|-----------------|  
|**adInheritBoth**|3|物件和其他容器，包含主要物件所繼承的項目。|  
|**adInheritContainers**|2|主要物件所含的其他容器繼承項目。|  
|**adInheritNone**|0|預設值。 沒有繼承關係，就會發生。|  
|**adInheritNoPropagate**|4|**AdInheritObjects**和**adInheritContainers**旗標不會傳播至繼承的項目。|  
|**adInheritObjects**|1|容器中的非容器物件繼承的權限。|  
  
## <a name="applies-to"></a>適用於  
 [SetPermissions 方法 (ADOX)](../../../ado/reference/adox-api/setpermissions-method-adox.md)

