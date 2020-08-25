---
description: InheritTypeEnum
title: InheritTypeEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
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
ms.openlocfilehash: d1fed614d90bbf53fdb2198e3ddd657a1e44acd1
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88770117"
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