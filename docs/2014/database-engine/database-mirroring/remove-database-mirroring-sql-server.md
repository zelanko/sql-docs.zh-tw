---
title: 移除資料庫鏡像 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- database mirroring [SQL Server], removing
- removing database mirroring [SQL Server]
ms.assetid: bbc4d7f7-3bc7-40d6-a822-af195fe7f8c0
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: a6d398c2c9d8439025c7ff5ec7a8e4295b24d337
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "62754683"
---
# <a name="remove-database-mirroring-sql-server"></a>移除資料庫鏡像 (SQL Server)
  此主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中移除資料庫內的資料庫鏡像。  資料庫擁有者可以隨時手動移除資料庫的鏡像，藉以停止資料庫鏡像工作階段。  
  
 
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 權限  
 需要資料庫的 ALTER 權限。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-remove-database-mirroring"></a>若要移除資料庫鏡像  
  
1.  在資料庫鏡像工作階段過程中，連接到主體伺服器執行個體，在 [物件總管] 中按一下伺服器名稱，以展開伺服器樹狀目錄。  
  
2.  展開 **[資料庫]** 並選取資料庫。  
  
3.  以滑鼠右鍵按一下資料庫，選取 [工作]****，然後按一下 [鏡像]****。 這會開啟 [**資料庫屬性**] 對話方塊的 [**鏡像**] 頁面。  
  
4.  在 **[選取頁面]** 窗格中按一下 **[鏡像]**。  
  
5.  若要移除鏡像，請按一下 **[移除鏡像]**。 會出現提示要求確認。 如果按一下 **[是]**，會停止工作階段，並從資料庫移除鏡像。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
 若要移除資料庫鏡像，請使用 **[資料庫屬性]**。 使用 **[資料庫屬性]** 對話方塊的 **[鏡像]** 頁面。  
  
#### <a name="to-remove-database-mirroring"></a>若要移除資料庫鏡像  
  
1.  連接到任一個鏡像夥伴的 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 。  
  
2.  在標準列中，按一下 **[新增查詢]** 。  
  
3.  發出下列 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式：  
  
    ```  
    ALTER DATABASE database_name SET PARTNER OFF  
    ```  
  
     其中 *資料庫名稱* 是您要移除其工作階段的鏡像資料庫。  
  
     下列範例會從 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 範例資料庫中移除資料庫鏡像。  
  
    ```  
    ALTER DATABASE AdventureWorks2012 SET PARTNER OFF;  
    ```  
  
##  <a name="follow-up-removing-database-mirroring"></a><a name="FollowUp"></a>後續操作：移除資料庫鏡像  
  
> [!NOTE]  
>  如需移除鏡像之影響的資訊，請參閱[移除資料庫鏡像 &#40;SQL Server&#41;](database-mirroring-sql-server.md)。  
  
-   **如果您打算在資料庫上重新啟動鏡像**  
  
     在您可以重新啟動鏡像之前，您必須先將鏡像移除之後在主體資料庫上建立的所有記錄備份套用到鏡像資料庫。  
  
-   **如果您不打算重新啟動鏡像**  
  
     另外，您也可以選擇復原先前的鏡像資料庫。 在原本是鏡像伺服器的伺服器執行個體上，您可以使用下列 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式：  
  
    ```  
    RESTORE DATABASE database_name WITH RECOVERY;  
    ```  
  
    > [!IMPORTANT]  
    >  如果復原這個資料庫，線上將會有兩個名稱相同但內容不同的資料庫。 因此，您必須確定用戶端只能存取其中一個資料庫 (通常是最新的主體資料庫)。  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> 相關工作  
  
-   [暫停或繼續資料庫鏡像工作階段 &#40;SQL Server&#41;](pause-or-resume-a-database-mirroring-session-sql-server.md)  
  
-   [從資料庫鏡像工作階段移除見證 &#40;SQL Server&#41;](remove-the-witness-from-a-database-mirroring-session-sql-server.md)  
  
-   [使用 Windows 驗證建立資料庫鏡像工作階段 &#40;SQL Server Management Studio&#41;](establish-database-mirroring-session-windows-authentication.md)  
  
-   [使用 Windows 驗證建立資料庫鏡像工作階段 &#40;Transact-SQL&#41;](database-mirroring-establish-session-windows-authentication.md)  
  
-   [範例：使用憑證設定資料庫鏡像 &#40;Transact-SQL&#41;](example-setting-up-database-mirroring-using-certificates-transact-sql.md)  
  
## <a name="see-also"></a>另請參閱  
 [資料庫鏡像 &#40;SQL Server&#41;](database-mirroring-sql-server.md)   
 [設定資料庫鏡像 &#40;SQL Server&#41;](setting-up-database-mirroring-sql-server.md)   
 [AlwaysOn Availability Groups (SQL Server)](../availability-groups/windows/always-on-availability-groups-sql-server.md)  
  
  
