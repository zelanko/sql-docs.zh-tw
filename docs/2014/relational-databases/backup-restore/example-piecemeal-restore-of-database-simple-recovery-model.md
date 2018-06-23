---
title: 範例：分次還原資料庫 (簡單復原模式) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- piecemeal restores [SQL Server], simple recovery model
- restore sequences [SQL Server], piecemeal
- simple recovery model [SQL Server], RESTORE examples
ms.assetid: 9834b14a-4e56-4654-b190-c2a38624b6b4
caps.latest.revision: 26
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 5725d193db83cb2648d1676cf99662af65a543d2
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36134968"
---
# <a name="example-piecemeal-restore-of-database-simple-recovery-model"></a>範例：分次還原資料庫 (簡單復原模式)
  分次還原順序會在檔案群組層級，分階段地還原與復原資料庫，先從主要檔案群組開始，然後才是所有的讀取/寫入次要檔案群組。  
  
 在此範例中，資料庫 `adb` 是在損毀之後還原至新的電腦。 此資料庫使用的是簡單復原模式。 在損毀之前，所有檔案群組都在線上。 檔案群組 `A` 和 `C` 可讀取/寫入，而檔案群組 `B` 則是唯讀的。 檔案群組 `B` 在最近一次部分備份之前變成唯讀，該部分備份包含主要檔案群組以及讀取/寫入次要檔案群組 `A` 和 `C`。 在檔案群組 `B` 變成唯讀之後，對檔案群組 `B` 進行了個別的檔案備份。  
  
## <a name="restore-sequences"></a>還原順序  
  
1.  主要檔案群組和檔案群組 `A` 和 `C`的部分還原。  
  
    ```  
    RESTORE DATABASE adb FILEGROUP='A',FILEGROUP='C'   
       FROM partial_backup   
       WITH PARTIAL, RECOVERY;  
  
    ```  
  
     此時，主要檔案群組和檔案群組 `A` 和 `C` 在線上。 檔案群組 `B` 中的所有檔案皆為復原暫止狀態，且檔案群組已離線。  
  
2.  線上還原檔案群組 `B`。  
  
    ```  
    RESTORE DATABASE adb FILEGROUP='B' FROM backup WITH RECOVERY;  
  
    ```  
  
     所有檔案群組現在都已在線上。  
  
## <a name="additional-examples"></a>其他範例  
  
-   [範例：僅限於部分檔案群組的分次還原 &#40;簡單復原模式&#41;](example-piecemeal-restore-of-only-some-filegroups-simple-recovery-model.md)  
  
-   [範例：線上還原唯讀檔案 &#40;簡單復原模式&#41;](example-online-restore-of-a-read-only-file-simple-recovery-model.md)  
  
-   [範例：分次還原資料庫 &#40;完整復原模式&#41;](example-piecemeal-restore-of-database-full-recovery-model.md)  
  
-   [範例：僅限於部分檔案群組的分次還原 &#40;完整復原模式&#41;](example-piecemeal-restore-of-only-some-filegroups-full-recovery-model.md)  
  
-   [範例：線上還原讀寫檔案 &#40;完整復原模式&#41;](example-online-restore-of-a-read-write-file-full-recovery-model.md)  
  
-   [範例：線上還原唯讀檔案 &#40;完整復原模式&#41;](example-online-restore-of-a-read-only-file-full-recovery-model.md)  
  
## <a name="see-also"></a>另請參閱  
 [線上還原 &#40;SQL Server&#41;](online-restore-sql-server.md)   
 [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)   
 [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)   
 [分次還原 &#40;SQL Server&#41;](piecemeal-restores-sql-server.md)  
  
  
