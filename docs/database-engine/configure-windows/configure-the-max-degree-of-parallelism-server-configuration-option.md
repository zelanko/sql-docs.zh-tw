---
title: 設定 max degree of parallelism 伺服器組態選項 | Microsoft Docs
ms.custom: ''
ms.date: 02/12/2020
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- parallel queries [SQL Server]
- processors [SQL Server], parallel queries
- number of processors for parallel queries
- max degree of parallelism option
- MaxDop
ms.assetid: 86b65bf1-a6a1-4670-afc0-cdfad1558032
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 47b9704591acd305a49ff315eb99314f14e87af1
ms.sourcegitcommit: 38c61c7e170b57dddaae5be72239a171afd293b9
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/14/2020
ms.locfileid: "77259223"
---
# <a name="configure-the-max-degree-of-parallelism-server-configuration-option"></a>設定 max degree of parallelism 伺服器組態選項
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  本主題描述如何使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或 [!INCLUDE[tsql](../../includes/tsql-md.md)]，在 SQL Server 中設定 [平行處理原則的最大程度 (MAXDOP)]  伺服器組態選項。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體在具有多個微處理器或 CPU 的電腦上執行時，會偵測平行處理原則的程度，也就是說，針對每一個平行計畫的執行，執行單一陳述式所要採用的處理器個數。 您可以使用 **max degree of parallelism** 選項來限制要用於平行計畫執行的處理器數目。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會針對查詢、索引資料定義語言 (DDL) 作業、平行插入、線上改變資料行、平行收集統計資料，以及靜態和索引鍵集驅動資料指標擴展，考慮平行執行計畫。

> [!NOTE]
> [!INCLUDE [sssqlv15-md](../../includes/sssqlv15-md.md)] 引入在安裝程序中設定 MAXDOP 的自動建議。 安裝程式使用者介面可讓您接受建議的設定或自訂設定。 如需詳細資訊，請參閱下列文章：
>  - [MaxDOP 已新增至 SQL 2019 安裝程式](https://techcommunity.microsoft.com/t5/premier-field-engineering/maxdop-added-to-sql-2019-ctp3-0-setup/ba-p/780071) (英文)
>  - [適用於 MAXDOP 和最大記憶體的 SQL Server 2019 安裝增強功能](https://www.mssqltips.com/sqlservertip/6211/sql-server-2019-installation-enhancements-for-maxdop-and-max-memory/) (英文)
>

##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Restrictions"></a> 限制事項  
  
-   如果 affinity mask 選項不是設成預設值，它可能會限制對稱式多處理 (SMP) 系統上 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可用的處理器個數。  

-   **平行處理原則最大程度 (MAXDOP)** 限制的設定會根據[工作](../../relational-databases/system-dynamic-management-views/sys-dm-os-tasks-transact-sql.md)。 它不是根據[要求](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)或查詢限制。 這表示平行查詢執行期間，單一要求可能會產生指派至排程器的多個工作。 如需詳細資訊，請參閱[執行緒與工作架構指南](../../relational-databases/thread-and-task-architecture-guide.md)。 
  
###  <a name="Recommendations"></a> 建議  
  
-   此選項是進階選項，只有具經驗的資料庫管理員或通過認證的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 專業人員才可變更。  
  
-   若要讓伺服器判斷平行處理原則的最大程度，請將此選項設定為 0 (預設值)。 將平行處理原則的最大程度設定為 0 就會允許 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用所有可用的處理器 (最多 64 個處理器)。 若要抑制平行計畫的產生，請將 **max degree of parallelism** 設成 1。 將此值設成 1 到 32,767 的數字會指定單一查詢執行可用的最大處理器核心數目。 如果指定的數值大於可用的處理器數目，就會使用可用處理器的實際數目。 如果電腦只有一個處理器，則會忽略 **max degree of parallelism** 值。  
  
-   您可以在查詢陳述適中指定 MAXDOP 查詢提示，來覆寫查詢中的 max degree of parallelism 值。 如需詳細資訊，請參閱[查詢提示 &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-query.md)。  
  
-   建立或重建索引的索引作業，或者卸除叢集索引的索引作業，都需要大量資源。 您可以在索引陳述式中指定 MAXDOP 索引選項，覆寫索引作業中的 max degree of parallelism 值。 MAXDOP 值會在執行時套用至陳述式，且不會儲存在索引中繼資料內。 如需詳細資訊，請參閱 [設定平行索引作業](../../relational-databases/indexes/configure-parallel-index-operations.md)。  
  
-   除了查詢作業和索引作業外，此選項也會控制 DBCC CHECKTABLE、DBCC CHECKDB 和 DBCC CHECKFILEGROUP 的平行處理原則。 您可以使用追蹤旗標 2528 來停用這些陳述式的平行執行計畫。 如需詳細資訊，請參閱[追蹤旗標 &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)。

> [!TIP]
> 若要在查詢層級完成此操作，請使用 **MAXDOP** [查詢提示](../../t-sql/queries/hints-transact-sql-query.md)。     
> 若要在資料庫層級完成此操作，請使用 **MAXDOP** [資料庫範圍設定](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)。      
> 若要在工作負載層級完成此操作，請使用 **MAX_DOP** [Resource Governor 工作負載群組組態選項](../../t-sql/statements/create-workload-group-transact-sql.md)。      

###  <a name="Guidelines"></a> 指導方針  
從 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 開始，若 [!INCLUDE[ssde_md](../../includes/ssde_md.md)] 在服務啟動期間偵測到啟動時每個 NUMA 節點或通訊端有超過八個實體核心，則會根據預設自動建立軟體式 NUMA 節點。 [!INCLUDE[ssde_md](../../includes/ssde_md.md)] 會將來自相同實體核心的邏輯處理器放入不同軟體式 NUMA 節點。 下表中建議事項目標是使所有平行查詢的背景工作執行緒保持在相同軟體式 NUMA 節點內。 這會改善查詢效能及工作負載 NUMA 節點中的背景工作執行緒分佈。 如需詳細資訊，請參閱[軟體式 NUMA](../../database-engine/configure-windows/soft-numa-sql-server.md)。

從 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 開始，請在您設定**最大平行處理程度**伺服器設定值時，使用下列方針：

||||
|----------------|-----------------|-----------------|
|具有單一 NUMA 節點的伺服器|小於或等於 8 個邏輯處理器|MAXDOP 保持在或低於 # 個邏輯處理器數目|
|具有單一 NUMA 節點的伺服器|多於 8 個邏輯處理器|MAXDOP 保持在 8|
|具有多個 NUMA 節點的伺服器|每個 NUMA 節點小於或等於 16 個邏輯處理器|每個 NUMA 節點的 MAXDOP 保持在或低於 # 個邏輯處理器數目|
|具有多個 NUMA 節點的伺服器|每個 NUMA 節點多於 16 個邏輯處理器|將 MAXDOP 保持在最大 (MAX) 值為每個 NUMA 節點 16 個邏輯伺服器數量的一半|
  
> [!NOTE]
> 上表中的 NUMA 節點指的是由 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 及更高版本自動建立的軟體式 NUMA 節點，若已停用軟體式 NUMA，則為硬體式 NUMA 節點。   
>  請在您為 Resource Governor 工作負載群組設定平行處理最大程度的選項時，使用這些相同的方針。 如需詳細資訊，請參閱 [CREATE WORKLOAD GROUP (Transact-SQL)](../../t-sql/statements/create-workload-group-transact-sql.md)。
  
從 [!INCLUDE[ssKatmai](../../includes/ssKatmai-md.md)] 到 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]，請在您設定**最大平行處理程度**伺服器設定值時，使用下列方針：

||||
|----------------|-----------------|-----------------|
|具有單一 NUMA 節點的伺服器|小於或等於 8 個邏輯處理器|MAXDOP 保持在或低於 # 個邏輯處理器數目|
|具有單一 NUMA 節點的伺服器|多於 8 個邏輯處理器|MAXDOP 保持在 8|
|具有多個 NUMA 節點的伺服器|每個 NUMA 節點小於或等於 8 個邏輯處理器|每個 NUMA 節點的 MAXDOP 保持在或低於 # 個邏輯處理器數目|
|具有多個 NUMA 節點的伺服器|每個 NUMA 節點多於 8 個邏輯處理器|MAXDOP 保持在 8|
  
###  <a name="Security"></a> Security  
  
####  <a name="Permissions"></a> 權限  
 不含參數或只含第一個參數之 **sp_configure** 上的執行權限預設會授與所有使用者。 以同時設定兩個參數的 **sp_configure** 來變更組態選項或執行 RECONFIGURE 陳述式時，使用者必須取得 ALTER SETTINGS 伺服器層級權限。 **系統管理員 (sysadmin)** 及 **serveradmin** 固定伺服器角色會隱含 ALTER SETTINGS 權限。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-configure-the-max-degree-of-parallelism-option"></a>設定 max degree of parallelism 選項  
  
1.  在 **[物件總管]** 中，以滑鼠右鍵按一下伺服器，然後選取 **[屬性]** 。  
  
2.  按一下 **[進階]** 節點。  
  
3.  在 **[平行處理原則的最大程度]** 方塊中，選取用於執行平行計畫的最大處理器數目。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-configure-the-max-degree-of-parallelism-option"></a>設定 max degree of parallelism 選項  
  
1.  連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在標準列中，按一下 **[新增查詢]** 。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]** 。 此範例示範如何使用 [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) 將 `max degree of parallelism` 選項設定為 `8`。  
  
```sql  
USE AdventureWorks2012 ;  
GO   
EXEC sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE WITH OVERRIDE;  
GO  
EXEC sp_configure 'max degree of parallelism', 16;  
GO  
RECONFIGURE WITH OVERRIDE;  
GO  
```  
  
 如需詳細資訊，請參閱 [伺服器設定選項 &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)伺服器組態選項。  
  
##  <a name="FollowUp"></a> 後續操作：在您設定完最大平行處理程度的選項後  
 設定會立即生效，不需要重新啟動伺服器。  
  
## <a name="see-also"></a>另請參閱  
 [ALTER DATABASE SCOPED CONFIGURATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)      
 [SQL Server 中 [平行處理原則最大程度] 設定選項的建議和指導方針](https://support.microsoft.com/help/2806535)     
 [affinity mask 伺服器組態選項](../../database-engine/configure-windows/affinity-mask-server-configuration-option.md)   
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [伺服器組態選項 &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [查詢處理架構指南](../../relational-databases/query-processing-architecture-guide.md#DOP)       
 [執行緒和工作架構指南](../../relational-databases/thread-and-task-architecture-guide.md)    
 [設定平行索引作業](../../relational-databases/indexes/configure-parallel-index-operations.md)    
 [查詢提示 &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-query.md)     
 [設定索引選項](../../relational-databases/indexes/set-index-options.md)     
