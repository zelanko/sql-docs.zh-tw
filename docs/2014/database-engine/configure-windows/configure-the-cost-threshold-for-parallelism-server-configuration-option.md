---
title: 設定 cost threshold for parallelism 伺服器組態選項 | Microsoft Docs
ms.custom: ''
ms.date: 10/26/2015
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- cost threshold for parallelism option
ms.assetid: dad21bee-fe28-41f6-9d2f-e6ababfaf9db
caps.latest.revision: 28
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 11e27a526265257278d47bcf27cda69529313261
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36030592"
---
# <a name="configure-the-cost-threshold-for-parallelism-server-configuration-option"></a>設定 cost threshold for parallelism 伺服器組態選項
  此主題描述如何使用 **或** ，在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中設定 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] cost threshold for parallelism [!INCLUDE[tsql](../../includes/tsql-md.md)]伺服器組態選項。 **平行處理原則的成本臨界值** 選項指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 為查詢建立及執行平行計劃的臨界值。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 **或**。 成本是指在特定硬體組態下，估計執行序列計畫所需的已耗用時間 (以秒為單位)。 **cost threshold for parallelism** 選項可設成從 0 到 32767 的任何值。 預設值為 5。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
     [建議](#Recommendations)  
  
     [Security](#Security)  
  
-   **使用下列方法設定 cost threshold for parallelism 選項：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **待處理**  [設定 cost threshold for parallelism 選項之後](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Restrictions"></a> 限制事項  
  
-   成本是指在特定硬體組態下，估計執行序列計畫所需的已耗用時間 (以秒為單位)。 只有在對稱式多重處理器上才應該設定 **cost threshold for parallelism** 。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會忽略 **或** 值：  
  
    -   您的電腦只有一個邏輯處理器。  
  
    -   因為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] affinity mask **組態選項的關係，只有一個邏輯處理器可供** 使用。  
  
    -   **max degree of parallelism** 選項設為 1。  
  
 邏輯處理器是處理器硬體的基本單位，允許作業系統分派工作或執行執行緒內容。 每個邏輯處理器一次只能執行一個執行緒內容。 處理器核心是提供解碼及執行指令能力的電路。 處理器核心可能包含一個或多個邏輯處理器。 下列 [!INCLUDE[tsql](../../includes/tsql-md.md)] 查詢可用於取得系統的 CPU 資訊。  
  
```  
SELECT (cpu_count / hyperthread_ratio) AS PhysicalCPUs,   
cpu_count AS logicalCPUs   
FROM sys.dm_os_sys_info  
```  
  
###  <a name="Recommendations"></a> 建議  
  
-   這個選項是進階選項，只有有經驗的資料庫管理員或通過認證的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 技術人員才可變更。  
  
-   在某些狀況下，即使查詢的成本計畫小於目前的 **cost threshold for parallelism** 值，還是會選擇平行計畫。 之所以會發生這種情形，是因為在決定要使用平行或序列計畫時，所依據的成本預估值是在完成整體最佳化之前提供的。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> 權限  
 不含參數或只含第一個參數之 **sp_configure** 上的執行權限預設會授與所有使用者。 以同時設定兩個參數的 **sp_configure** 來變更組態選項或執行 RECONFIGURE 陳述式時，使用者必須取得 ALTER SETTINGS 伺服器層級權限。 **系統管理員 (sysadmin)** 及 **serveradmin** 固定伺服器角色會隱含 ALTER SETTINGS 權限。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-configure-the-cost-threshold-for-parallelism-option"></a>設定 cost threshold for parallelism 選項  
  
1.  在 [物件總管] 中，以滑鼠右鍵按一下伺服器，然後選取 **[屬性]**。  
  
2.  按一下 **[進階]** 節點。  
  
3.  在 **[平行處理原則]** 下，將 **[CostThresholdForParallelism]** 選項變更為所需的值。 輸入或選取 0 到 32767 之間的值。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-configure-the-cost-threshold-for-parallelism-option"></a>設定 cost threshold for parallelism 選項  
  
1.  連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在標準列中，按一下 **[新增查詢]**。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]**。 此範例示範如何使用 [sp_configure](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql) 將 `cost threshold for parallelism` 選項的值設定為 `10`。  
  
```tsql  
USE AdventureWorks2012 ;  
GO  
EXEC sp_configure 'show advanced options', 1 ;  
GO  
RECONFIGURE  
GO  
EXEC sp_configure 'cost threshold for parallelism', 10 ;  
GO  
RECONFIGURE  
GO  
```  
  
 如需詳細資訊，請參閱 [伺服器設定選項 &#40;SQL Server&#41;](server-configuration-options-sql-server.md)伺服器組態選項。  
  
##  <a name="FollowUp"></a> 待處理：設定 cost threshold for parallelism 選項之後  
 設定會立即生效，不需要重新啟動伺服器。  
  
## <a name="see-also"></a>另請參閱  
 [設定平行索引作業](../../relational-databases/indexes/configure-parallel-index-operations.md)   
 [查詢提示 &#40;Transact-SQL&#41;](/sql/t-sql/queries/hints-transact-sql-query)   
 [ALTER WORKLOAD GROUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-workload-group-transact-sql)   
 [affinity mask 伺服器組態選項](affinity-mask-server-configuration-option.md)   
 [RECONFIGURE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reconfigure-transact-sql)   
 [伺服器組態選項 &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)  
  
  
