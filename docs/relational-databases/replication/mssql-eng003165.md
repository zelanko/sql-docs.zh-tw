---
title: MSSQL_ENG003165 | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- MSSQL_ENG003165 error
ms.assetid: 707d33dd-644e-4cc9-ac51-dddd49031530
caps.latest.revision: 15
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 7edb7577c4f51c5aed9e9643fa670598db4c5a43
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="mssqleng003165"></a>MSSQL_ENG003165
    
## <a name="message-details"></a>訊息詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|3165|  
|事件來源|MSSQLSERVER|  
|元件|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|符號名稱||  
|訊息文字|資料庫 '%ls' 已還原，不過在還原/移除複寫時遇到錯誤。 資料庫已保持離線。 請參閱《SQL Server 線上叢書》中的主題＜MSSQL_ENG003165＞。|  
  
## <a name="explanation"></a>說明  
 如果在還原複寫資料庫的備份時出現錯誤，將引發此錯誤：  
  
-   如果將備份還原至執行備份的資料庫和伺服器，此錯誤表示複寫設定無法正確還原。  
  
-   如果將備份還原至不同的資料庫或伺服器，此錯誤表示複寫設定無法正確移除 (依預設，如果資料庫或伺服器不同，將移除複寫設定)。  
  
 此錯誤可能是由於，還原的資料庫與包含複寫中繼資料的一個或多個系統資料庫 ( **msdb**、 **master**或散發資料庫) 之間狀態不符而導致。  
  
## <a name="user-action"></a>使用者動作  
 若要解決此問題：  
  
1.  請執行 ALTER DATABASE 以使資料庫連線；例如： `ALTER DATABASE AdventureWorks SET ONLINE`。 如需詳細資訊，請參閱 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)。 如果您要保留複寫設定，請移至步驟 2。 如果沒有，請移至步驟 3。  
  
2.  執行 [sp_restoredbreplication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-restoredbreplication-transact-sql.md)。 如果此預存程序成功執行，則還原完成。 如果未成功執行，請移至步驟 3。  
  
3.  執行 [sp_removedbreplication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md) 以移除所有複寫設定。  
  
     必要時請重新設定複寫。 如果您已根據建議編寫了複寫拓撲的指令碼，請使用指令碼以重新設定拓撲。  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server 資料庫的備份與還原](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)   
 [備份及還原複寫的資料庫](../../relational-databases/replication/administration/back-up-and-restore-replicated-databases.md)   
 [錯誤和事件參考 &#40;複寫&#41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  
