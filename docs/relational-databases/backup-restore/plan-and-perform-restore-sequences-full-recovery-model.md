---
title: "規劃和執行還原順序 (完整復原模式) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- restore sequences [SQL Server], planning for
- full recovery model [SQL Server], planning restore sequences
ms.assetid: 9cbefaf8-d2b6-41c9-83fc-b3807a841fe2
caps.latest.revision: 33
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 92fca3a74586d7c7adbe135422283342db36a204
ms.contentlocale: zh-tw
ms.lasthandoff: 04/11/2017

---
# <a name="plan-and-perform-restore-sequences-full-recovery-model"></a>規劃和執行還原順序 (完整復原模式)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  此主題說明如何針對一般使用完整復原模式的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫，規劃及執行還原順序。 「還原順序」是一或多個 [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md) 陳述式的順序。 還原順序通常會初始化所還原之資料庫、檔案及/或頁面的內容 (資料複製階段)、向前復原記錄的交易 (重做階段)，再回復未認可的交易 (恢復階段)。  
  
 在單純的情況下，還原順序只需要一個完整資料庫備份、一個差異資料庫備份，以及一或多個後續記錄備份。 這種時候，建構正確的還原順序相當容易， 例如，若要將整個資料庫還原到失敗點，可以從備份使用中交易記錄 (記錄的「結尾」) 開始。 然後，還原最近一次完整資料庫備份、最近一次差異備份 (若有的話)，再依照進行記錄備份的順序還原所有後續的記錄備份。  
  
 在更複雜的情況下，建構正確的還原順序會是很複雜的程序。 例如，還原順序可能需要多個檔案備份，或者必須將資料還原到特定的時間點。 在極其複雜的情況下，甚至可能需要周遊跨越一個或多個復原分支的分岔復原路徑。  
  
> [!NOTE]  
>  「復原路徑」是指將資料庫復原到特定時間點 (稱為復原點) 的資料和記錄備份順序。 復原路徑是一組特定轉換，這些轉換會使資料庫隨時間而變化，同時又能維護資料庫的一致性。 復原路徑描述從起點 (LSN,GUID) 到終點 (LSN,GUID) 的 LSN 範圍。 復原路徑中的 LSN 範圍從開始到結束可能會跨越一個或多個復原分支。  
  
## <a name="to-plan-a-restore-sequence"></a>規劃還原順序  
 在啟動還原順序前，請遵循下列步驟：  
  
1.  盡可能建立資料庫的結尾記錄備份。 如需詳細資訊，請參閱[結尾記錄備份 &#40;SQL Server&#41;](../../relational-databases/backup-restore/tail-log-backups-sql-server.md)。  
  
2.  判斷目標復原點。  
  
     目標復原點可以是交易記錄備份中的任何時間點或標示。 如需詳細資訊，請參閱[將 SQL Server 資料庫還原至某個時間點 &#40;完整復原模式&#41;](../../relational-databases/backup-restore/restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md) 或[使用標示的交易以一致的方式復原相關資料庫 &#40;完整復原模式&#41;](../../relational-databases/backup-restore/use-marked-transactions-to-recover-related-databases-consistently.md)。  
  
3.  決定要執行的還原類型。 如需詳細資訊，請參閱 [還原和復原概觀 &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md)。  
  
4.  識別所需的備份，並確定必要的媒體集和備份裝置都可使用。 如需詳細資訊，請參閱[備份裝置 &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md) 和[媒體集、媒體家族與備份組 &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)。  
  
## <a name="to-perform-a-restore-sequence"></a>執行還原順序  
 若要執行還原順序，請遵循下列步驟：  
  
1.  若要啟動順序，請還原一或多個資料備份，例如資料庫備份、部分備份、一或多個檔案備份。  
  
2.  此外，也可以還原以這些完整備份為基礎的最新差異備份。  
  
     針對您要還原的每個完整備份，判斷它是否為任何差異備份的基底。 若是如此，請盡可能還原最近一次的差異備份。 如需詳細資訊，請參閱[差異備份 &#40;SQL Server&#41;](../../relational-databases/backup-restore/differential-backups-sql-server.md)。  
  
3.  依序還原記錄備份以向前復原資料庫，最後再還原包含復原點的備份。 是否需要套用所有的記錄備份，取決於什麼記錄備份包含了目標復原點，如下所述：  
  
    -   如果復原點是失敗點，則必須還原在您還原的最後一個資料 (完整或差異) 備份之後所建立的每個記錄備份。 如需詳細資訊，請參閱[套用交易記錄備份 &#40;SQL Server&#41;](../../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md)。  
  
    -   如果是時間點還原，您可能就不需要最近一次的記錄備份。 如果您使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]，Database Recovery Advisor 會確定只選取要還原到指定的時間點所需的備份。 這些備份為您的時間點還原構成了建議的還原計畫。 如需詳細資訊，請參閱[將 SQL Server 資料庫還原至某個時間點 &#40;完整復原模式&#41;](../../relational-databases/backup-restore/restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md)。  
  
## <a name="restarting-a-restore-sequence"></a>重新啟動還原順序  
 如果還原順序產生的結果有問題，您可以停止還原順序，然後從頭開始重新啟動。 例如，如果您不小心還原了太多記錄備份，並且超過預期的復原點，就必須重新啟動還原順序，一直到含有目標復原點的記錄備份。  
  
## <a name="see-also"></a>另請參閱  
 [備份概觀 &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-overview-sql-server.md)   
 [還原和復原概觀 &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md)   
 [完整資料庫還原 &#40;完整復原模式&#41;](../../relational-databases/backup-restore/complete-database-restores-full-recovery-model.md)   
 [線上還原 &#40;SQL Server&#41;](../../relational-databases/backup-restore/online-restore-sql-server.md)   
 [檔案還原 &#40;完整復原模式&#41;](../../relational-databases/backup-restore/file-restores-full-recovery-model.md)   
 [還原頁面 &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-pages-sql-server.md)   
 [分次還原 &#40;SQL Server&#41;](../../relational-databases/backup-restore/piecemeal-restores-sql-server.md)  
  
  
