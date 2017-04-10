---
title: "變更主要與次要記錄傳送伺服器間的角色 (SQL Server) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-high-availability"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "記錄傳送 [SQL Server]，角色變更"
  - "次要資料檔 [SQL Server]，在其間變更的角色"
  - "主要資料庫 [SQL Server]"
  - "初始角色變更 [SQL Server]"
  - "記錄傳送 [SQL Server]，容錯移轉"
  - "容錯移轉 [SQL Server]，記錄傳送"
ms.assetid: 2d7cc40a-47e8-4419-9b2b-7c69f700e806
caps.latest.revision: 20
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 20
---
# 變更主要與次要記錄傳送伺服器間的角色 (SQL Server)
  將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 記錄傳送組態容錯移轉到次要伺服器之後，您可以設定次要資料庫做為主要資料庫。 接著，您就可以視需要交換主要與次要資料庫。  
  
## 執行初始角色變更  
 初次想要容錯移轉到次要資料庫，並將它作為主要資料庫時，您必須採取一連串的步驟。 遵循並完成這些初始步驟之後，您就可以輕輕鬆鬆交換主要資料庫與次要資料庫間的角色。  
  
1.  從主要資料庫手動容錯移轉到次要資料庫。 請確定要使用 NORECOVERY，在主要伺服器上備份使用中的交易記錄檔。 如需詳細資訊，請參閱[容錯移轉至記錄傳送次要 &#40;SQL Server&#41;](../../database-engine/log-shipping/fail-over-to-a-log-shipping-secondary-sql-server.md)。  
  
2.  停用原始主要伺服器上的記錄傳送備份作業，以及原始次要伺服器上的複製與還原作業。  
  
3.  在次要資料庫上 (要它作為新的主要資料庫)，使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 設定記錄傳送。 如需詳細資訊，請參閱[設定記錄傳送 &#40;SQL Server&#41;](../../database-engine/log-shipping/configure-log-shipping-sql-server.md)。 包括以下步驟：  
  
    1.  使用您已為原始主要伺服器建立的相同共用，來建立備份。  
  
    2.  新增次要資料庫時，請在 **[次要資料庫設定]** 對話方塊的 **[次要資料庫]** 方塊中，輸入原始的資料庫名稱。  
  
    3.  在 **[次要資料庫設定]** 對話方中，選取 **[否，次要資料庫已初始化]**。  
  
4.  如果您先前的記錄傳送組態已啟用記錄傳送監視，請將記錄傳送監視重新設定為監視新的記錄傳送組態。  執行下列命令，以資料庫的名稱取代 *database_name*：  
  
    1.  **在新的主要伺服器上**  
  
         執行下列 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式：  
  
        ```  
        -- Statement to execute on the new primary server  
        USE msdb  
        GO  
        EXEC master.dbo.sp_change_log_shipping_secondary_database @secondary_database = N'database_name', @threshold_alert_enabled = 0;  
        GO  
        ```  
  
    2.  **在新的次要伺服器上**  
  
         執行下列 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式：  
  
        ```  
        -- Statement to execute on the new secondary server  
        USE msdb  
        GO  
        EXEC master.dbo.sp_change_log_shipping_primary_database @database=N'database_name', @threshold_alert_enabled = 0;  
        GO  
        ```  
  
## 交換角色  
 完成上述初始角色變更的步驟後，可遵循此節的步驟變更主要資料庫與次要資料庫間的角色。 若要執行角色變更，請遵循以下的一般步驟：  
  
1.  使次要資料庫連線工作，使用 NORECOVERY 備份主要伺服器上的交易記錄檔。  
  
2.  停用原始主要伺服器上的記錄傳送備份作業，以及原始次要伺服器上的複製與還原作業。  
  
3.  啟用次要伺服器 (新的主要伺服器) 上的記錄傳送備份作業，以及主要伺服器 (新的次要伺服器) 上的複製與還原工作。  
  
> [!IMPORTANT]  
>  當您將次要資料庫變更為主要資料庫時，為了提供一致的經驗給使用者和應用程式，可能需要在新主要伺服器執行個體上為資料庫重新建立部份或全部的中繼資料，例如登入和作業。 如需詳細資訊，請參閱[在另一個伺服器執行個體上提供可用的資料庫時，管理中繼資料 &#40;SQL Server&#41;](../../relational-databases/databases/manage metadata when making a database available on another server.md)。  
  
##  <a name="RelatedTasks"></a> 相關工作  
  
-   [容錯移轉至記錄傳送次要 &#40;SQL Server&#41;](../../database-engine/log-shipping/fail-over-to-a-log-shipping-secondary-sql-server.md)  
  
-   [角色切換後針對登入和作業進行管理 &#40;SQL Server&#41;](../../sql-server/failover-clusters/management-of-logins-and-jobs-after-role-switching-sql-server.md)  
  
## 另請參閱  
 [記錄傳送資料表與預存程序](../../database-engine/log-shipping/log-shipping-tables-and-stored-procedures.md)  
  
  