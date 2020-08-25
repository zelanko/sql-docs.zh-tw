---
description: ActionEnum
title: ActionEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
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
ms.openlocfilehash: 2c9032dfdb3394e582541f60afce7b930751a5c0
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88777777"
---
# <a name="actionenum"></a>ActionEnum
指定呼叫 [SetPermissions](./setpermissions-method-adox.md) 時要執行的動作類型。  
  
|持續性|值|描述|  
|--------------|-----------|-----------------|  
|**adAccessDeny**|3|群組或使用者將被拒絕指定的許可權。|  
|**adAccessGrant**|1|群組或使用者至少會有所要求的許可權。|  
|**adAccessRevoke**|4|將會撤銷群組或使用者的任何明確存取權。|  
|**adAccessSet**|2|群組或使用者將完全擁有所要求的許可權。|