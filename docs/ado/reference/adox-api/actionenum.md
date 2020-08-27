---
description: ActionEnum
title: ActionEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ActionEnum
helpviewer_keywords:
- ActionEnum enumeration [ADOX]
ms.assetid: f948febd-c885-4621-823b-421e116fec4e
author: rothja
ms.author: jroth
ms.openlocfilehash: 02422de45f3e0ec28901678528468dc72f021549
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88985919"
---
# <a name="actionenum"></a>ActionEnum
指定呼叫 [SetPermissions](./setpermissions-method-adox.md) 時要執行的動作類型。  
  
|持續性|值|描述|  
|--------------|-----------|-----------------|  
|**adAccessDeny**|3|群組或使用者將被拒絕指定的許可權。|  
|**adAccessGrant**|1|群組或使用者至少會有所要求的許可權。|  
|**adAccessRevoke**|4|將會撤銷群組或使用者的任何明確存取權。|  
|**adAccessSet**|2|群組或使用者將完全擁有所要求的許可權。|