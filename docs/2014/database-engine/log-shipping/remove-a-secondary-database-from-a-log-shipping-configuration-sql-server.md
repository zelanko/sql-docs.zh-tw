---
title: 從記錄傳送設定中移除次要資料庫 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- deleting secondary databases
- secondary databases [SQL Server], in log shipping
- removing secondary databases
- secondary data files [SQL Server], removing
- log shipping [SQL Server], secondary databases
ms.assetid: ebe368a4-ca1c-45d0-9a71-3ddbd5b26a8e
caps.latest.revision: 18
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: b8bb81e77c75e8fd385fbe9221a5f66cdf0cd548
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36031973"
---
# <a name="remove-a-secondary-database-from-a-log-shipping-configuration-sql-server"></a>從記錄傳送組態中移除次要資料庫 (SQL Server)
  本主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 移除 [!INCLUDE[tsql](../../includes/tsql-md.md)]中的記錄傳送次要資料庫。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [Security](#Security)  
  
-   **若要移除記錄傳送次要資料庫，請使用：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   [相關工作](#RelatedTasks)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> 權限  
 記錄傳送預存程序需要 **sysadmin** 固定伺服器角色中的成員資格。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-remove-a-log-shipping-secondary-database"></a>若要移除記錄傳送次要資料庫  
  
1.  連接至目前是記錄傳送主要伺服器的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體，並展開該執行個體。  
  
2.  展開 [資料庫]，以滑鼠右鍵按一下記錄傳送主要資料庫，然後按一下 [屬性]。  
  
3.  在 **[選取頁面]** 下，按一下 **[交易記錄傳送]**。  
  
4.  在 **[次要伺服器執行個體與資料庫]** 下，按一下您要移除的資料庫。  
  
5.  按一下 **[移除]**。  
  
6.  按一下 **[確定]** 以更新組態。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-remove-a-secondary-database"></a>若要移除次要資料庫  
  
1.  在主要伺服器上，執行 [sp_delete_log_shipping_primary_secondary](/sql/relational-databases/system-stored-procedures/sp-delete-log-shipping-primary-secondary-transact-sql) 以刪除主要伺服器上關於次要資料庫的資訊。  
  
2.  在次要伺服器上，執行 [sp_delete_log_shipping_secondary_database](/sql/relational-databases/system-stored-procedures/sp-delete-log-shipping-secondary-database-transact-sql) 以刪除次要資料庫。  
  
    > [!NOTE]  
    >  如果沒有具有相同次要識別碼的其他次要資料庫，就會從 **sp_delete_log_shipping_secondary_database** 叫用 **sp_delete_log_shipping_secondary_primary** ，並且刪除次要識別碼的項目及複製與還原作業。  
  
3.  在次要伺服器上停用複製與還原作業。 如需詳細資訊，請參閱 [Disable or Enable a Job](../../ssms/agent/disable-or-enable-a-job.md)。  
  
##  <a name="RelatedTasks"></a> 相關工作  
  
-   [升級記錄傳送到 SQL Server 2014 &#40;Transact SQL&#41;](upgrading-log-shipping-to-sql-server-2016-transact-sql.md)  
  
-   [設定記錄傳送 &#40;SQL Server&#41;](configure-log-shipping-sql-server.md)  
  
-   [將次要資料庫加入至記錄傳送組態 &#40;SQL Server&#41;](add-a-secondary-database-to-a-log-shipping-configuration-sql-server.md)  
  
-   [移除記錄傳送 &#40;SQL Server&#41;](remove-log-shipping-sql-server.md)  
  
-   [檢視記錄傳送報表 &#40;SQL Server Management Studio&#41;](view-the-log-shipping-report-sql-server-management-studio.md)  
  
-   [監視記錄傳送 &#40;Transact-SQL&#41;](monitor-log-shipping-transact-sql.md)  
  
-   [容錯移轉至記錄傳送次要 &#40;SQL Server&#41;](fail-over-to-a-log-shipping-secondary-sql-server.md)  
  
## <a name="see-also"></a>另請參閱  
 [關於記錄傳送 &#40;SQL Server&#41;](about-log-shipping-sql-server.md)   
 [記錄傳送資料表與預存程序](log-shipping-tables-and-stored-procedures.md)  
  
  
