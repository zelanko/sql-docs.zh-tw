---
description: RuleEnum
title: RuleEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: 66367d872e27629f1bf437961b99908d0c42e9f2
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88983369"
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