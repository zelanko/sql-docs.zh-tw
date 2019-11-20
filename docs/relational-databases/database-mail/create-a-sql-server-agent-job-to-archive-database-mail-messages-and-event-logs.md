---
title: 建立 SQL Server Agent 作業以封存 Database Mail 訊息及事件
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- archiving mail messages and attachments [SQL Server]
- removing mail messages and attachements
- Database Mail [SQL Server], archiving
- saving mail messages and attachments
ms.assetid: 8f8f0fba-f750-4533-9b76-a9cdbcdc3b14
author: stevestein
ms.author: sstein
ms.custom: seo-dt-2019
ms.openlocfilehash: 926822356c6e7f9f4d775ca0710ee2f815c0e7f5
ms.sourcegitcommit: 15fe0bbba963d011472cfbbc06d954d9dbf2d655
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/14/2019
ms.locfileid: "74094499"
---
# <a name="create-a-sql-server-agent-job-to-archive-database-mail-messages-and-event-logs"></a>建立 SQL Server Agent 作業以封存 Database Mail 訊息及事件記錄檔
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  Database Mail 訊息的副本及其附件會隨著 Database Mail 事件記錄檔一起保留在 **msdb** 資料表。 您可能需要定期減少資料表的大小，並封存不再需要的訊息和事件。 下列程序可建立 SQL Server Agent 作業以便自動執行程序。  
  
-   **開始之前**  ： [必要條件](#Prerequisites)、 [建議](#Recommendations)、 [權限](#Permissions)  
  
-   **使用以下方式封存 Database Mail 訊息和記錄：** [SQL Server Agent](#Process_Overview)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Prerequisites"></a> 必要條件  
 要儲存封存資料的新資料表可能位在特殊的封存資料庫中。 資料列也可以匯出至文字檔。  
   
###  <a name="Recommendations"></a> 建議  
 在實際執行環境中，您可能會想要加入其他錯誤檢查，並在作業失敗時傳送電子郵件訊息給操作員。  
  
  
###  <a name="Permissions"></a> 權限  
 您必須是 **系統管理員 (sysadmin)** 固定伺服器角色的成員，才能執行此主題中所描述的預存程序。  
  
  
###  <a name="Process_Overview"></a> 處理序的概觀  
  
-   第一個程序會建立一個名稱為「封存 Database Mail」的作業，此作業包含下列步驟。  
  
    1.  將 Database Mail 資料表的所有訊息複製到新資料表，該新資料表是以上個月來命名，格式為 **DBMailArchive_** <年_月>  。  
  
    2.  將第一個步驟複製之訊息的相關附件，從 Database Mail 資料表複製到新資料表，該新資料表是以上個月來命名，格式為 **DBMailArchive_Attachments_** <年_月>  。  
  
    3.  將 Database Mail 事件記錄檔中第一個步驟複製之訊息的相關事件，從 Database Mail 資料表複製到新資料表，該新資料表是以上個月來命名，格式為 **DBMailArchive_Log_** <年_月>  。  
  
    4.  刪除 Database Mail 資料表中已轉移郵件項目的記錄。  
  
    5.  刪除 Database Mail 事件記錄檔中已轉移郵件項目的相關事件。  
  
-   排程定期執行作業。  
  
  
## <a name="to-create-a-sql-server-agent-job"></a>若要建立 SQL Server Agent 作業  
  
1.  在 [物件總管] 中，展開 [ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent]，以滑鼠右鍵按一下 **[作業]** ，然後按一下 **[新增作業]** 。  
  
2.  在 **[新增作業]** 對話方塊的 **[名稱]** 方塊中，輸入 **封存 Database Mail**。  
  
3.  在 **[擁有者]** 方塊中，確認該位擁有者是 **系統管理員 (sysadmin)** 固定伺服器角色的成員。  
  
4.  在 **[類別目錄]** 方塊中，按一下 **[資料庫維護]** 。  
  
5.  在 **[描述]** 方塊中，輸入 **[封存 Database Mail 訊息]** ，然後按一下 **[步驟]** 。  

 [概觀](#Process_Overview)  
  
## <a name="to-create-a-step-to-archive-the-database-mail-messages"></a>建立封存 Database Mail 訊息的步驟  
  
1.  在 **[步驟]** 頁面上，按一下 **[新增]** 。  
  
2.  在 **[步驟名稱]** 方塊中，輸入 **複製 Database Mail 項目**。  
  
3.  在 **[類型]** 方塊中，選取 **[Transact-SQL 指令碼 (T-SQL)]** 。  
  
4.  在 **[資料庫]** 方塊中，選取 **[msdb]** 。  
  
5.  在 **[命令]** 方塊中，輸入下列陳述式建立一個資料表，以上一個月份命名，包含這個月之前的所有資料列：  
  
    ```sql  
    DECLARE @LastMonth nvarchar(12);  
    DECLARE @CopyDate nvarchar(20) ;  
    DECLARE @CreateTable nvarchar(250) ;  
    SET @LastMonth = (SELECT CAST(DATEPART(yyyy,GETDATE()) AS CHAR(4)) + '_' + CAST(DATEPART(mm,GETDATE())-1 AS varchar(2))) ;  
    SET @CopyDate = (SELECT CAST(CONVERT(char(8), CURRENT_TIMESTAMP- DATEPART(dd,GETDATE()-1), 112) AS datetime))  
    SET @CreateTable = 'SELECT * INTO msdb.dbo.[DBMailArchive_' + @LastMonth + '] FROM sysmail_allitems WHERE send_request_date < ''' + @CopyDate +'''';  
    EXEC sp_executesql @CreateTable ;  
    ```  
  
6.  按一下 **[確定]** 以儲存步驟。  
  
 [概觀](#Process_Overview)  
  
## <a name="to-create-a-step-to-archive-the-database-mail-attachments"></a>建立封存 Database Mail 附加檔案的步驟  
  
1.  在 **[步驟]** 頁面上，按一下 **[新增]** 。  
  
2.  在 **[步驟名稱]** 方塊中，輸入 **複製 Database Mail 附加檔案**。  
  
3.  在 **[類型]** 方塊中，選取 **[Transact-SQL 指令碼 (T-SQL)]** 。  
  
4.  在 **[資料庫]** 方塊中，選取 **[msdb]** 。  
  
5.  在 **[命令]** 方塊中，輸入下列陳述式建立一個附加檔案資料表，以上一個月份命名，包含前一步驟轉移訊息所對應的附件：  
  
    ```sql  
    DECLARE @LastMonth nvarchar(12);  
    DECLARE @CopyDate nvarchar(20) ;  
    DECLARE @CreateTable nvarchar(250) ;  
    SET @LastMonth = (SELECT CAST(DATEPART(yyyy,GETDATE()) AS CHAR(4)) + '_' + CAST(DATEPART(mm,GETDATE())-1 AS varchar(2))) ;  
    SET @CopyDate = (SELECT CAST(CONVERT(char(8), CURRENT_TIMESTAMP- DATEPART(dd,GETDATE()-1), 112) AS datetime))  
    SET @CreateTable = 'SELECT * INTO msdb.dbo.[DBMailArchive_Attachments_' + @LastMonth + '] FROM sysmail_attachments   
     WHERE mailitem_id in (SELECT DISTINCT mailitem_id FROM [DBMailArchive_' + @LastMonth + '] )';  
    EXEC sp_executesql @CreateTable ;  
    ```  
  
6.  按一下 **[確定]** 以儲存步驟。  
  
 [概觀](#Process_Overview)  
  
## <a name="to-create-a-step-to-archive-the-database-mail-log"></a>建立封存 Database Mail 記錄的步驟  
  
1.  在 **[步驟]** 頁面上，按一下 **[新增]** 。  
  
2.  在 **[步驟名稱]** 方塊中，輸入 **複製 Database Mail 記錄**。  
  
3.  在 **[類型]** 方塊中，選取 **[Transact-SQL 指令碼 (T-SQL)]** 。  
  
4.  在 **[資料庫]** 方塊中，選取 **[msdb]** 。  
  
5.  在 **[命令]** 方塊中，輸入下列陳述式建立一個記錄資料表，以上一個月份命名，包含前面步驟轉移訊息所對應的記錄項目：  
  
    ```sql  
    DECLARE @LastMonth nvarchar(12);  
    DECLARE @CopyDate nvarchar(20) ;  
    DECLARE @CreateTable nvarchar(250) ;  
    SET @LastMonth = (SELECT CAST(DATEPART(yyyy,GETDATE()) AS CHAR(4)) + '_' + CAST(DATEPART(mm,GETDATE())-1 AS varchar(2))) ;  
    SET @CopyDate = (SELECT CAST(CONVERT(char(8), CURRENT_TIMESTAMP- DATEPART(dd,GETDATE()-1), 112) AS datetime))  
    SET @CreateTable = 'SELECT * INTO msdb.dbo.[DBMailArchive_Log_' + @LastMonth + '] FROM sysmail_Event_Log   
     WHERE mailitem_id in (SELECT DISTINCT mailitem_id FROM [DBMailArchive_' + @LastMonth + '] )';  
    EXEC sp_executesql @CreateTable ;  
    ```  
  
6.  按一下 **[確定]** 以儲存步驟。  
  
 [概觀](#Process_Overview)  
  
## <a name="to-create-a-step-to-remove-the-archived-rows-from-database-mail"></a>建立從 Database Mail 移除封存資料列的步驟  
  
1.  在 **[步驟]** 頁面上，按一下 **[新增]** 。  
  
2.  在 **[步驟名稱]** 方塊中，輸入 **從 Database Mail 移除資料列**。  
  
3.  在 **[類型]** 方塊中，選取 **[Transact-SQL 指令碼 (T-SQL)]** 。  
  
4.  在 **[資料庫]** 方塊中，選取 **[msdb]** 。  
  
5.  在 **[命令]** 方塊中，輸入下列陳述式，從 Database Mail 資料表移除這個月之前的資料列：  
  
    ```sql  
    DECLARE @CopyDate nvarchar(20) ;  
    SET @CopyDate = (SELECT CAST(CONVERT(char(8), CURRENT_TIMESTAMP- DATEPART(dd,GETDATE()-1), 112) AS datetime)) ;  
    EXECUTE msdb.dbo.sysmail_delete_mailitems_sp @sent_before = @CopyDate ;  
    ```  
  
6.  按一下 **[確定]** 以儲存步驟。  
  
 [概觀](#Process_Overview)  
  
## <a name="to-create-a-step-to-remove-the-archived-items-from-database-mail-event-log"></a>建立從 Database Mail 事件記錄檔移除封存項目的步驟  
  
1.  在 **[步驟]** 頁面上，按一下 **[新增]** 。  
  
2.  在 **[步驟名稱]** 方塊中，輸入 **從 Database Mail 事件記錄檔移除資料列**。  
  
3.  在 **[類型]** 方塊中，選取 **[Transact-SQL 指令碼 (T-SQL)]** 。  
  
4.  在 **[命令]** 方塊中，輸入下列陳述式，從 Database Mail 事件記錄檔移除這個月之前的資料列：  
  
    ```sql  
    DECLARE @CopyDate nvarchar(20) ;  
    SET @CopyDate = (SELECT CAST(CONVERT(char(8), CURRENT_TIMESTAMP- DATEPART(dd,GETDATE()-1), 112) AS datetime)) ;  
    EXECUTE msdb.dbo.sysmail_delete_log_sp @logged_before = @CopyDate ;  
    ```  
  
5.  按一下 **[確定]** 以儲存步驟。  
  
 [概觀](#Process_Overview)  
  
## <a name="to-schedule-the-job-to-run-periodically"></a>排程定期執行作業  
  
1.  在 **[新增作業]** 對話方塊中，按一下 **[排程]** 。  
  
2.  在 **[排程]** 頁面上，按一下 **[新增]** 。  
  
3.  在 **[名稱]** 方塊中，輸入 **封存 Database Mail**。  
  
4.  在 **[排程類型]** 方塊中，選取 **[重複執行]** 。  
  
5.  在 **[頻率]** 區域中，選取定期執行作業的選項 (例如一個月一次)。  
  
6.  在 [每日頻率]  區域中，選取 [執行一次於 \<時間>]  。  
  
7.  視需要設定其他選項，然後按一下 **[確定]** 儲存排程。  
  
8.  按一下 **[確定]** 以儲存作業。  
  
 [概觀](#Process_Overview)  
  
  
