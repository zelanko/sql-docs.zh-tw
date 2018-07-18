---
title: 資料庫卸離與附加 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: databases
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- upgrading databases
- databases [SQL Server], detaching
- detach database [SQL Server]
- databases [SQL Server], attaching
- removing databases
- transaction logs [SQL Server], detaching
- databases [SQL Server], removing
- restoring [SQL Server], attached databases
- transaction logs [SQL Server], attaching
- differential backups, after detaching
- moving databases
- attach database [SQL Server]
- detaching databases [SQL Server]
- differential base [SQL Server]
- attaching databases [SQL Server]
- databases [SQL Server], moving
ms.assetid: d0de0639-bc54-464e-98b1-6af22a27eb86
caps.latest.revision: 98
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d77629ddd1ebd711d9ec026c0b1a7a4ae9001f1b
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/10/2018
ms.locfileid: "33990484"
---
# <a name="database-detach-and-attach-sql-server"></a>資料庫卸離與附加 (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  您可以將資料庫的資料和交易記錄檔卸離，然後再重新附加至相同或不同的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體。 若要將資料庫變更至同一台電腦上的不同 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體，或要移動資料庫，卸離和附加資料庫相當有用。  
  
  
##  <a name="Security"></a> Security  
 檔案存取權限是在數個資料庫作業期間設定，包括卸離或附加資料庫。  
  
> [!IMPORTANT]  
>  建議您不要附加或還原來源不明或來源不受信任的資料庫。 這種資料庫可能包含惡意程式碼，因此可能執行非預期的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 程式碼，或是修改結構描述或實體資料庫結構而造成錯誤。 使用來源不明或來源不受信任的資料庫之前，請先在非實際執行伺服器的資料庫上執行 [DBCC CHECKDB](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md) ，同時檢查資料庫中的程式碼，例如預存程序或其他使用者定義程式碼。  
  
##  <a name="DetachDb"></a> 卸離資料庫  
 卸離資料庫時會從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體移除該資料庫，但會保留資料庫中的資料檔和交易記錄檔。 您可使用這些檔案將資料庫附加到任何 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體，包括已卸離該資料庫的伺服器。  
  
 如果下列任一情況為真，則您不能卸離資料庫：  
  
-   資料庫已複寫和發行。 如果複寫的話，必須取消發行資料庫。 在卸離資料庫之前，您必須先執行 [sp_replicationdboption](../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md)以停用發行。  
  
    > [!NOTE]  
    >  如果您無法使用 **sp_replicationdboption**，可執行 [sp_removedbreplication](../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md)來移除複寫。  
  
-   資料庫有資料庫快照集存在。  
  
     在卸離資料庫之前，您必須先卸除它的所有快照集。 如需詳細資訊，請參閱 [卸除資料庫快照集 &#40;Transact-SQL&#41;](../../relational-databases/databases/drop-a-database-snapshot-transact-sql.md)執行個體。  
  
    > [!NOTE]  
    >  無法卸離或附加資料庫快照集。  
  
-   資料庫正在資料庫鏡像工作階段中進行鏡像。  
  
     除非工作階段結束，否則，您無法卸離資料庫。 如需詳細資訊，請參閱 [移除資料庫鏡像 &#40;SQL Server&#41;](../../database-engine/database-mirroring/removing-database-mirroring-sql-server.md)＞。  
  
-   資料庫受質疑。 您無法卸離受質疑的資料庫，而必須先將受質疑的資料庫設定為緊急模式，才能將其卸離。 如需有關如何使資料庫進入緊急模式的詳細資訊，請參閱 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)。  
  
-   此資料庫是系統資料庫。  
  
### <a name="backup-and-restore-and-detach"></a>備份和還原與卸離  
 卸離唯讀資料庫會失去有關差異備份之差異基底的資訊。 如需詳細資訊，請參閱 [差異備份 &#40;SQL Server&#41;](../../relational-databases/backup-restore/differential-backups-sql-server.md)。  
  
### <a name="responding-to-detach-errors"></a>回應卸離錯誤  
 若在卸離資料庫時發生錯誤，資料庫將無法完全關閉，也無法重建交易記錄檔。 若您收到錯誤訊息，請執行下列訂正動作：  
  
1.  重新附加所有與資料庫關聯的檔案，而非只有主要檔案。  
  
2.  解決造成錯誤訊息的問題。  
  
3.  再次卸離資料庫。  
  
##  <a name="AttachDb"></a> 附加資料庫  
 您可以附加複製的或卸離的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫。 當您將包含全文檢索目錄檔案的 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 資料庫附加至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 伺服器執行個體時，系統就會從先前的位置附加這些目錄檔案以及其他資料庫檔案，此行為與 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]的行為相同。 如需詳細資訊，請參閱 [升級全文檢索搜尋](../../relational-databases/search/upgrade-full-text-search.md)。  
  
 當您附加資料庫時，所有的資料檔 (MDF 和 NDF 檔案) 都必須可供使用。 如果資料檔案的路徑與資料庫第一次建立或最後一次附加時的路徑不同，您必須指定檔案的目前路徑。  
  
> [!NOTE]  
>  如果附加的主要資料檔是唯讀的，則 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 會假設該資料庫也是唯讀的。  
  
 第一次將加密的資料庫附加到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體時，資料庫擁有者必須執行下列陳述式來開啟資料庫的主要金鑰：OPEN MASTER KEY DECRYPTION BY PASSWORD = **'***password***'**。 建議您執行下列陳述式來啟用主要金鑰的自動解密：ALTER MASTER KEY ADD ENCRYPTION BY SERVICE MASTER KEY。 如需詳細資訊，請參閱 [CREATE MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-master-key-transact-sql.md) 和 [ALTER MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-master-key-transact-sql.md)。  
  
 要不要附加記錄檔，其需求有一部分視資料庫是可讀寫或唯讀而定，如下所示：  
  
-   如果是讀寫資料庫，您通常可以在新位置附加記錄檔。 不過，某些情況下，重新附加資料庫需要其現有的記錄檔。 因此，請務必保留所有卸離的記錄檔，直到資料庫在沒有這些檔案的情形下成功附加為止。  
  
     如果讀寫資料庫具有單一記錄檔，而您未指定新位置給該記錄檔，附加作業就會在舊位置尋找該檔案。 如果找到，就會使用舊的記錄檔，不論資料庫是否完全關閉。 不過，如果找不到舊記錄檔，且資料庫已完全關閉而無使用中的記錄鏈結，附加作業便會嘗試為該資料庫建立新的記錄檔。  
  
-   如果附加的主要資料檔是唯讀的，則 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 會假設該資料庫也是唯讀的。 如果是讀寫資料庫，在資料庫主要檔案所指定的位置一定會有一或多個記錄檔。 由於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 無法更新儲存在主要檔案中的記錄檔位置，所以無法建立新記錄檔。  
  
  
###  <a name="Metadata"></a> 附加資料庫時的中繼資料變更  
 卸離後再重新附加唯讀資料庫時，會遺失目前差異基底的備份資訊。 *「差異基底」* (Differential Base) 是資料庫或資料庫之檔案或檔案群組子集中所有資料的最新完整備份。 如果沒有基底備份資訊， **master** 資料庫就會變成無法與唯讀資料庫同步處理，而之後所採用的差異備份可能會提供非預期的結果。 因此，如果搭配唯讀資料庫使用差異備份，重新附加資料庫後，應該利用完整備份來建立新的差異基底。 如需差異備份的相關資訊，請參閱[差異備份 &#40;SQL Server&#41;](../../relational-databases/backup-restore/differential-backups-sql-server.md)。  
  
 附加時會啟動資料庫。 一般來說，附加資料庫時，會將資料庫設定為先前卸離或複製時的相同狀態。 不過，附加與卸離作業會停用資料庫的跨資料庫擁有權鏈結。 如需如何啟用鏈結的相關資訊，請參閱 [跨資料庫擁有權鏈結伺服器組態選項](../../database-engine/configure-windows/cross-db-ownership-chaining-server-configuration-option.md)。 

 >[!IMPORTANT]
 > 根據預設且為了安全起見，每當附加資料庫時，*is_broker_enabled*、*is_honor_broker_priority_on* 和 *is_trustworthy_on* 的選項都會設定為 OFF。 如需如何將這些選項設定為 ON 的資訊，請參閱 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)。  如需中繼資料的詳細資訊，請參閱[管理在另一部伺服器上提供資料庫時所需的中繼資料](../../relational-databases/databases/manage-metadata-when-making-a-database-available-on-another-server.md)。
  
### <a name="backup-and-restore-and-attach"></a>備份和還原與附加  
 就像任何完全或部分離線的資料庫一樣，內含還原中檔案的資料庫是無法附加的。 如果停止還原順序，則可以附加資料庫。 然後，還是可以重新啟動還原順序。  
  
###  <a name="OtherServerInstance"></a> 將資料庫附加至另一個伺服器執行個體  
  
> [!IMPORTANT]  
>  由較新版本 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 所建立的資料庫無法附加在舊版本中。  
  
 將資料庫附加至另一個伺服器執行個體時，為了提供一致的經驗給使用者和應用程式，您可能會需要在其他伺服器執行個體上為資料庫重新建立部分或所有中繼資料，例如登入和作業。 如需詳細資訊，請參閱[管理在另一個伺服器執行個體上提供資料庫時所需的中繼資料 &#40;SQL Server&#41;](../../relational-databases/databases/manage-metadata-when-making-a-database-available-on-another-server.md)。  
  
##  <a name="RelatedTasks"></a> 相關工作  
 **若要卸離資料庫**  
  
-   [sp_detach_db &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-detach-db-transact-sql.md)  
  
-   [卸離資料庫](../../relational-databases/databases/detach-a-database.md)  
  
 **若要附加資料庫**  
  
-   [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)  
  
-   [附加資料庫](../../relational-databases/databases/attach-a-database.md)  
  
-   [sp_attach_db &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-attach-db-transact-sql.md)  
  
-   [sp_attach_single_file_db &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-attach-single-file-db-transact-sql.md)  
  
 **使用卸離和附加作業來升級資料庫**  
  
-   [使用卸離與附加來升級資料庫 &#40;Transact-SQL&#41;](../../relational-databases/databases/upgrade-a-database-using-detach-and-attach-transact-sql.md)  
  
 **使用卸離和附加作業來移動資料庫**  
  
-   [使用卸離與附加來移動資料庫 &#40;Transact-SQL&#41;](../../relational-databases/databases/move-a-database-using-detach-and-attach-transact-sql.md)  
  
 **若要刪除資料庫快照集**  
  
-   [卸除資料庫快照集 &#40;Transact-SQL&#41;](../../relational-databases/databases/drop-a-database-snapshot-transact-sql.md)  
  
## <a name="see-also"></a>另請參閱  
 [資料庫檔案與檔案群組](../../relational-databases/databases/database-files-and-filegroups.md)  
  
  
