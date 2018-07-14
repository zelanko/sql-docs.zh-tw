---
title: 重新啟動中斷的還原作業 (Transact-SQL) | Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: backup-restore
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- interrupted restore operation
- restoring databases [SQL Server], restarting interrupted operation
- resetting options changed after backup
- database restores [SQL Server], restarting interrupted operation
- restarting interrupted restore operation
- restoring interrupted operation [SQL Server]
ms.assetid: 6413a07d-fd90-448d-8f29-12c5a1972618
caps.latest.revision: 21
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 872e3b59ccb8d3ae01957cf67ac1d7c368916613
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37178115"
---
# <a name="restart-an-interrupted-restore-operation-transact-sql"></a>重新啟動中斷的還原作業 (Transact-SQL)
  此主題說明如何重新啟動被中斷的還原作業。  
  
### <a name="to-restart-an-interrupted-restore-operation"></a>若要重新啟動被中斷的還原作業  
  
1.  再執行一次被中斷的 RESTORE 陳述式，並指定下列項目：  
  
    -   與原始 RESTORE 陳述式相同的子句。  
  
    -   RESTART 子句。  
  
## <a name="example"></a>範例  
 此範例會重新啟動被中斷的還原作業。  
  
```tsql  
-- Restore a full database backup of the AdventureWorks database.  
RESTORE DATABASE AdventureWorks  
   FROM DISK = 'C:\AdventureWorks.bck'  
GO  
-- The restore operation halted prematurely.  
-- Repeat the original RESTORE statement specifying WITH RESTART.  
RESTORE DATABASE AdventureWorks   
   FROM DISK = 'C:\AdventureWorks.bck'  
   WITH RESTART  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [完整資料庫還原 &#40;完整復原模式&#41;](complete-database-restores-full-recovery-model.md)   
 [完整資料庫還原 &#40;簡單復原模式&#41;](complete-database-restores-simple-recovery-model.md)   
 [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)  
  
  
