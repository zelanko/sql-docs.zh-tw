---
title: 開啟 CLR 整合微軟文件
description: 託管 CLR 的 Microsoft SQL 伺服器稱為 CLR 整合,預設情況下禁用該整合。 使用sp_configure儲存過程啟用 CLR 整合。
ms.custom: ''
ms.date: 09/17/2019
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
ms.openlocfilehash: 7d161135c8c8b0c7d7932eb08aa98509efc4bc45
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2020
ms.locfileid: "81488101"
---
# <a name="clr-integration---enabling"></a>CLR 整合 - 啟用
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  預設會停用 Common Language Runtime (CLR) 整合功能，且為了使用 CLR 整合所實作的物件，必須啟用這個功能。 要啟用 CLR 整合,請使用 sp_configure[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]**儲存過程**的**clr 啟用**選項,  
  
```sql  
EXEC sp_configure 'clr enabled', 1;  
RECONFIGURE;  
GO  
```  
  
 通過將**啟用 clr**的選項設置為 0,可以禁用 CLR 整合。 禁用 CLR[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]整合時 ,請停止執行所有使用者定義的 CLR 例程式並卸載所有應用程式域。 依賴於 CLR 的功能(如**層次結構數據類型**、`FORMAT`功能、複製和基於策略的管理)不受此設置的影響,並將繼續運行。
  
> [!NOTE]  
>  要啟用 CLR 整合,您必須具有 ALTER SETTINGS 伺服器等級許可權,該許可權由**系統管理員**和**伺服器管理員**固定伺服器角色的成員隱式持有。  
  
> [!NOTE]  
>  啟動伺服器時，以大量記憶體及大量處理器設定的電腦可能無法載入 SQL Server 的 CLR 整合功能。 要解決此問題,請使用 **-gmemory_to_reserve**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]服務啟動選項啟動伺服器,並指定足夠大的記憶體值。 如需詳細資訊，請參閱 [Database Engine Service Startup Options](../../database-engine/configure-windows/database-engine-service-startup-options.md)。  
  
> [!NOTE]  
>  輕量型共用不支援 Common Language Runtime (CLR) 的執行。 在啟用 CLR 整合以前，您必須停用輕量型共用。 如需詳細資訊，請參閱 [輕量型共用伺服器組態選項](../../database-engine/configure-windows/lightweight-pooling-server-configuration-option.md)。  
  
## <a name="see-also"></a>另請參閱  
 [sp_configure&#40;交易-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [開啟 clr 伺服器設定選項](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md)   
 [重新設定&#40;轉瞬端-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [伺服器級角色](../../relational-databases/security/authentication-access/server-level-roles.md)  
  
  
