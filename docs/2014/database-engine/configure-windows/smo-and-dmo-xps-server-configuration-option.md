---
title: SMO 和 DMO XPs 伺服器組態選項 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: bcd945ba-5d81-4124-9a2b-d87491c2a369
caps.latest.revision: 14
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: fe06dd6034c8ada7c5b702655304fc245bb9d8b1
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36133764"
---
# <a name="smo-and-dmo-xps-server-configuration-option"></a>SMO 和 DMO XPs 伺服器組態選項
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
  
  