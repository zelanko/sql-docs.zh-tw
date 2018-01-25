---
title: "準備大量匯入資料 (SQL Server) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: import-export
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-bulk-import-export
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- bulk importing [SQL Server], about bulk importing
- BULK INSERT statement, guidelines
- BULK INSERT statement, restrictions
- bcp utility [SQL Server], guidelines
- bcp utility [SQL Server], restrictions
- hidden characters
- OPENROWSET function, BCP guidelines
ms.assetid: a82ef43c-d006-4c71-bfca-f001a3ba1ba0
caps.latest.revision: "34"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3f5c80e05dd49dc5d1280be66d98baf42deb02cc
ms.sourcegitcommit: 6c54e67818ec7b0a2e3c1f6e8aca0fdf65e6625f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/19/2018
---
# <a name="prepare-to-bulk-import-data-sql-server"></a>準備大量匯入資料 (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  您可以使用 **bcp** 命令、BULK INSERT 陳述式或 OPENROWSET(BULK) 函數，僅從資料檔案大量匯入資料。  
  
> [!NOTE]  
>  撰寫自訂應用程式來從物件 (而非文字檔) 大量匯入資料也是可行的。 若要從記憶體緩衝區大量匯入資料，請使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client (ODBC) 應用程式開發介面 (API) 或 OLE DB **IRowsetFastLoad** 介面的 bcp 延伸模組。  若要從 C# 資料表大量匯入資料，請使用 ADO.NET 大量複製 API **SqlBulkCopy**。  
  
> [!NOTE]  
>  不支援大量匯入資料到遠端資料表。  
  
 當您將資料檔案中的資料大量匯入到 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的執行個體時，請使用下列方針：  
  
-   為您的使用者帳戶取得必要的權限。  
  
     使用者帳戶，用來使用 **bcp** 公用程式、BULK INSERT 陳述式或 INSERT ...SELECT * FROM OPENROWSET(BULK...) 陳述式的使用者帳戶必須擁有資料表的必要權限 (由資料表擁有者指派)。 如需每個方法所需之權限的詳細資訊，請參閱 [bcp 公用程式](../../tools/bcp-utility.md)、[OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md) 和 [BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)。  
  
-   使用大量記錄復原模式。  
  
     這個指導方針適用於使用完整復原模式的資料庫。 大量記錄復原模式在對未編製索引的資料表 (「堆積」) 執行大量作業時很有用。 因為大量記錄復原不會執行記錄檔資料列插入的作業，所以使用大量記錄復原模式，將有助於防止因記錄交易而用盡空間的情形。 如需大量記錄復原模式的詳細資訊，請參閱[復原模式 &#40;SQL Server&#41;](../../relational-databases/backup-restore/recovery-models-sql-server.md)。  
  
     建議您在大量匯入作業之前，立即將資料庫變更為使用大量記錄復原模式。 事後則應立刻將資料庫重設成完整復原模式。 如需詳細資訊，請參閱[檢視或變更資料庫的復原模式 &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-or-change-the-recovery-model-of-a-database-sql-server.md)。  
  
    > [!NOTE]  
    >  如需如何在大量匯入作業期間盡量減少記錄的詳細資訊，請參閱[大量匯入採用最低限度記錄的必要條件](../../relational-databases/import-export/prerequisites-for-minimal-logging-in-bulk-import.md)。  
  
-   在大量匯入資料之後備份。  
  
     如果是使用簡單復原模式的資料庫，我們建議您在大量匯入作業完成之後進行完整或差異備份。 如需詳細資訊，請參閱[建立完整資料庫備份 &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md) 或[建立差異資料庫備份 &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-differential-database-backup-sql-server.md)。  
  
     如果是大量記錄復原模式或完整復原模式，記錄備份便已足夠。 如需詳細資訊，請參閱[交易記錄備份 &#40;SQL Server&#41;](../../relational-databases/backup-restore/transaction-log-backups-sql-server.md)。  
  
-   卸除資料表索引以改善大型大量匯入的效能。  
  
     這個指導方針的使用時機，是要匯入的資料量比資料表內的資料量多出很多時。 在此情況下，在執行大量匯入作業之前從資料表卸除索引可以大幅提高效能。  
  
    > [!NOTE]  
    >  但是，如果載入小量資料 (相較於已存在資料表中的資料量)，卸除索引可能會造成不良的後果。 重建索引需要的時間，可能會多於大量匯入作業所省下的時間。  
  
-   尋找並移除資料檔中的隱藏字元。  
  
     許多公用程式和文字編輯器會顯示隱藏字元，這些字元通常是在資料檔結尾。 大量匯入作業期間，ASCII 資料檔中的隱藏字元可能會產生問題，造成「發現非預期的 NULL」錯誤。 尋找並移除所有的隱藏字元，應該有助於防止這個問題的發生。  
  
## <a name="see-also"></a>另請參閱  
 [使用 bcp 公用程式匯入及匯出大量資料 &#40;SQL Server&#41;](../../relational-databases/import-export/import-and-export-bulk-data-by-using-the-bcp-utility-sql-server.md)   
 [使用 BULK INSERT 或 OPENROWSET&#40;BULK...&#41; 匯入大量資料 &#40;SQL Server&#41;](../../relational-databases/import-export/import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md)   
 [bcp 公用程式](../../tools/bcp-utility.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)   
 [大量匯入或大量匯出的資料格式 &#40;SQL Server&#41;](../../relational-databases/import-export/data-formats-for-bulk-import-or-bulk-export-sql-server.md)   
 [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)  
  
  
