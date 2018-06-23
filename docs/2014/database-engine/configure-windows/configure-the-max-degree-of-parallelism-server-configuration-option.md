---
title: 設定 max degree of parallelism 伺服器組態選項 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- parallel queries [SQL Server]
- processors [SQL Server], parallel queries
- number of processors for parallel queries
- max degree of parallelism option
ms.assetid: 86b65bf1-a6a1-4670-afc0-cdfad1558032
caps.latest.revision: 30
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: aca180298fef5edde0d2923e6676a535915bb5ce
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36136278"
---
# <a name="configure-the-max-degree-of-parallelism-server-configuration-option"></a>設定 max degree of parallelism 伺服器組態選項
  本主題描述如何設定`max degree of parallelism`伺服器組態選項中的[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]使用[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]或[!INCLUDE[tsql](../../includes/tsql-md.md)]。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體在具有多個微處理器或 CPU 的電腦上執行時，會偵測平行處理原則的最佳程度，也就是說，針對每一個平行計畫的執行，執行單一陳述式所要採用的處理器個數。 您可以使用 `max degree of parallelism` 選項來限制執行平行計畫所用的處理器數目。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 考慮針對查詢、 索引資料定義語言 (DDL) 作業，以及靜態和索引鍵集驅動資料指標擴展平行執行計畫。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
     [建議](#Recommendations)  
  
     [Security](#Security)  
  
-   **若要設定 max degree of parallelism 選項，使用：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **待處理**  [設定 max degree of parallelism 選項之後](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Restrictions"></a> 限制事項  
  
-   如果 affinity mask 選項不是設成預設值，它可能會限制對稱式多處理 (SMP) 系統上 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可用的處理器個數。  
  
###  <a name="Recommendations"></a> 建議  
  
-   這個選項是進階選項，只有有經驗的資料庫管理員或通過認證的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 技術人員才可變更。  
  
-   若要讓伺服器判斷平行處理原則的最大程度，請將此選項設定為 0 (預設值)。 將平行處理原則的最大程度設定為 0 就會允許 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用所有可用的處理器 (最多 64 個處理器)。 若要抑制平行計畫的產生，請將 `max degree of parallelism` 設定為 1。 將此值設成 1 到 32,767 的數字會指定單一查詢執行可用的最大處理器核心數目。 如果指定的數值大於可用的處理器數目，就會使用可用處理器的實際數目。 如果電腦只有一個處理器，則會忽略 `max degree of parallelism` 值。  
  
-   您可以在查詢陳述適中指定 MAXDOP 查詢提示，來覆寫查詢中的 max degree of parallelism 值。 如需詳細資訊，請參閱[查詢提示 &#40;Transact-SQL&#41;](/sql/t-sql/queries/hints-transact-sql-query)。  
  
-   建立或重建索引的索引作業，或者卸除叢集索引的索引作業，都需要大量資源。 您可以在索引陳述式中指定 MAXDOP 索引選項，覆寫索引作業中的 max degree of parallelism 值。 MAXDOP 值會在執行時套用至陳述式，且不會儲存在索引中繼資料內。 如需詳細資訊，請參閱 [設定平行索引作業](../../relational-databases/indexes/configure-parallel-index-operations.md)。  
  
-   除了查詢作業和索引作業外，此選項也會控制 DBCC CHECKTABLE、DBCC CHECKDB 和 DBCC CHECKFILEGROUP 的平行處理原則。 您可以使用追蹤旗標 2528 來停用這些陳述式的平行執行計畫。 如需詳細資訊，請參閱[追蹤旗標 &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql)。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> 權限  
 不含參數或只含第一個參數之 **sp_configure** 上的執行權限預設會授與所有使用者。 以同時設定兩個參數的 **sp_configure** 來變更組態選項或執行 RECONFIGURE 陳述式時，使用者必須取得 ALTER SETTINGS 伺服器層級權限。 **系統管理員 (sysadmin)** 及 **serveradmin** 固定伺服器角色會隱含 ALTER SETTINGS 權限。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-configure-the-max-degree-of-parallelism-option"></a>設定 max degree of parallelism 選項  
  
1.  在 **[物件總管]** 中，以滑鼠右鍵按一下伺服器，然後選取 **[屬性]**。  
  
2.  按一下 **[進階]** 節點。  
  
3.  在 **[平行處理原則的最大程度]** 方塊中，選取用於執行平行計畫的最大處理器數目。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-configure-the-max-degree-of-parallelism-option"></a>設定 max degree of parallelism 選項  
  
1.  連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在標準列中，按一下 **[新增查詢]**。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]**。 此範例示範如何使用 [sp_configure](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql) 將 `max degree of parallelism` 選項設定為 `8`。  
  
```tsql  
USE AdventureWorks2012 ;  
GO   
EXEC sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE WITH OVERRIDE;  
GO  
EXEC sp_configure 'max degree of parallelism', 8;  
GO  
RECONFIGURE WITH OVERRIDE;  
GO  
```  
  
 如需詳細資訊，請參閱 [伺服器組態選項 &#40;SQL Server&#41;](server-configuration-options-sql-server.md)。  
  
##  <a name="FollowUp"></a> 待處理：設定 max degree of parallelism 選項之後  
 設定會立即生效，不需要重新啟動伺服器。  
  
## <a name="see-also"></a>另請參閱  
 [affinity mask 伺服器組態選項](affinity-mask-server-configuration-option.md)   
 [RECONFIGURE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reconfigure-transact-sql)   
 [伺服器組態選項 &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)   
 [CREATE INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-index-transact-sql)   
 [ALTER INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-index-transact-sql)   
 [ALTER TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-table-transact-sql)   
 [DBCC CHECKTABLE &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-checktable-transact-sql)   
 [DBCC CHECKDB &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-checkdb-transact-sql)   
 [DBCC CHECKFILEGROUP &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-checkfilegroup-transact-sql)   
 [設定平行索引作業](../../relational-databases/indexes/configure-parallel-index-operations.md)   
 [查詢提示 &#40;Transact-SQL&#41;](/sql/t-sql/queries/hints-transact-sql-query)   
 [設定索引選項](../../relational-databases/indexes/set-index-options.md)  
  
  
