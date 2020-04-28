---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: aef8f768dd991e4e6ed740cc56600a6f1a8020e0
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "67965958"
---
# <a name="inherittypeenum"></a>InheritTypeEnum
指定物件如何繼承使用[SetPermissions](../../../ado/reference/adox-api/setpermissions-method-adox.md)所設定的許可權。  
  
|持續性|值|描述|  
|--------------|-----------|-----------------|  
|**adInheritBoth**|3|主要物件所包含的物件和其他容器都會繼承此專案。|  
|**adInheritContainers**|2|主要物件所包含的其他容器會繼承此專案。|  
|**adInheritNone**|0|預設值。 不會發生任何繼承。|  
|**adInheritNoPropagate**|4|**AdInheritObjects**和**adInheritContainers**旗標不會傳播至繼承的專案。|  
|**adInheritObjects**|1|容器中的非容器物件會繼承許可權。|  
  
## <a name="applies-to"></a>套用至  
 [SetPermissions 方法 (ADOX)](../../../ado/reference/adox-api/setpermissions-method-adox.md)
