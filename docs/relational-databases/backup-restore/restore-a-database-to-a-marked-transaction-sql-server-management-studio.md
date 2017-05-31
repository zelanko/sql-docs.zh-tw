---
title: "還原資料庫至標示的交易 (SQL Server Management Studio) | Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.restoretlog.markedtransaction.f1
helpviewer_keywords:
- database restores [SQL Server], marked transactions
- restoring databases [SQL Server], marked transactions
- marked transactions [SQL Server], restoring
ms.assetid: 8f0ea144-1819-4832-905f-e5d0f49b066b
caps.latest.revision: 21
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 48529229420d7c2dafad334f3104e01add1a6746
ms.contentlocale: zh-tw
ms.lasthandoff: 04/11/2017

---
# <a name="restore-a-database-to-a-marked-transaction-sql-server-management-studio"></a>還原資料庫至標示的異動 (SQL Server Management Studio)
  當資料庫處於還原中狀態時，您可以利用 [還原交易記錄] 對話方塊，將資料庫還原成可用記錄備份中標示的交易。  
  
> [!NOTE]  
>  如需詳細資訊，請參閱[使用標示的交易以一致的方式復原相關資料庫 &#40;完整復原模式&#41;](../../relational-databases/backup-restore/use-marked-transactions-to-recover-related-databases-consistently.md) 和[復原包含標示之交易的相關資料庫](../../relational-databases/backup-restore/recovery-of-related-databases-that-contain-marked-transaction.md)。  
  
### <a name="to-restore-a-marked-transaction"></a>若要還原標示的交易  
  
1.  連接到適當的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]執行個體之後，在 [物件總管] 中按一下伺服器名稱展開伺服器樹狀目錄。  
  
2.  展開 **[資料庫]**，然後視資料庫而定，選取使用者資料庫，或者展開 **[系統資料庫]** 並選取一個系統資料庫。  
  
3.  以滑鼠右鍵按一下資料庫，指向 [工作]，然後按一下 [還原]。  
  
4.  按一下 [交易記錄]，這會開啟 [還原交易記錄] 對話方塊。  
  
5.  在 [一般] 頁面的 [還原至] 區段中，選取 [標示的交易]，這會開啟 [選取標示的交易] 對話方塊。 這個對話方塊會顯示一個方格，其中列出在選取的交易記錄備份中，可用之標示的交易。  
  
     依預設，會還原到標示的交易，但是不含該交易。 若也要還原標示的交易，請選取 **[包含標示的交易]**。  
  
     下表列出方格的各資料行標頭，並描述各標頭的值。  
  
    |標頭|Value|  
    |------------|-----------|  
    |\<空白>|顯示選取標示的核取方塊。|  
    |**交易標示**|在認可交易時，由使用者所指定之標示交易的名稱。|  
    |**日期**|認可交易的日期和時間。 交易日期和時間是依照 **msdbgmarkhistory** 資料表中的記錄所顯示，而非依照用戶端電腦的日期和時間。|  
    |**描述**|在認可交易時，由使用者所指定之標示交易的描述 (如果有的話)。|  
    |**LSN**|標示之交易的記錄序號。|  
    |**資料庫**|認可標示的交易之資料庫的名稱。|  
    |**使用者名稱**|認可標示的交易之資料庫使用者的名稱。|  
  
## <a name="see-also"></a>另請參閱  
 [Restore a Database Backup Using SSMS](../../relational-databases/backup-restore/restore-a-database-backup-using-ssms.md)   
 [還原交易記錄備份 &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-transaction-log-backup-sql-server.md)  
  
  
