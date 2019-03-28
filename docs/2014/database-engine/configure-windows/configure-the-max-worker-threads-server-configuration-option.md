---
title: 設定 max worker threads 伺服器組態選項 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- worker threads [SQL Server]
- max worker threads option
ms.assetid: abeadfa4-a14d-469a-bacf-75812e48fac1
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 5d4aae8a264bd77d51c3365183ee510043ae814b
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/27/2019
ms.locfileid: "58536070"
---
# <a name="configure-the-max-worker-threads-server-configuration-option"></a>設定 max worker threads 伺服器組態選項
  此主題描述如何使用 **或** ，在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中設定 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] max worker threads [!INCLUDE[tsql](../../includes/tsql-md.md)]伺服器組態選項。 **max worker threads** 選項會設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 處理序可使用的工作者執行緒數目。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用作業系統的原生執行緒服務，因此會有一個或多個執行緒同時支援 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 所支援的每個網路、由另一個執行緒負責處理資料庫檢查點，而所有使用者則由一個執行緒集區負責處理。 **max worker threads** 的預設值是 0。 這會讓 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在啟動時自動設定工作者執行緒的數目。 此預設值對大多數系統都是最佳的。 但依系統組態而定，將 **max worker threads** 設為特定的值有時候可提高效能。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
     [建議](#Recommendations)  
  
     [Security](#Security)  
  
-   **使用下列方法設定 max worker threads 選項：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **後續操作：**[設定 max worker threads 選項之後](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Restrictions"></a> 限制事項  
  
-   當實際的查詢要求數目小於 **max worker threads**的設定值時，就會由一個執行緒處理每一個查詢要求。 然而，當實際的查詢要求數目超過 **max worker threads**的設定值時， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 就會將工作者執行緒納入集區中，好讓下一個可用的工作者執行緒來處理要求。  
  
###  <a name="Recommendations"></a> 建議  
  
-   這個選項是進階選項，只有有經驗的資料庫管理員或通過認證的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 技術人員才可變更。  
  
-   當大量用戶端連接到伺服器時，執行緒集區有助於最佳化效能。 通常，會針對每一個查詢要求建立個別的作業系統執行緒。 然而，在數以百計的伺服器連接之下，若每個查詢要求都使用一個執行緒，反而會耗用大量的系統資源。 **max worker threads** 選項可讓 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 建立工作者執行緒集區，以服務更多的查詢要求數量，進而改善效能。  
  
-   下表顯示為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的不同 CPU 和版本組合自動設定的最大工作者執行緒數。  
  
    |CPU 數|32 位元電腦|64 位元電腦|  
    |--------------------|----------------------|----------------------|  
    |\<= 4 個處理器|256|512|  
    |8 個處理器|288|576|  
    |16 個處理器|352|704|  
    |32 個處理器|480|960|  
    |64 個處理器|736|1472|  
    |128 個處理器|4224|4480|  
    |256 個處理器|8320|8576|  
  
    > [!NOTE]  
    >  如需有關使用超過 64 個 CPU 的建議事項，請參閱[在超過 64 個 CPU 之電腦上執行 SQL Server 的最佳作法](https://technet.microsoft.com/library/ee210547\(SQL.105\).aspx)。  
  
    > [!WARNING]  
    >  建議在 32 位元電腦上執行的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的最大工作者執行緒設為 1024。  
  
-   當所有的工作者執行緒都在進行長時間執行的查詢時，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可能會反應遲緩，直到工作者執行緒完成並恢復為可用狀態為止。 雖然這不算是瑕疵，但有時卻讓人困擾。 若處理序反應遲緩，而且無法處理新查詢，請使用專用管理員連接 (DAC) 來連接 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，然後清除處理序。 若要避免這個問題，請增加 max worker threads 的最大數目。  
  
 **max worker threads** 伺服器組態選項不會將所有系統工作 (例如可用性群組、Service Broker、鎖定管理員與其他工作) 需要的執行緒納入考量。  如果超過設定的執行緒數目，下列查詢會提供已產生其他執行緒之系統工作的相關資訊。  
  
```  
SELECT  
s.session_id,  
r.command,  
r.status,  
r.wait_type,  
r.scheduler_id,  
w.worker_address,  
w.is_preemptive,  
w.state,  
t.task_state,  
t.session_id,  
t.exec_context_id,  
t.request_id  
FROM sys.dm_exec_sessions AS s  
INNERJOIN sys.dm_exec_requests AS r  
    ON s.session_id = r.session_id  
INNER JOIN sys.dm_os_tasks AS t  
    ON r.task_address = t.task_address  
INNER JOIN sys.dm_os_workers AS w  
    ON t.worker_address = w.worker_address  
WHERE s.is_user_process = 0;  
  
```  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> 權限  
 不含參數或只含第一個參數之 **sp_configure** 上的執行權限預設會授與所有使用者。 以同時設定兩個參數的 **sp_configure** 來變更組態選項或執行 RECONFIGURE 陳述式時，使用者必須取得 ALTER SETTINGS 伺服器層級權限。 **系統管理員 (sysadmin)** 及 **serveradmin** 固定伺服器角色會隱含 ALTER SETTINGS 權限。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-configure-the-max-worker-threads-option"></a>設定 max worker threads 選項  
  
1.  在物件總管中，請以滑鼠右鍵按一下伺服器，然後選取 [屬性]。  
  
2.  按一下 **[處理器]** 節點。  
  
3.  在 **[最大工作者執行緒]** 方塊中，輸入或選取 128 到 32767 之間任一數值。  
  
     **Max worker threads** 選項可用來設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 處理序可使用的工作者執行緒數目。 **max worker threads** 的預設值對大部份系統而言都是最合適的。 但依系統組態而定，將 **max worker threads** 設為較小的值有時候可提高效能。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-configure-the-max-worker-threads-option"></a>設定 max worker threads 選項  
  
1.  連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在標準列中，按一下 **[新增查詢]**。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]**。 此範例示範如何使用 [sp_configure](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql) 將 `max worker threads` 選項設定為 `900`。  
  
```sql  
USE AdventureWorks2012 ;  
GO  
EXEC sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE ;  
GO  
EXEC sp_configure 'max worker threads', 900 ;  
GO  
RECONFIGURE;  
GO  
  
```  
  
 如需詳細資訊，請參閱 [伺服器設定選項 &#40;SQL Server&#41;](server-configuration-options-sql-server.md)伺服器組態選項。  
  
##  <a name="FollowUp"></a> 後續操作：設定 max worker threads 選項之後  
 變更立即生效，不需要重新啟動 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 。  
  
## <a name="see-also"></a>另請參閱  
 [RECONFIGURE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reconfigure-transact-sql)   
 [伺服器組態選項 &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)   
 [資料庫管理員的診斷連接](diagnostic-connection-for-database-administrators.md)  
  
  
