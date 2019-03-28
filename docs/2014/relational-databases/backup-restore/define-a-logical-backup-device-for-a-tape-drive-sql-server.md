---
title: 定義磁帶機的邏輯備份裝置 (SQL Server) | Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- backup devices [SQL Server], defining
- backup devices [SQL Server], tapes
- backing up databases [SQL Server], tapes
- database backups [SQL Server], tapes
- tape backup devices, creating
ms.assetid: 66f36e1d-0287-4fac-8a51-71f9f0d7ad5b
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 14a96a44967c41b185d3196c9d6577f67547e77a
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/27/2019
ms.locfileid: "58537410"
---
# <a name="define-a-logical-backup-device-for-a-tape-drive-sql-server"></a>定義磁帶機的邏輯備份裝置 (SQL Server)
  此主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中定義磁帶機的邏輯備份裝置。 邏輯裝置是使用者定義名稱，指向特定的實體備份裝置 (磁碟檔案或磁帶機)。  當備份寫入備份裝置後，才會進行實體裝置的初始化。  
  
> [!NOTE]  
>  未來的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]版本中將會移除磁帶備份裝置的支援。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
     [Security](#Security)  
  
-   **若要使用下列項目定義磁帶機的邏輯備份裝置：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Restrictions"></a> 限制事項  
  
-   磁帶機必須受到 Microsoft Windows 作業系統支援。  
  
-   磁帶裝置必須在實體上連接至執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體的電腦。 不支援備份至遠端磁帶裝置。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> 權限  
 需要 **diskadmin** 固定伺服器角色的成員資格。  
  
 需要寫入磁碟的權限。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-define-a-logical-backup-device-for-a-tape-drive"></a>定義磁帶機的邏輯備份裝置  
  
1.  連接到適當的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]執行個體之後，在 [物件總管] 中按一下伺服器名稱展開伺服器樹狀目錄。  
  
2.  展開 [伺服器物件]，然後以滑鼠右鍵按一下 [備份裝置]。  
  
3.  按一下 **[新增備份裝置]**，開啟 **[備份裝置]** 對話方塊。  
  
4.  輸入裝置名稱。  
  
5.  在目的地中，請按一下 **[磁帶]** ，選取尚未與其他備份裝置連接的磁帶機。 如果沒有這樣的磁帶機可用， **[磁帶]** 選項會停用。  
  
6.  若要定義新裝置，請按一下 **[確定]**。  
  
 若要備份至這個新裝置，請將它加入 [備份資料庫] ([一般]) 對話方塊中的 [備份至:] 欄位。 如需詳細資訊，請參閱 [建立完整資料庫備份 &#40;SQL Server&#41;](create-a-full-database-backup-sql-server.md)中建立差異資料庫備份。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-define-a-logical-backup-device-for-a-tape-drive"></a>定義磁帶機的邏輯備份裝置  
  
1.  連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在標準列中，按一下 **[新增查詢]**。  
  
3.  複製下列範例並將其貼到查詢視窗中，然後按一下 **[執行]**。 這個範例示範如何使用 [sp_addumpdevice](/sql/relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql) ，定義磁帶的邏輯備份裝置。 範例會加入名稱為 `tapedump1`的磁帶備份裝置，實體名稱是 `\\.\tape0`。  
  
```sql  
USE AdventureWorks2012 ;  
GO  
EXEC sp_addumpdevice 'tape', 'tapedump1', '\\.\tape0' ;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)   
 [sys.backup_devices &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-backup-devices-transact-sql)   
 [sp_addumpdevice &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql)   
 [sp_dropdevice &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-dropdevice-transact-sql)   
 [備份裝置 &#40;SQL Server&#41;](backup-devices-sql-server.md)   
 [定義磁碟檔案的邏輯備份裝置 &#40;SQL Server&#41;](define-a-logical-backup-device-for-a-disk-file-sql-server.md)   
 [檢視邏輯備份裝置的屬性和內容 &#40;SQL Server&#41;](view-the-properties-and-contents-of-a-logical-backup-device-sql-server.md)  
  
  
