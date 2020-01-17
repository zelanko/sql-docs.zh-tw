---
title: 還原資料庫：簡單復原模式 (Transact-SQL)
ms.custom: seo-lt-2019
ms.date: 12/17/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- full backups [SQL Server]
- database restores [SQL Server], full backups
- backing up databases [SQL Server], full backups
- database backups [SQL Server], full backups
- restoring databases [SQL Server], full backups
ms.assetid: a928fa36-e285-476f-9a7b-6840a8bb7283
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 835f5c6a4571359f750862d3487817a7e11f6503
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/19/2019
ms.locfileid: "75244231"
---
# <a name="restore-a-database-backup-under-the-simple-recovery-model-transact-sql"></a>在簡單復原模式下還原資料庫備份 (Transact-SQL)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  本主題說明如何還原完整資料庫備份。  
  
> [!IMPORTANT]  
>  負責還原完整資料庫備份的系統管理員，必須是目前唯一正在使用即將還原之資料庫的人員。  
  
## <a name="prerequisites-and-recommendations"></a>先決條件和建議  
  
-   若要還原加密的資料庫，您必須能夠存取之前用來加密資料庫的憑證或非對稱金鑰。 如果沒有該憑證或非對稱金鑰，就無法還原資料庫。 因此，只要需要備份，就必須保留用來加密資料庫加密金鑰的憑證。 如需詳細資訊，請參閱 [SQL Server Certificates and Asymmetric Keys](../../relational-databases/security/sql-server-certificates-and-asymmetric-keys.md)。  
  
-   基於安全性的理由，建議您不要附加或還原來源不明或來源不受信任的資料庫。 這種資料庫可能包含惡意程式碼，因此可能執行非預期的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 程式碼，或是修改結構描述或實體資料庫結構而造成錯誤。 使用來源不明或來源不受信任的資料庫之前，請先在非實際執行伺服器的資料庫上執行 [DBCC CHECKDB](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md) ，同時檢查資料庫中的程式碼，例如預存程序或其他使用者定義程式碼。  
  
## <a name="database-compatibility-level-after-upgrade"></a>升級後的資料庫相容性層級  
 **tempdb**、 **模型**、 **msdb** 和 **資源** 資料庫的相容性層級在升級之後會設定為 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 的相容性層級。 **主要** 系統資料庫會保留升級前的相容性層級，除非層級小於 100。 如果升級前 **主要** 的相容性層級小於 100，升級後會設定為 100。  
  
 如果使用者資料庫的相容性層級在升級前為 100 或更高層級，則在升級後仍會保持相同。 如果升級前的相容性層級為 90，則在升級後的資料庫中，相容性層級會設定為 100 (這是 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]所支援的最低相容性層級)。  
  
> [!NOTE]  
>  新的使用者資料庫會繼承 **模型** 資料庫的相容性層級。  
  
## <a name="procedures"></a>程序  
  
#### <a name="to-restore-a-full-database-backup"></a>還原完整資料庫備份  
  
1.  執行 RESTORE DATABASE 陳述式以還原完整資料庫備份，請指定：  
  
    -   所要還原的資料庫名稱。  
  
    -   將要還原完整資料庫備份的備份裝置。  
  
    -   如果完整資料庫備份還原以後需要套用交易記錄或差異資料庫備份，則請指定 NORECOVERY 子句。  
  
    > [!IMPORTANT]  
    >  若要還原加密的資料庫，您必須能夠存取之前用來加密資料庫的憑證或非對稱金鑰。 如果沒有該憑證或非對稱金鑰，就無法還原資料庫。 因此，只要需要備份，就必須保留用來加密資料庫加密金鑰的憑證。 如需詳細資訊，請參閱 [SQL Server Certificates and Asymmetric Keys](../../relational-databases/security/sql-server-certificates-and-asymmetric-keys.md)。  
  
2.  (選擇性) 指定：  
  
    -   識別備份裝置上欲還原之備份組的 FILE 子句。  
  
> [!NOTE]  
>  如果您將舊版資料庫還原至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]，資料庫會自動升級。 通常，資料庫立即變為可用。 不過，如果 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 資料庫具有全文檢索索引，升級程序就會根據  **upgrade_option** 伺服器屬性的設定，匯入、重設或重建這些索引。 如果升級選項設定為匯入 (**upgrade_option** = 2) 或重建 (**upgrade_option** = 0)，則全文檢索索引在升級期間將無法使用。 根據進行索引的資料數量而定，匯入可能需要數個小時，而重建可能需要十倍以上的時間。 此外，請注意，當升級選項設定為 [匯入] 時，如果全文檢索目錄無法使用，系統就會重建相關聯的全文檢索索引。 若要變更 **upgrade_option** 伺服器屬性的設定，請使用 [sp_fulltext_service](../../relational-databases/system-stored-procedures/sp-fulltext-service-transact-sql.md)。  
  
## <a name="example"></a>範例  
  
### <a name="description"></a>描述  
 此範例會從磁帶還原 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 完整資料庫備份。  
  
### <a name="example"></a>範例  
  
```  
USE master;  
GO  
RESTORE DATABASE AdventureWorks2012  
   FROM TAPE = '\\.\Tape0';  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [完整資料庫還原 &#40;完整復原模式&#41;](../../relational-databases/backup-restore/complete-database-restores-full-recovery-model.md)   
 [完整資料庫還原 &#40;簡單復原模式&#41;](../../relational-databases/backup-restore/complete-database-restores-simple-recovery-model.md)   
 [完整資料庫備份 &#40;SQL Server&#41;](../../relational-databases/backup-restore/full-database-backups-sql-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [備份記錄與標頭資訊 &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-history-and-header-information-sql-server.md)   
 [重建系統資料庫](../../relational-databases/databases/rebuild-system-databases.md)  
  
  
