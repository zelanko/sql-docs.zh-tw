---
title: "啟用 CLR 整合 |Microsoft 文件"
ms.custom: 
ms.date: 08/01/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: clr
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- clr enabled option
- common language runtime [SQL Server], enabling
ms.assetid: eb3e9c64-7486-42e7-baf6-c956fb311a2c
caps.latest.revision: 
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Active
ms.openlocfilehash: 70cf91f827d9cc181107e28bbe51c01ca0a99440
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/09/2018
---
# <a name="clr-integration---enabling"></a>CLR 整合-啟用
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
預設會停用 Common Language Runtime (CLR) 整合功能，且為了使用 CLR 整合所實作的物件，必須啟用這個功能。 若要啟用 CLR 整合，請使用**clr 已啟用**選項**sp_configure**預存程序中的[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]:  
  
```sql  
  
sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE;  
GO  
sp_configure 'clr enabled', 1;  
GO  
RECONFIGURE;  
GO  
```  
  
 您可以藉由設定停用 CLR 整合**clr 已啟用**選項設為 0。 當您停用 CLR 整合時，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會停止執行所有 CLR 常式，並卸載所有應用程式網域。  
  
> [!NOTE]  
>  若要啟用 CLR 整合，您必須有 ALTER SETTINGS 伺服器層級權限，其中的成員隱含地擁有**sysadmin**和**serveradmin**固定伺服器角色。  
  
> [!NOTE]  
>  啟動伺服器時，以大量記憶體及大量處理器設定的電腦可能無法載入 SQL Server 的 CLR 整合功能。 若要解決此問題，請啟動伺服器使用**-gmemory_to_reserve** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]服務啟動選項，並指定夠大的記憶體值。 如需詳細資訊，請參閱 [Database Engine Service Startup Options](../../database-engine/configure-windows/database-engine-service-startup-options.md)。  
  
> [!NOTE]  
>  輕量型共用不支援 Common Language Runtime (CLR) 的執行。 在啟用 CLR 整合以前，您必須停用輕量型共用。 如需詳細資訊，請參閱 [輕量型共用伺服器組態選項](../../database-engine/configure-windows/lightweight-pooling-server-configuration-option.md)。  
  
## <a name="see-also"></a>另請參閱  
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [clr 已啟用伺服器組態選項](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md)   
 [RECONFIGURE &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [伺服器層級角色](../../relational-databases/security/authentication-access/server-level-roles.md)  
  
  
