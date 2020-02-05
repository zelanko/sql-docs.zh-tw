---
title: 部分備份 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- full backups [SQL Server]
- partial backups [SQL Server]
- READ_WRITE_FILEGROUPS option
- database backups [SQL Server], about backing up databases
ms.assetid: fe6b6bb1-38d0-46c4-bab8-31df14e8999c
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: a2c265d3a373eb53b822142fa2955d07b96b88f2
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/01/2020
ms.locfileid: "68033647"
---
# <a name="partial-backups-sql-server"></a>部分備份 (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 復原模式皆支援部分備份，因此本主題與所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫都有關。 但是，部分備份設計為在簡單復原模式下用以改善備份超大型資料庫 (其中包含一個或多個唯讀檔案群組) 時的彈性。  
  
 每當您想要排除唯讀檔案群組時，部分備份就十分有用。 *「部分備份」* (Partial backup) 與完整資料庫備份類似，但部分備份不包含所有檔案群組。 然而，若為讀寫資料庫，則部分備份包含主要檔案群組、每個讀寫檔案群組，以及 (選擇性地) 一個或多個唯讀檔案中的資料。 唯讀資料庫的部分備份只包含主要檔案群組。  
  
> [!NOTE]  
>  如果唯讀資料庫在部分備份之後變成可讀寫，可能有不在部分備份中的可讀寫次要檔案群組。 在此情況下，當您試圖進行差異部分備份時，備份會失敗。 您必須先進行另一個部分備份，才可以進行資料庫的差異部分備份。 新的部分備份會包含每個讀取/寫入次要檔案群組，並且可作為差異部分備份的基底。  
  
 唯讀檔案群組的檔案備份可以結合部分備份。 如需檔案備份的相關資訊，請參閱[完整檔案備份 &#40;SQL Server&#41;](../../relational-databases/backup-restore/full-file-backups-sql-server.md)。  
  
 部分備份可以當成差異部分備份的 *「差異基底」* (Differential base)。 如需詳細資訊，請參閱 [差異備份 &#40;SQL Server&#41;](../../relational-databases/backup-restore/differential-backups-sql-server.md)。  
  
##  <a name="RelatedTasks"></a> 相關工作  
  
> [!NOTE]  
>  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或 [維護計畫精靈] 不支援部分備份。  
  
 **建立部分備份**  
  
-   [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md) (READ_WRITE_FILEGROUPS; FILEGROUP 選項，如有需要)  
  
 **在還原順序中使用部分備份**  
  
-   [範例：分次還原資料庫 &#40;簡單復原模式&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-database-simple-recovery-model.md)  
  
-   [範例：僅限於部分檔案群組的分次還原 &#40;簡單復原模式&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-only-some-filegroups-simple-recovery-model.md)  
  
## <a name="see-also"></a>另請參閱  
 [備份概觀 &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-overview-sql-server.md)   
 [檔案還原 &#40;簡單復原模式&#41;](../../relational-databases/backup-restore/file-restores-simple-recovery-model.md)   
 [分次還原 &#40;SQL Server&#41;](../../relational-databases/backup-restore/piecemeal-restores-sql-server.md)  
  
  
