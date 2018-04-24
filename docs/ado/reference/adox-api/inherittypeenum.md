---
title: InheritTypeEnum |Microsoft 文件
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
- InheritTypeEnum
helpviewer_keywords:
- InheritTypeEnum enumeration [ADOX]
ms.assetid: c2f6ce79-c4b3-4d40-ac95-21025208f991
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e4be349722f849c0a5f059236b4a1d689cf18494
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/18/2018
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
