---
title: 檢視備份磁帶或檔案的內容 (SQL Server) | Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- backup devices [SQL Server], tapes
- displaying backup content
- viewing backup content
- tape backup devices, viewing contents
- database backups [SQL Server], viewing content
- backing up databases [SQL Server], viewing content
ms.assetid: cd6674a2-ca55-4b5a-a971-878ba001821e
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: cbfe09a2d8110a98885686e078146cfccc305c51
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48051524"
---
# <a name="view-the-contents-of-a-backup-tape-or-file-sql-server"></a>檢視備份磁帶或檔案的內容 (SQL Server)
  此主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中檢視備份磁帶或檔案的內容。  
  
> [!NOTE]  
>  未來的 SQL Server 版本中將會移除磁帶備份裝置的支援。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [Security](#Security)  
  
-   **若要使用下列項目檢視備份磁帶或檔案的內容：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Security"></a> 安全性  
 如需安全性的相關資訊，請參閱 [RESTORE HEADERONLY &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-headeronly-transact-sql)。  
  
####  <a name="Permissions"></a> Permissions  
 在 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 及更新版本中，取得有關備份組或備份裝置的資訊需要 CREATE DATABASE 權限。 如需詳細資訊，請參閱 [GRANT 資料庫權限 &#40;Transact-SQL&#41;](/sql/t-sql/statements/grant-database-permissions-transact-sql)。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-view-the-content-of-a-backup-tape-or-file"></a>檢視備份磁帶或檔案的內容  
  
1.  連接到適當的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]執行個體之後，在 [物件總管] 中按一下伺服器名稱展開伺服器樹狀目錄。  
  
2.  展開 **[資料庫]**，然後視資料庫而定，選取使用者資料庫，或者展開 **[系統資料庫]** 並選取一個系統資料庫。  
  
3.  以滑鼠右鍵按一下要備份的資料庫，指向 [工作]，然後按一下 [備份]。 會出現 **[備份資料庫]** 對話方塊。  
  
4.  在 **[一般]** 頁面的 **[目的地]** 區段中，按一下 **[磁碟]** 或 **[磁帶]**。 在 **[備份至]** 清單方塊中，找出您要的磁碟檔案或磁帶。  
  
     如果清單方塊中未顯示磁碟檔案或磁帶，按一下 [新增]。 選取檔案名稱或磁帶機。 按一下 [確定]，將其加入 [備份至] 清單方塊。  
  
5.  在 [備份至] 清單方塊中，選取您要檢視的磁碟或磁帶機路徑，然後按一下 [內容]。 這會開啟 **[裝置內容]** 對話方塊。  
  
6.  右窗格會針對所選取的磁帶或檔案，顯示其媒體集與備份組的詳細資訊。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-view-the-content-of-a-backup-tape-or-file"></a>檢視備份磁帶或檔案的內容  
  
1.  連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在標準列中，按一下 **[新增查詢]**。  
  
3.  使用 [RESTORE HEADERONLY](/sql/t-sql/statements/restore-statements-headeronly-transact-sql) 陳述式。 此範例會傳回 `AdventureWorks2012-FullBackup.bak`檔案的相關資訊。  
  
```tsql  
USE AdventureWorks2012;  
RESTORE HEADERONLY   
FROM DISK = N'C:\AdventureWorks2012-FullBackup.bak' ;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [backupfilegroup &#40;Transact-SQL&#41;](/sql/relational-databases/system-tables/backupfilegroup-transact-sql)   
 [backupfile &#40;Transact-SQL&#41;](/sql/relational-databases/system-tables/backupfile-transact-sql)   
 [backupset &#40;Transact-SQL&#41;](/sql/relational-databases/system-tables/backupset-transact-sql)   
 [backupmediaset &#40;Transact-SQL&#41;](/sql/relational-databases/system-tables/backupmediaset-transact-sql)   
 [backupmediafamily &#40;Transact-SQL&#41;](/sql/relational-databases/system-tables/backupmediafamily-transact-sql)   
 [備份裝置 &#40;SQL Server&#41;](backup-devices-sql-server.md)   
 [定義磁碟檔案的邏輯備份裝置 &#40;SQL Server&#41;](define-a-logical-backup-device-for-a-disk-file-sql-server.md)   
 [定義磁帶機的邏輯備份裝置 &#40;SQL Server&#41;](define-a-logical-backup-device-for-a-tape-drive-sql-server.md)  
  
  
