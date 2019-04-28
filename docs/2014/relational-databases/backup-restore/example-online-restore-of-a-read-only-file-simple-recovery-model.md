---
title: 範例線上還原唯讀檔案 （簡單復原模式） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- restore sequences [SQL Server], online
- online restores [SQL Server], simple recovery model
- simple recovery model [SQL Server], RESTORE examples
ms.assetid: 0c691fc6-9865-46a7-b055-8097424492d6
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: ccbb89a7af71545c3b410356b6ab6b101983798d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62876148"
---
# <a name="example-online-restore-of-a-read-only-file-simple-recovery-model"></a>範例線上還原讀取/寫入檔案 (簡單復原模式)
  本主題是關於在簡單復原模式下，包含唯讀檔案群組的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫。 在簡單復原模式下，如果有檔案成為唯讀後保留的備份檔案，就可以線上還原唯讀檔案。  
  
 在此範例中，名為 `adb` 的資料庫包含三個檔案群組。 檔案群組 `A` 可讀取/寫入，而檔案群組 `B` 和 `C` 則是唯讀的。 所有的檔案群組一開始都是在線上。 在檔案群組 `B`中，必須還原的是唯讀檔案 `b1`。 資料庫管理員可以使用在檔案成為唯讀後保留的備份進行還原。 檔案群組 `B` 在還原期間會處於離線，但資料庫的其他檔案群組仍會維持線上工作。  
  
## <a name="restore-sequence"></a>還原順序  
  
> [!NOTE]  
>  線上還原順序的語法和離線還原順序的語法相同。  
  
 為還原檔案，資料庫管理員會使用下列還原順序：  
  
```  
RESTORE DATABASE adb FILE='b1' FROM filegroup_B_backup   
WITH RECOVERY  
```  
  
 檔案現在已經在線上。  
  
## <a name="additional-examples"></a>其他範例  
  
-   [範例：分次還原資料庫 &#40;簡單復原模式&#41;](example-piecemeal-restore-of-database-simple-recovery-model.md)  
  
-   [範例：僅限於部分檔案群組的分次還原 &#40;簡單復原模式&#41;](example-piecemeal-restore-of-only-some-filegroups-simple-recovery-model.md)  
  
-   [範例：分次還原資料庫 &#40;完整復原模式&#41;](example-piecemeal-restore-of-database-full-recovery-model.md)  
  
-   [範例：僅限於部分檔案群組的分次還原 &#40;完整復原模式&#41;](example-piecemeal-restore-of-only-some-filegroups-full-recovery-model.md)  
  
-   [範例：線上還原讀取/寫入檔案 &#40;完整復原模式&#41;](example-online-restore-of-a-read-write-file-full-recovery-model.md)  
  
-   [範例：線上還原唯讀檔案 &#40;完整復原模式&#41;](example-online-restore-of-a-read-only-file-full-recovery-model.md)  
  
## <a name="see-also"></a>另請參閱  
 [線上還原 &#40;SQL Server&#41;](online-restore-sql-server.md)   
 [分次還原 &#40;SQL Server&#41;](piecemeal-restores-sql-server.md)   
 [檔案還原 &#40;簡單復原模式&#41;](file-restores-simple-recovery-model.md)   
 [還原和復原概觀 &#40;SQL Server&#41;](restore-and-recovery-overview-sql-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)  
  
  
