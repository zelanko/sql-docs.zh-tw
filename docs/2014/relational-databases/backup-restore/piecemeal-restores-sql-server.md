---
title: 分次還原 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- partial updates [SQL Server]
- staged restores [SQL Server]
- piecemeal restores [SQL Server]
- restoring [SQL Server], piecemeal restore scenario
ms.assetid: 208f55e0-0762-4cfb-85c4-d36a76ea0f5b
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 55520388424e110420ad96d329081ee7a61fe028
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48057766"
---
# <a name="piecemeal-restores-sql-server"></a>分次還原 (SQL Server)
  這個主題僅與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Enterprise 版中包含多個檔案或檔案群組 (若是簡單模式，僅適用唯讀檔案群組) 的資料庫有關。  
  
 如需分次還原及記憶體最佳化資料表的詳細資訊，請參閱 [分次還原具有記憶體最佳化資料表的資料庫](../in-memory-oltp/memory-optimized-tables.md)。  
  
 *「分次還原」* (Piecemeal Restore) 允許對含有多個檔案群組的資料庫分段進行還原與復原。 分次還原涉及一連串的還原順序，這會從主要檔案群組開始，而在某些情況下，還會從其中一個或多個次要的檔案群組開始。 分次還原會維護各項檢查，以確保最後資料庫能維持一致。 還原順序完成後，就可以直接讓復原的檔案 (如果這些檔案有效，而且與資料庫一致) 上線。  
  
 分次還原適用於所有恢復模式，但它對於完整模式和大量記錄模式，可以提供比簡單模式更大的彈性。  
  
 每個分次還原都會從稱為「部分還原順序」(Partial-Restore Sequence) 的初始還原順序開始進行。 部分還原順序至少會還原並復原主要檔案群組，而在簡單復原模式下，則是所有的讀取/寫入檔案群組。 在分次還原順序期間，整個資料庫必須離線。 此後，資料庫便會在線上，而還原的檔案群組也可供使用。 不過，任何未還原的檔案群組會維持離線且無法存取。 但是，您可以稍後再利用檔案還原來還原離線檔案群組並讓它們回到線上。  
  
 不論資料庫使用的復原模式為何，部分還原順序從還原完整備份及指定 PARTIAL 選項的 RESTORE DATABASE 陳述式開始。 PARTIAL 選項永遠會開始新的分次還原，因此您只能在部分還原順序的初始陳述式中指定 PARTIAL 一次。 完成部分還原順序並讓資料庫回到線上後，其餘的檔案狀態都會變成「復原暫止」，因為檔案的復原已經延後。  
  
 其後，分次還原通常包含一或多個還原順序，這稱為「檔案群組還原順序」。 只要您願意等，就可以等著執行特定的檔案群組還原順序。 每個檔案群組還原順序都會將一或多個離線檔案群組還原並復原到與資料庫一致的點上。 檔案群組還原順序的時間和次數取決於您的復原目標、您要還原的離線檔案群組數目，以及您在每一檔案群組還原順序當中還原的檔案群組數。  
  
 執行分次還原的實際需求視資料庫的復原模式而定。 如需詳細資訊，請參閱本主題稍後的「在簡單復原模式下分次還原」與「在完整復原模式下分次還原」。  
  
## <a name="piecemeal-restore-scenarios"></a>分次還原實例  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的所有版本都支援離線分次還原。 在 Enterprise 版中，分次還原可以在線上或離線進行。 離線與線上分次還原的含意如下：  
  
-   離線分次還原實例  
  
     在離線分次還原中，資料庫會在部分還原順序之後上線。 尚未還原的檔案群組會保持離線，但是有必要時，可以先將資料庫離線，再還原這些檔案群組。  
  
-   線上分次還原實例  
  
     如果是在部分還原順序之後的線上分次還原中，資料庫會在線上運作，且可使用主要檔案群組和任何復原的次要檔案群組。 尚未還原的檔案群組會保持離線，但資料庫持續在線上運作時可視需要予以還原。  
  
     線上分次還原可以包括延遲交易。 當只有還原檔案群組的子集時，可能會延遲相依於線上檔案群組之資料庫中的交易。 這是正常狀況，因為整個資料庫必須維持一致。 如需詳細資訊，請參閱 [延遲交易 &#40;SQL Server&#41;](deferred-transactions-sql-server.md)中無用的檔案群組。  
  
-   [!INCLUDE[hek_1](../../includes/hek-1-md.md)] 分次還原狀況  
  
     如需記憶體中 OLTP 資料庫之分次還原的相關資訊，請參閱 [使用記憶體最佳化資料表分次備份和還原資料庫](../in-memory-oltp/memory-optimized-tables.md)。  
  
## <a name="restrictions"></a>限制  
 如果部分還原順序排除任何 [FILESTREAM](../blob/filestream-sql-server.md) 檔案群組，則不支援時間點還原。 您可以強制還原順序，以繼續進行。 但是，絕對無法還原 RESTORE 陳述式中省略的 FILESTREAM 檔案群組。 若要強制時間點還原，請指定 CONTINUE_AFTER_ERROR 選項，連同 STOPAT、STOPATMARK 或 STOPBEFOREMARK 選項，而且您也必須在後續的 RESTORE LOG 陳述式中指定這些項目。 如果您指定 CONTINUE_AFTER_ERROR，則部分還原順序會成功，而 FILESTREAM 檔案群組則會變成無法復原。  
  
## <a name="piecemeal-restore-under-the-simple-recovery-model"></a>在簡單復原模式下分次還原  
 在簡單復原模式下，分次還原順序必須從完整資料庫或部分備份開始。 然後，如果還原備份是差異基底，請接著還原最近一次的差異備份。  
  
 在第一個部分還原順序期間，如果只還原讀取/寫入檔案群組的子集，則當您復原部分還原的資料庫時，任何未還原的檔案群組就會變得無用。 只有下列情況才適合省略部分還原順序中的讀取/寫入檔案群組：  
  
-   想要讓未還原的檔案群組變得無用。  
  
-   還原順序將到達每個未還原的檔案群組都變唯讀、被捨棄或解除功能 (於部分還原順序的前一個還原期間) 的復原點。  
  
-   完整備份是在資料庫使用簡單復原模式當時所進行的，但是復原點則是在資料庫使用完整復原模式的時候。 如需詳細資訊，請參閱本主題稍後的「針對已從簡單復原模式切換到完整復原模式的資料庫執行分次還原」。  
  
### <a name="requirements-for-piecemeal-restore-under-the-simple-recovery-model"></a>在簡單復原模式下分次還原的需求  
 在簡單復原模式下，初始階段會還原並復原主要檔案群組以及所有的讀取/寫入次要檔案群組。 初始階段完成後，就可以直接讓復原的檔案 (如果這些檔案有效，而且與資料庫一致) 上線。  
  
 此後，可以分一個或多個其他階段來還原唯讀檔案群組。  
  
 只有在下列情況成立時，才能對唯讀次要檔案群組進行分次還原：  
  
-   備份時唯讀。  
  
-   保持唯讀 (與主要檔案群組保持邏輯上的一致)。  
  
 若要執行分次還原，必須遵守下列方針：  
  
-   分次還原簡單復原模式資料庫的完整備份組必須包含下列項目：  
  
    -   包含主要檔案群組與所有檔案群組的部分或完整資料庫備份 (這些檔案群組在進行備份時都是可讀取/寫入的)。  
  
    -   每個唯讀檔案的備份。  
  
-   若要唯讀檔案的備份與主要檔案群組一致，從備份次要檔案群組開始，到包含主要檔案群組的備份完成為止，次要檔案群組都必須是唯讀。 如果差異檔案備份是在檔案群組成為唯讀之後才建立，您可以使用這些差異檔案備份。  
  
### <a name="piecemeal-restore-stages-simple-recovery-model"></a>分次還原階段 (簡單復原模式)  
 分次還原實例牽涉到下列階段：  
  
-   初始階段 (還原並復原主要檔案群組與所有讀取/寫入檔案群組)  
  
     初始階段會執行部分還原。 部分還原順序會還原主要檔案群組、所有讀取/寫入次要檔案群組，以及 (選擇性的) 某些唯讀檔案群組。 在初始階段，整個資料庫必須離線。 在初始階段之後，資料庫會持續在線上運作，且可使用還原的檔案群組。 不過，所有尚未還原的唯讀檔案群組會保持離線。  
  
     初始階段中的第一個 RESTORE 陳述式必須執行下列工作：  
  
    -   使用包含主要檔案群組與所有檔案群組 (進行備份時都是讀取/寫入的) 的部分或完整資料庫備份。 部分還原的順序，通常是從還原部分備份開始。  
  
    -   指定 PARTIAL 選項，指出分次還原的開始。  
  
    > [!NOTE]  
    >  PARTIAL 選項會執行安全性檢查，確保產生的資料庫適合用來做為實際執行的資料庫。  
  
    -   如果備份是完整資料庫備份，請指定 READ_WRITE_FILEGROUPS 選項。  
  
-   當資料庫在線上時，您可以使用一或多個線上檔案還原來還原並復原離線唯讀檔案 (在備份時是唯讀的)。 線上檔案還原的時間視您何時需要讓資料上線而定。  
  
     是否必須將資料還原到檔案，取決於下列條件：  
  
    -   與資料庫一致的有效唯讀檔案加以復原之後，不需還原任何資料，即可直接上線。  
  
    -   損毀或與資料庫不一致的檔案必須在復原之前予以還原。  
  
### <a name="examples"></a>範例  
  
-   [範例：分次還原資料庫 &#40;簡單復原模式&#41;](example-piecemeal-restore-of-database-simple-recovery-model.md)  
  
-   [範例：僅限於部分檔案群組的分次還原 &#40;簡單復原模式&#41;](example-piecemeal-restore-of-only-some-filegroups-simple-recovery-model.md)  
  
## <a name="piecemeal-restore-under-the-full-recovery-model"></a>在完整復原模式下分次還原  
 在完整復原模式或大量記錄復原模式下，分次還原適用於任何包含多個檔案群組的資料庫，而且您可以將資料庫還原到任何一個時間點。 分次還原的還原順序的運作方式如下：  
  
-   部分還原順序  
  
     部分還原順序會還原主要檔案群組，以及選擇性地還原某些次要檔案群組。  
  
     第一個 RESTORE DATABASE 陳述式必須執行下列工作：  
  
    -   指定 PARTIAL 選項。 這會指出分次還原的開始。  
  
    -   使用包含主要檔案群組的任何完整資料庫備份。 部分還原的順序，通常是從還原部分備份開始。  
  
    -   若要還原到特定時間點，您必須在部分還原順序中指定時間。 還原順序的每個連續步驟都必須指定相同的時間點。  
  
-   檔案群組還原順序會讓其他檔案群組在線上與資料庫保持一致。  
  
     在 Enterprise 版中，可以在資料庫仍在線上運作時還原並復原任何離線的次要檔案群組。 如果特定唯讀檔案是未受損的，且與資料庫一致，就不需要還原檔案。 如需詳細資訊，請參閱[復原資料庫而不還原資料 &#40;Transact-SQL&#41;](recover-a-database-without-restoring-data-transact-sql.md)。  
  
### <a name="applying-log-backups"></a>套用記錄備份  
 如果唯讀檔案群組從建立檔案備份以前已經是唯讀，就不需要將記錄備份套用到檔案群組，而且檔案還原會將它略過。 如果檔案群組是可讀取/寫入，就必須套用無間斷記錄備份鏈結至最後一個完整或差異還原，才能將檔案群組向前復原到目前的記錄檔。  
  
### <a name="examples"></a>範例  
  
-   [範例：分次還原資料庫 &#40;完整復原模式&#41;](example-piecemeal-restore-of-database-full-recovery-model.md)  
  
-   [範例：僅限於部分檔案群組的分次還原 &#40;完整復原模式&#41;](example-piecemeal-restore-of-only-some-filegroups-full-recovery-model.md)  
  
## <a name="performing-a-piecemeal-restore-of-a-database-whose-recovery-model-has-been-switched-from-simple-to-full"></a>針對已從簡單復原模式切換到完整復原模式的資料庫執行分次還原  
 從完整的部分或資料庫備份起，您就可以開始針對已經從簡單復原模式切換到完整復原模式的資料庫執行分次還原。 例如，考慮有個資料庫採取了下列步驟：  
  
1.  建立簡單模式資料庫的部分備份 (backup_1)。  
  
2.  過一段時間以後，將復原模式變更為「完整」。  
  
3.  建立差異備份。  
  
4.  開始進行記錄備份。  
  
 之後，以下的順序有效：  
  
1.  忽略部分次要檔案群組的部分還原。  
  
2.  差異還原後有其他必要的還原。  
  
3.  稍後，從 backup_1 部分備份進行讀取/寫入次要檔案群組 WITH NORECOVERY 檔案還原  
  
4.  差異備份之後緊接著原始分次還原順序中所還原的任何其他備份，可還原資料直到原始的復原點為止。  
  
## <a name="see-also"></a>另請參閱  
 [套用交易記錄備份 &#40;SQL Server&#41;](transaction-log-backups-sql-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)   
 [將 SQL Server 資料庫還原至某個時間點 &#40;完整復原模式&#41;](restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md)   
 [還原和復原概觀 &#40;SQL Server&#41;](restore-and-recovery-overview-sql-server.md)   
 [規劃和執行還原順序 &#40;完整復原模式&#41;](plan-and-perform-restore-sequences-full-recovery-model.md)  
  
  
