---
title: 定義邏輯備份裝置 - 磁碟
description: 本文說明如何使用 SQL Server Management Studio 或 Transact-SQL，在 SQL Server 中定義磁碟檔案的邏輯備份裝置。
ms.custom: seo-lt-2019
ms.date: 12/17/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- backup devices [SQL Server], defining
- backup devices [SQL Server], disks
- disk backup devices [SQL Server]
- database backups [SQL Server], disks
- backing up databases [SQL Server], disks
ms.assetid: 86331d43-c738-4523-ae3d-7d6700348ed1
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 4f2e54b5d8873e34eaff65fd6f9ec6a86feb32c3
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85748251"
---
# <a name="define-a-logical-backup-device-for-a-disk-file-sql-server"></a>定義磁碟檔案的邏輯備份裝置 (SQL Server)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  此主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中定義磁碟檔案的邏輯備份裝置。 邏輯裝置是使用者定義名稱，指向特定的實體備份裝置 (磁碟檔案或磁帶機)。  當備份寫入備份裝置後，才會進行實體裝置的初始化。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
     [建議](#Recommendations)  
  
     [安全性](#Security)  
  
-   **若要使用下列項目定義磁碟檔案的邏輯備份裝置：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 限制事項  
  
-   邏輯裝置名稱在伺服器執行個體上所有邏輯備份裝置中都必須是唯一的。 若要檢視現有的邏輯裝置名稱，請查詢 [sys.backup_devices](../../relational-databases/system-catalog-views/sys-backup-devices-transact-sql.md) 目錄檢視。  
  
###  <a name="recommendations"></a><a name="Recommendations"></a> 建議  
  
-   我們建議備份磁碟應該與資料庫資料和記錄磁碟使用不同的磁碟。 為了確保您可以在資料或記錄磁碟故障時存取備份，這樣做有其必要。  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 權限  
 需要 **diskadmin** 固定伺服器角色的成員資格。  
  
 需要寫入磁碟的權限。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-define-a-logical-backup-device-for-a-disk-file"></a>定義磁碟檔案的邏輯備份裝置  
  
1.  連線到適當的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 執行個體之後，在物件總管中按一下伺服器名稱，以展開伺服器樹狀目錄。  
  
2.  展開 [伺服器物件]  ，然後以滑鼠右鍵按一下 [備份裝置]  。  
  
3.  按一下 **[新增備份裝置]** 。 會開啟 **[備份裝置]** 對話方塊。  
  
4.  輸入裝置名稱。  
  
5.  若要指定目的地，請按一下 **[檔案]** 並指定檔案的完整路徑。  
  
6.  若要定義新裝置，請按一下 **[確定]** 。  
  
 若要備份至這個新裝置，請將它加入 [備份資料庫]  \([一般]  ) 對話方塊中的 [備份至:]  欄位。 如需詳細資訊，請參閱 [建立完整資料庫備份 &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)中建立差異資料庫備份。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-define-a-logical-backup-for-a-disk-file"></a>定義磁碟檔案的邏輯備份裝置  
  
1.  連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在標準列中，按一下 **[新增查詢]** 。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]** 。 這個範例示範如何使用 [sp_addumpdevice](../../relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql.md) ，定義磁碟檔案的邏輯備份裝置。 範例會加入名稱為 `mydiskdump`的磁碟備份裝置，實體名稱是 `c:\dump\dump1.bak`。  
  
```sql  
USE AdventureWorks2012 ;  
GO  
EXEC sp_addumpdevice 'disk', 'mydiskdump', 'c:\dump\dump1.bak' ;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [備份裝置 &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md)   
 [sys.backup_devices &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-backup-devices-transact-sql.md)   
 [sp_addumpdevice &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql.md)   
 [sp_dropdevice &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropdevice-transact-sql.md)   
 [定義磁帶機的邏輯備份裝置 &#40;SQL Server&#41;](../../relational-databases/backup-restore/define-a-logical-backup-device-for-a-tape-drive-sql-server.md)   
 [檢視邏輯備份裝置的屬性和內容 &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-the-properties-and-contents-of-a-logical-backup-device-sql-server.md)  
  
  
