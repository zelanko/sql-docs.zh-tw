---
title: 啟用通用條件合規性設定 | Microsoft Docs
description: 了解通用準則合規性選項在 SQL Server 中啟用的準則，以及如何符合通用準則評估保證層級 4+。
ms.custom: ''
ms.date: 08/21/2018
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- common criteria compliance
helpviewer_keywords:
- CC (common criteria) [Database Engine]
- common criteria compliance [Database Engine]
- Risidual Information Protection [Database Engine]
- RIP (Residual Information Protection)
ms.assetid: 61766eea-c450-408d-af33-fbe7ef8c9ff2
author: rothja
ms.author: jroth
ms.openlocfilehash: 2a33ce838ce32c6a7d2b883c5b256f668c213745
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85659815"
---
# <a name="common-criteria-compliance-enabled-server-configuration"></a>啟用通用條件合規性伺服器設定
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

通用條件合規性選項會啟用 [Common Criteria for Information Technology Security Evaluation](https://www.commoncriteriaportal.org/) (資訊技術安全性評估通用條件) 所需的下列項目。  
  
|準則|描述|  
|--------------|-----------------|  
|剩餘資訊保護 (RIP)|在記憶體重新配置到新的資源之前，RIP 需要使用已知的位元模式來覆寫記憶體配置。 符合 RIP 標準可促使安全性改善。不過，覆寫記憶體配置可能會降低效能。 啟用 common criteria compliance enabled 選項之後，就會進行覆寫。|  
|檢視登入統計資料的功能|啟用 common criteria compliance enabled 選項之後，就會啟用登入稽核。 每次使用者成功登入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]時，就會提供一些資訊，包括上次登入成功的時間、上次登入不成功的時間，以及上次登入成功與目前登入時間之間的登入嘗試次數。 您可以透過查詢 [sys.dm_exec_sessions](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md) 動態管理檢視，檢視這些登入統計資料。|  
|資料行 `GRANT` 不應該覆寫資料表 `DENY`|啟用 common criteria compliance enabled 選項之後，資料表層級 `DENY` 的優先順序會高於資料行層級 `GRANT`。 如果未啟用此選項，資料行層級 `GRANT` 的優先順序會高於資料表層級 `DENY`。|  
  
 [通用條件符合已啟用] 選項是一個進階選項。 Common Criteria 只會針對 Enterprise Edition 和 Datacenter Edition 進行評估和認證。 如需有關 Common Criteria 認證的最新狀態，請參閱 [Microsoft SQL Server Common Criteria](https://go.microsoft.com/fwlink/?LinkId=616319) 網站。  
  
> [!IMPORTANT]  
>  除了啟用 common criteria compliance enabled 選項之外，您也必須下載並執行可將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 設定為符合通用條件評估保證層級 4 (EAL4+) 的指令碼。 您可以從 [Microsoft SQL Server Common Criteria](https://go.microsoft.com/fwlink/?LinkId=616319) 網站下載此指令碼。  
  
 如果您要使用 `sp_configure` 系統預存程序來變更此設定，只有當 [顯示進階選項] 設為 1 時，才能變更 [通用條件符合已啟用]。 伺服器重新啟動之後，設定才會生效。 可能的值為 0 和 1：  
  
-   0 表示通用條件符合未啟用。 這是預設值。  
  
-   1 表示通用條件符合已啟用。  
  
## <a name="examples"></a>範例  
 下列範例會啟用通用條件符合。  
  
```  
sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE;  
GO  
sp_configure 'common criteria compliance enabled', 1;  
GO  
RECONFIGURE WITH OVERRIDE; 
GO  
```  

重新啟動 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]。
  
## <a name="see-also"></a>另請參閱  
 [伺服器組態選項 &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)
