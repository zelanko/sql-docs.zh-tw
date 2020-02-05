---
title: SMO 和 DMO XPs 伺服器組態選項 | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: bcd945ba-5d81-4124-9a2b-d87491c2a369
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: a0c867d9acba6542d90f72595fa0f71ab6d62e64
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2020
ms.locfileid: "68026047"
---
# <a name="smo-and-dmo-xps-server-configuration-option"></a>SMO 和 DMO XPs 伺服器組態選項
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  使用 SMO 和 DMO XP 選項可啟用此伺服器上的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Object (SMO) 擴充預存程序。  
  
 請注意，從 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]開始，已經從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中移除 DMO。  
  
 下表說明可用的值：  
  
|值|意義|  
|-----------|-------------|  
|0|無法使用 SMO XP。|  
|1|可使用 SMO XP。 這是預設值。|  
  
 設定會立即生效。  
  
## <a name="examples"></a>範例  
 下列範例會啟用 SMO 擴充預存程序。  
  
```  
sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE;  
GO  
sp_configure 'SMO and DMO XPs', 1;  
GO  
RECONFIGURE  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server 管理物件 &#40;SMO&#41; 程式設計指南](../../relational-databases/server-management-objects-smo/sql-server-management-objects-smo-programming-guide.md)  
  
  
