---
description: RuleEnum
title: RuleEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- RuleEnum
helpviewer_keywords:
- RuleEnum enumeration [ADOX]
ms.assetid: 738fd3ff-3daf-483d-a0b9-88bef1be54c1
author: rothja
ms.author: jroth
ms.openlocfilehash: da49bbacf8ba59ba12f59fb072e9b5ec8c2ec2ea
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88769457"
---
# <a name="ruleenum"></a>RuleEnum
指定刪除 [金鑰](./key-object-adox.md) 時要遵循的規則。  
  
|持續性|值|描述|  
|--------------|-----------|-----------------|  
|**adRICascade**|1|串聯變更。|  
|**adRINone**|0|預設值。 不採取任何動作。|  
|**adRISetDefault**|3|外鍵值設定為預設值。|  
|**adRISetNull**|2|外鍵值設定為 null。|  
  
## <a name="applies-to"></a>套用至  
 [DeleteRule 屬性 (ADOX)](./deleterule-property-adox.md)