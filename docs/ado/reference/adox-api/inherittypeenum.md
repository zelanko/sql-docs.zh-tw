---
title: InheritTypeEnum |Microsoft 文件
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
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
ms.openlocfilehash: b3a167913b23005cf2b78e4acc682ec2af75157c
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/11/2018
ms.locfileid: "35286647"
---
# <a name="inherittypeenum"></a>InheritTypeEnum
指定如何物件都會繼承的權限集與[SetPermissions](../../../ado/reference/adox-api/setpermissions-method-adox.md)。  
  
|常數|ReplTest1|描述|  
|--------------|-----------|-----------------|  
|**adInheritBoth**|3|物件和其他容器，包含主要物件所繼承的項目。|  
|**adInheritContainers**|2|主要物件所含的其他容器繼承項目。|  
|**adInheritNone**|0|預設值。 沒有繼承關係，就會發生。|  
|**adInheritNoPropagate**|4|**AdInheritObjects**和**adInheritContainers**旗標不會傳播至繼承的項目。|  
|**adInheritObjects**|@shouldalert|容器中的非容器物件繼承的權限。|  
  
## <a name="applies-to"></a>適用於  
 [SetPermissions 方法 (ADOX)](../../../ado/reference/adox-api/setpermissions-method-adox.md)
