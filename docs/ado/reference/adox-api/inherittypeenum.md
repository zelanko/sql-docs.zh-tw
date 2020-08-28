---
description: InheritTypeEnum
title: InheritTypeEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- InheritTypeEnum
helpviewer_keywords:
- InheritTypeEnum enumeration [ADOX]
ms.assetid: c2f6ce79-c4b3-4d40-ac95-21025208f991
author: rothja
ms.author: jroth
ms.openlocfilehash: 37c6eba57eb7efb05d2b718e294e33b9616cac77
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88984099"
---
# <a name="inherittypeenum"></a>InheritTypeEnum
指定物件如何繼承使用 [SetPermissions](./setpermissions-method-adox.md)所設定的許可權。  
  
|持續性|值|描述|  
|--------------|-----------|-----------------|  
|**adInheritBoth**|3|主要物件所包含的物件和其他容器都會繼承專案。|  
|**adInheritContainers**|2|主要物件所包含的其他容器會繼承該專案。|  
|**adInheritNone**|0|預設值。 不會發生任何繼承。|  
|**adInheritNoPropagate**|4|**AdInheritObjects**和**adInheritContainers**旗標不會傳播至繼承的專案。|  
|**adInheritObjects**|1|容器中的非容器物件會繼承許可權。|  
  
## <a name="applies-to"></a>套用至  
 [SetPermissions 方法 (ADOX)](./setpermissions-method-adox.md)