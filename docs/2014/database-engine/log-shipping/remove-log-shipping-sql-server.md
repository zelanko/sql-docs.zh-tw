---
title: 移除記錄傳送 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- log shipping [SQL Server], removing
- removing log shipping
- deleting log shipping
ms.assetid: 859373db-c744-4a4b-8479-45163f61e8cb
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 14fdc36c66073e89dcc2014aed4319a2ce78a98f
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84931109"
---
# <a name="remove-log-shipping-sql-server"></a>移除記錄傳送 (SQL Server)
  本主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 移除 [!INCLUDE[tsql](../../includes/tsql-md.md)]中的記錄傳送。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [安全性](#Security)  
  
-   **若要移除記錄傳送，請使用：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   [相關工作](#RelatedTasks)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 權限  
 記錄傳送預存程序需要 **sysadmin** 固定伺服器角色中的成員資格。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-remove-log-shipping"></a>若要移除記錄傳送  
  
1.  連接至目前是記錄傳送主要伺服器的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體，並展開該執行個體。  
  
2.  展開 [資料庫]  ，以滑鼠右鍵按一下記錄傳送主要資料庫，然後按一下 [屬性]  。  
  
3.  在 **[選取頁面]** 下，按一下 **[交易記錄傳送]** 。  
  
4.  清除 **[將此啟用為記錄傳送組態的主要資料庫 ]** 核取方塊。  
  
5.  按一下 **[確定]** ，以便從這個主要資料庫移除記錄傳送。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-remove-log-shipping"></a>若要移除記錄傳送  
  
1.  在記錄傳送主要伺服器上執行 [sp_delete_log_shipping_primary_secondary](/sql/relational-databases/system-stored-procedures/sp-delete-log-shipping-primary-secondary-transact-sql) ，以刪除主要伺服器上的次要資料庫相關資訊。  
  
2.  在記錄傳送次要伺服器上執行 [sp_delete_log_shipping_secondary_database](/sql/relational-databases/system-stored-procedures/sp-delete-log-shipping-secondary-database-transact-sql) ，以刪除次要資料庫。  
  
    > [!NOTE]  
    >  如果沒有具有相同次要識別碼的其他次要資料庫，就會從 **sp_delete_log_shipping_secondary_database** 叫用 **sp_delete_log_shipping_secondary_primary** ，並刪除次要識別碼的項目與複製及還原作業。  
  
3.  在記錄傳送主要伺服器上執行 **sp_delete_log_shipping_primary_database** ，以刪除主要伺服器上的記錄傳送設定相關資訊。 這也會刪除備份作業。  
  
4.  在記錄傳送主要伺服器上，停用備份作業。 如需詳細資訊，請參閱 [Disable or Enable a Job](../../ssms/agent/disable-or-enable-a-job.md)。  
  
5.  在記錄傳送次要伺服器上，停用複製與還原作業。  
  
6.  若您不再需要使用記錄傳送次要資料庫，也可選擇從次要伺服器中刪除該資料庫。  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> 相關工作  
  
-   [將記錄傳送升級至 SQL Server 2014 &#40;Transact-sql&#41;](upgrading-log-shipping-to-sql-server-2016-transact-sql.md)  
  
-   [設定記錄傳送 &#40;SQL Server&#41;](configure-log-shipping-sql-server.md)  
  
-   [將次要資料庫加入至記錄傳送組態 &#40;SQL Server&#41;](add-a-secondary-database-to-a-log-shipping-configuration-sql-server.md)  
  
-   [從記錄傳送組態中移除次要資料庫 &#40;SQL Server&#41;](remove-a-secondary-database-from-a-log-shipping-configuration-sql-server.md)  
  
-   [監視記錄傳送 &#40;Transact-SQL&#41;](monitor-log-shipping-transact-sql.md)  
  
-   [容錯移轉至記錄傳送次要 &#40;SQL Server&#41;](fail-over-to-a-log-shipping-secondary-sql-server.md)  
  
-   [Disable or Enable a Job](../../ssms/agent/disable-or-enable-a-job.md)  
  
## <a name="see-also"></a>另請參閱  
 [關於記錄傳送 &#40;SQL Server&#41;](about-log-shipping-sql-server.md)   
 [記錄傳送資料表與預存程序](log-shipping-tables-and-stored-procedures.md)  
  
  
