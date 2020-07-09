---
title: 刪除備份裝置 (SQL Server) | Microsoft 文件
description: 本文說明如何使用 SQL Server Management Studio 或 Transact-SQL，在 SQL Server 中刪除備份裝置。
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- database backups [SQL Server], deleting devices
- backup devices [SQL Server], deleting
- deleting backup devices
- removing backup devices
- backing up databases [SQL Server], backup devices
ms.assetid: 7be62480-ed6a-4262-a071-1feba73b1c02
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 50f92b7fcc6e15e8866ba50ad3ecc85ec617826d
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85748115"
---
# <a name="delete-a-backup-device-sql-server"></a>刪除備份裝置 (SQL Server)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  此主題描述如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 來刪除 [!INCLUDE[tsql](../../includes/tsql-md.md)]中的備份裝置。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [安全性](#Security)  
  
-   **若要使用下列項目刪除備份裝置：**  
  
     [Transact-SQL](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="security"></a><a name="Security"></a> Security  
  
####  <a name="permissions"></a><a name="Permissions"></a> 權限  
 需要 **diskadmin** 固定伺服器角色的成員資格。  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-delete-a-backup-device"></a>刪除備份裝置  
  
1.  連接到適當的 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]執行個體之後，請在 [物件總管] 中按一下伺服器名稱以展開伺服器樹狀目錄。  
  
2.  展開 **[伺服器物件]** ，然後展開 **[備份裝置]** 。  
  
3.  以滑鼠右鍵按一下所要的裝置，然後按一下 [刪除]  。  
  
4.  在 **[刪除物件]** 對話方塊，確認 **[物件名稱]** 資料行中所顯示的裝置名稱是正確的。  
  
5.  按一下 [確定]  。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-delete-a-backup-device"></a>刪除備份裝置  
  
1.  連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在標準列中，按一下 **[新增查詢]** 。  
  
3.  複製下列範例並貼入查詢中。 此範例示範如何使用 [sp_dropdevice](../../relational-databases/system-stored-procedures/sp-dropdevice-transact-sql.md) 刪除備份裝置。 執行第一個範例，建立 `mybackupdisk` 備份裝置和實體名稱 `c:\backup\backup1.bak`。 執行 **sp_dropdevice** 刪除 `mybackupdisk` 備份裝置。 `delfile` 參數會刪除實體名稱。  
  
```sql  
--Define a backup device and physical name.   
USE AdventureWorks2012 ;  
GO  
EXEC sp_addumpdevice 'disk', 'mybackupdisk', 'c:\backup\backup1.bak' ;  
GO  
--Delete the backup device and the physical name.  
USE AdventureWorks2012 ;  
GO  
EXEC sp_dropdevice ' mybackupdisk ', 'delfile' ;  
GO  
  
```  
  
## <a name="see-also"></a>另請參閱  
 [檢視邏輯備份裝置的屬性和內容 &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-the-properties-and-contents-of-a-logical-backup-device-sql-server.md)   
 [sys.backup_devices &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-backup-devices-transact-sql.md)   
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [備份裝置 &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md)   
 [sp_addumpdevice &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql.md)  
  
  
