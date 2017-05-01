---
title: "檢視邏輯備份裝置的屬性和內容 (SQL Server) | Microsoft 文件"
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- displaying backup content
- viewing backup content
- database backups [SQL Server], viewing content
- backing up databases [SQL Server], viewing content
- backing up databases [SQL Server], properties
- displaying backup properties
- backup devices [SQL Server], viewing information
- viewing backup properties
- database backups [SQL Server], properties
ms.assetid: 3a309074-e816-454d-b6c3-fcfdde0cbf74
caps.latest.revision: 22
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 1e0a3fad1cc54f9367d95ac36c903deeede0814b
ms.lasthandoff: 04/11/2017

---
# <a name="view-the-properties-and-contents-of-a-logical-backup-device-sql-server"></a>檢視邏輯備份裝置的屬性和內容 (SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  此主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中檢視邏輯備份裝置的屬性和內容。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [安全性](#Security)  
  
-   **若要使用下列項目檢視邏輯備份裝置的屬性和內容：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Security"></a> 安全性  
 如需安全性的相關資訊，請參閱 [RESTORE LABELONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-labelonly-transact-sql.md)。  
  
####  <a name="Permissions"></a> Permissions  
 在 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 及更新版本中，取得有關備份組或備份裝置的資訊需要 CREATE DATABASE 權限。 如需詳細資訊，請參閱 [GRANT 資料庫權限 &#40;Transact-SQL&#41;](../../t-sql/statements/grant-database-permissions-transact-sql.md)。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-view-the-properties-and-contents-of-a-logical-backup-device"></a>若要檢視邏輯備份裝置的屬性和內容  
  
1.  連接到適當的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]執行個體之後，在 [物件總管] 中按一下伺服器名稱展開伺服器樹狀目錄。  
  
2.  展開 **[伺服器物件]**，然後展開 **[備份裝置]**。  
  
3.  按一下裝置，然後以滑鼠右鍵按一下 [屬性]，這時會開啟 [備份裝置] 對話方塊。  
  
4.  **[一般]** 頁面會顯示裝置名稱和目的地 (可能是磁帶裝置或檔案路徑)。  
  
5.  在 **[選取頁面]** 窗格中，按一下 **[媒體內容]**。  
  
6.  右窗格會顯示在下列屬性面板中：  
  
    -   **媒體**  
  
         媒體順序資訊 (如果有的話，則為媒體序號、家族序號及鏡像識別碼) 及媒體建立的日期和時間。  
  
    -   **媒體集**  
  
         媒體集資訊：媒體集名稱和描述 (如果有的話)，以及媒體集的家族數目。  
  
7.  **[備份組]** 方格會顯示媒體集內容的相關資訊。  
  
> [!NOTE]  
>  如需詳細資訊，請參閱 [媒體內容頁面](../../relational-databases/backup-restore/backup-device-media-contents-page.md)。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-view-the-properties-and-contents-of-a-logical-backup-device"></a>若要檢視邏輯備份裝置的屬性和內容  
  
1.  連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在標準列中，按一下 **[新增查詢]**。  
  
3.  使用 [RESTORE LABELONLY](../../t-sql/statements/restore-statements-labelonly-transact-sql.md) 陳述式。 此範例會傳回 `AdvWrks2008R2Backup` 邏輯備份裝置的資訊。  
  
```tsql  
USE AdventureWorks2012 ;  
RESTORE LABELONLY  
   FROM AdvWrks2008R2Backup ;  
GO  
  
```  
  
## <a name="see-also"></a>另請參閱  
 [backupfilegroup &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupfilegroup-transact-sql.md)   
 [backupfile &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupfile-transact-sql.md)   
 [backupset &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupset-transact-sql.md)   
 [backupmediaset &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupmediaset-transact-sql.md)   
 [backupmediafamily &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupmediafamily-transact-sql.md)   
 [sp_addumpdevice &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql.md)   
 [備份裝置 &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md)  
  
  
