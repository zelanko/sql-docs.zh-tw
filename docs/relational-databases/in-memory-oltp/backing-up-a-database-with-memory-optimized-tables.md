---
title: 備份含有記憶體最佳化資料表的資料庫 | Microsoft Docs
ms.custom: ''
ms.date: 03/20/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 83d47694-e56d-4dae-b54e-14945bf8ba31
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 0d607699e630ee7107b2ae3460e3b3152bb94bb4
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47703416"
---
# <a name="backing-up-a-database-with-memory-optimized-tables"></a>備份含有記憶體最佳化資料表的資料庫
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  記憶體最佳化資料表會當做正常資料庫備份的一部分進行備份。 如果是磁碟資料表，資料庫備份作業會驗證資料的 CHECKSUM 和差異檔案組，以便偵測是否有儲存體損毀。  
  
> [!NOTE]  
>  在備份期間，若您偵測到記憶體最佳化的檔案群組中，一或多個檔案有 CHECKSUM 錯誤，則備份作業失敗。 在此情況下，您必須從最後的已知良好備份還原資料庫。  
>   
>  若您沒有備份，可以從記憶體最佳化的資料表和磁碟基礎的資料表匯出資料，並在卸除及重新建立資料庫之後重新載入。  
  
 包含一個或多個記憶體最佳化資料表之資料庫的完整備份是由以下項目所組成：為磁碟資料表配置的儲存體 (如果有的話)、使用中的交易記錄，以及記憶體最佳化資料表的資料和差異檔案組 (又稱為檢查點檔案組)。 不過，如 [記憶體最佳化資料表的持久性](../../relational-databases/in-memory-oltp/durability-for-memory-optimized-tables.md)中所述，記憶體最佳化資料表所使用的儲存空間可能會遠超過它在記憶體中的大小，而且會影響資料庫備份的大小。  
  
## <a name="full-database-backup"></a>完整資料庫備份  
 因為磁碟資料表的備份是相同的，所以此處的討論內容著重於只包含持久性記憶體最佳化資料表之資料庫的資料庫備份。 記憶體最佳化檔案群組中的檢查點檔案組可能處於各種不同狀態。 下表描述備份檔案的哪個部分。  
  
|檢查點檔案組狀態|Backup|  
|--------------------------------|------------|  
|已預先建立|僅限檔案中繼資料|  
|建構中|僅限檔案中繼資料|  
|使用中|檔案中繼資料加上使用的位元組|  
|合併目標|僅限檔案中繼資料|  
|等候記錄截斷|檔案中繼資料加上使用的位元組|  
  
 如需檢查點檔案組狀態的描述，請參閱 [sys.dm_db_xtp_checkpoint_files &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-checkpoint-files-transact-sql.md) 及其資料行 state_desc。  
  
 包含一或多個記憶體最佳化資料表之資料庫備份的大小通常超過其在記憶體中的大小，但是小於磁碟儲存體的大小。 額外的大小取決於其他因素之間的已刪除資料列數目。  
  
### <a name="estimating-size-of-full-database-backup"></a>估計完整資料庫備份的大小  
  
> [!IMPORTANT]  
>  建議您不要使用 BackupSizeInBytes 值來估計記憶體中 OLTP 的備份大小。  
  
 第一個工作負載案例主要是為了插入。 在此案例中，大部分的資料檔案都處於使用中狀態，並且已完全載入，而且已刪除的資料列很少。 資料庫備份的大小與記憶體中的資料大小十分接近。  
  
 第二個工作負載案例適用於頻繁的插入、刪除與更新作業。 在最糟榚的情況下，在考量已刪除的資料列之後，每一個檢查點檔案組的載入程度為 50%。 資料庫備份的大小至少為記憶體中資料大小的兩倍。  
  
## <a name="differential-backups-of-databases-with-memory-optimized-tables"></a>使用記憶體最佳化資料表的資料庫差異備份  
 記憶體最佳化資料表的儲存體包含資料和差異檔案，如 [記憶體最佳化資料表的持久性](../../relational-databases/in-memory-oltp/durability-for-memory-optimized-tables.md)中所述。 具有記憶體最佳化資料表之資料庫的差異備份會包含下列資料：  
  
-   記憶體最佳化資料表的存在並不會影響儲存磁碟資料表之檔案群組的差異備份。  
  
-   使用中交易記錄與完整資料庫備份中相同。  
  
-   對於記憶體最佳化資料檔案群組而言，差異備份會使用與完整資料庫備份相同的演算法來識別資料和差異檔案以進行備份，但是它會接著篩選出檔案的子集，如下所述：  
  
    -   資料檔案包含新插入的資料列，當該檔案已滿時，會關閉並標示為唯讀。 資料檔案只有在上一次完整資料庫備份之後關閉時，才會進行備份。 差異備份只會備份資料檔案，其中包含上次完整資料庫備份後插入的資料列。 例外狀況為更新和刪除案例，部分插入的資料列可能已標示為記憶體回收，或是已遭記憶體回收。  
  
    -   差異檔案會儲存已刪除資料列的參考。 由於所有後續交易都可以刪除資料列，因此差異檔案可以在其存留期內隨時修改，而且永遠不會關閉。 差異檔案一律會備份。 差異檔案通常使用不到 10% 的儲存空間，因此差異檔案對於差異備份大小的影響非常小。  
  
 如果記憶體最佳化資料表是您資料庫大小的重要部分，則差異備份能夠大幅減少資料庫備份的大小。 如果是一般 OLTP 工作負載，差異備份將會遠小於完整資料庫備份。  
  
## <a name="see-also"></a>另請參閱  
 [備份、還原及復原記憶體最佳化資料表](http://msdn.microsoft.com/library/3f083347-0fbb-4b19-a6fb-1818d545e281)  
  
  
