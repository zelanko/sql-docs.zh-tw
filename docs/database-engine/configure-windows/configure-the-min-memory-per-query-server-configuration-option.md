---
title: 設定 min memory per query 伺服器組態選項 | Microsoft Docs
ms.custom: ''
ms.date: 11/24/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- memory [SQL Server], queries
- minimum query memory
- queries [SQL Server], memory
- min memory per query option
- min memory grant
ms.assetid: ecd3fb79-b4a6-432f-9ef5-530e0d42d5a6
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 9e7a08defb9ff222ac1699c924691c923a7f2c2e
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2020
ms.locfileid: "68012510"
---
# <a name="configure-the-min-memory-per-query-server-configuration-option"></a>設定 min memory per query 伺服器組態選項
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  此主題描述如何使用 **或** ，在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中設定 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] min memory per query [!INCLUDE[tsql](../../includes/tsql-md.md)]伺服器組態選項。 **每個查詢的最小記憶體** 選項會指定為執行查詢所配置的最小記憶體數量 (以 KB 為單位)。 這也稱為最小記憶體授與。 例如，如果將 **min memory per query** 設成 2,048 KB，就可以保證查詢至少有這些記憶體量可使用。 預設值為 1,024 KB。 最小值是 512 KB，最大值則是 2,147,483,647 KB (2 GB)。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
     [建議](#Recommendations)  
  
     [安全性](#Security)  
  
-   **使用下列方法設定 min memory per query 選項：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **後續操作：** [設定每個查詢的最小記憶體選項之後](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Restrictions"></a> 限制事項  
  
-   每個查詢的最小記憶體數量之優先順序，高於 [[索引建立記憶體]](../../database-engine/configure-windows/configure-the-index-create-memory-server-configuration-option.md) 選項。 若您同時變更了兩個選項，且索引建立記憶體選項小於每個查詢的最小記憶體，您會看到警告訊息，但仍會設定該值。 執行查詢時，您會看到另一個類似的警告。  
  
###  <a name="Recommendations"></a> 建議  
  
-   此選項是進階選項，只有具經驗的資料庫管理員或通過認證的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 專業人員才可變更。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 查詢處理器會嘗試判斷要配置給查詢的最佳記憶體數量。 min memory per query 選項可讓系統管理員指定任何單一查詢所接收的最小記憶體數量。 若查詢中含有大量資料的雜湊和排序作業，則這些查詢通常會接收比此值更多的記憶體。 提高 min memory per query 的值也許可以改善一些小型至中型查詢的效能，但這樣做也可能導致競用記憶體資源的情形增加。 每個查詢的最小記憶體選項包含為排序作業所配置的記憶體。  

-    因為查詢必須等到<sup>1</sup>其可取得要求的最小記憶體，或是等到超過查詢等候伺服器設定選項中指定的值為止，所以請勿將 min memory per query 伺服器設定選項設得太高，特別是在非常忙碌的系統上。 如果可用的記憶體多於執行所需的指定最小值，那麼只要記憶體可以有效地供查詢使用，查詢就會利用額外的記憶體。     

<sup>1</sup> 在此情況下，等候類型通常是 RESOURCE_SEMAPHORE。 如需詳細資訊，請參閱 [sys.dm_os_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md)。

###  <a name="Security"></a> Security  
  
####  <a name="Permissions"></a> 權限  
 不含參數或只含第一個參數之 **sp_configure** 上的執行權限預設會授與所有使用者。 以同時設定兩個參數的 **sp_configure** 來變更組態選項或執行 RECONFIGURE 陳述式時，使用者必須取得 ALTER SETTINGS 伺服器層級權限。 **系統管理員 (sysadmin)** 及 **serveradmin** 固定伺服器角色會隱含 ALTER SETTINGS 權限。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-configure-the-min-memory-per-query-option"></a>設定 min memory per query 選項  
  
1.  在物件總管中，請以滑鼠右鍵按一下伺服器，然後選取 [屬性]  。  
  
2.  按一下 **[記憶體]** 節點。  
  
3.  在 **[每個查詢的最小記憶體]** 方塊中，輸入將為執行查詢而配置的最小記憶體數量 (以 KB 為單位)。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-configure-the-min-memory-per-query-option"></a>設定 min memory per query 選項  
  
1.  連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在標準列中，按一下 **[新增查詢]** 。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]** 。 此範例示範如何使用 [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) 將 `min memory per query` 選項的值設定為 `3500` KB。  
  
```sql  
USE AdventureWorks2012 ;  
GO  
EXEC sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE ;  
GO  
EXEC sp_configure 'min memory per query', 3500 ;  
GO  
RECONFIGURE;  
GO    
```  
  
##  <a name="FollowUp"></a> 後續操作：設定每個查詢的最小記憶體選項之後  
 設定會立即生效，不需要重新啟動伺服器。  
  
## <a name="see-also"></a>另請參閱  
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [伺服器組態選項 &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [設定 index create memory 伺服器設定選項](../../database-engine/configure-windows/configure-the-index-create-memory-server-configuration-option.md)     
 [sys.dm_os_wait_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md)     
 [sys.dm_exec_query_memory_grants &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-memory-grants-transact-sql.md)
  
  
