---
title: SMO 和 DMO XPs 伺服器組態選項 | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: configure-windows
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: bcd945ba-5d81-4124-9a2b-d87491c2a369
caps.latest.revision: 15
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6922050ae1ff3451c6484319fced5973a416a460
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="smo-and-dmo-xps-server-configuration-option"></a>SMO 和 DMO XPs 伺服器組態選項
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  使用 SMO 和 DMO XP 選項可啟用此伺服器上的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Object (SMO) 擴充預存程序。  
  
 請注意，從 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]開始，已經從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中移除 DMO。  
  
 下表說明可用的值：  
  
|ReplTest1|意義|  
|-----------|-------------|  
|0|無法使用 SMO XP。|  
|@shouldalert|可使用 SMO XP。 這是預設值。|  
  
 這項設定會立即生效。  
  
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
  
  
