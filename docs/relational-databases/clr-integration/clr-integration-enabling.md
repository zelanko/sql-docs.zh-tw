---
title: 啟用 CLR 整合 |Microsoft Docs
ms.custom: ''
ms.date: 08/01/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- clr enabled option
- common language runtime [SQL Server], enabling
ms.assetid: eb3e9c64-7486-42e7-baf6-c956fb311a2c
author: rothja
ms.author: jroth
ms.openlocfilehash: 207723b511f5bf700d65176f4031ee024ec76c17
ms.sourcegitcommit: 734529a6f108e6ee6bfce939d8be562d405e1832
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/02/2019
ms.locfileid: "70212405"
---
# <a name="clr-integration---enabling"></a>CLR 整合 - 啟用
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  預設會停用 Common Language Runtime (CLR) 整合功能，且為了使用 CLR 整合所實作的物件，必須啟用這個功能。 若要啟用 CLR 整合, 請在中[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]使用**sp_configure**預存程式的**CLR enabled**選項:  
  
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
  
 您可以將**clr enabled**選項設定為 0, 以停用 clr 整合。 當您停用 CLR 整合時，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會停止執行所有 CLR 常式，並卸載所有應用程式網域。  
  
> [!NOTE]  
>  若要啟用 CLR 整合, 您必須擁有 ALTER SETTINGS 伺服器層級許可權, 這會由**sysadmin**和**serveradmin**固定伺服器角色的成員隱含持有。  
  
> [!NOTE]  
>  啟動伺服器時，以大量記憶體及大量處理器設定的電腦可能無法載入 SQL Server 的 CLR 整合功能。 若要解決此問題, 請使用 **-gmemory_to_reserve** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]服務啟動選項來啟動伺服器, 並指定夠大的記憶體值。 如需詳細資訊，請參閱 [Database Engine Service Startup Options](../../database-engine/configure-windows/database-engine-service-startup-options.md)。  
  
> [!NOTE]  
>  輕量型共用不支援 Common Language Runtime (CLR) 的執行。 在啟用 CLR 整合以前，您必須停用輕量型共用。 如需詳細資訊，請參閱 [輕量型共用伺服器組態選項](../../database-engine/configure-windows/lightweight-pooling-server-configuration-option.md)。  
  
## <a name="see-also"></a>另請參閱  
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [CLR 已啟用伺服器組態選項](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md)   
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [伺服器層級角色](../../relational-databases/security/authentication-access/server-level-roles.md)  
  
  
