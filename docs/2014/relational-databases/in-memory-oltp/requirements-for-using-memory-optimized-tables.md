---
title: 使用記憶體最佳化資料表的需求 | Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- SQL Server 2014
ms.assetid: 47d9a7e8-c597-4b95-a58a-dcf66df8e572
caps.latest.revision: 53
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: f4b47ee3a3f4274ca94175060f10722fa45b6693
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37190388"
---
# <a name="requirements-for-using-memory-optimized-tables"></a>使用記憶體最佳化資料表的需求
  除了[硬體和軟體需求，安裝 SQL Server 2014](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)，以下還有使用記憶體內部 OLTP 的需求：  
  
-   [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 64 位元 Enterprise、Developer 或 Evaluation Edition。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 需要足夠的記憶體來容納記憶體最佳化資料表和索引中的資料。 為了說明資料列版本，您應該提供記憶體最佳化的資料表和索引預期大小兩倍的記憶體數量。 但是所需的實際記憶體數目將取決於您的工作負載。 您應該監視記憶體使用量並視需要進行調整。 記憶體最佳化資料表的資料大小不得超過集區所允許的百分比。 若要探索記憶體最佳化資料表的大小，請參閱[sys.dm_db_xtp_table_memory_stats &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-db-xtp-table-memory-stats-transact-sql)。  
  
     如果資料庫中有以磁碟為基礎的資料表，您需要提供足夠的記憶體，讓緩衝集區和查詢能夠在這些資料表上進行處理。  
  
     請務必了解記憶體中 OLTP 應用程式需要多少記憶體。 如需詳細資訊，請參閱 [估計記憶體最佳化資料表的記憶體需求](memory-optimized-tables.md) 。  
  
-   釋放持久的記憶體最佳化資料表大小的兩倍磁碟空間。  
  
-   處理器需要支援指令 **cmpxchg16b** 以使用記憶體中 OLTP。 所有新型 64 位元處理器都支援 **cmpxchg16b**。  
  
     如果您使用 VM 主應用程式和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]顯示，較舊處理器造成的錯誤，請參閱 「 應用程式是否有設定選項，以允許**cmpxchg16b**。 如果沒有，您可以使用 Hyper-V，它可以支援 **cmpxchg16b** ，而不需要修改組態選項。  
  
-   若要安裝記憶體內部 OLTP，請選取**Database Engine Services**當您安裝[!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]。  
  
     若要安裝報表產生 ([判斷是否將資料表或預存程序應該移植至記憶體中 OLTP](determining-if-a-table-or-stored-procedure-should-be-ported-to-in-memory-oltp.md)) 和[!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] (管理記憶體中 OLTP 透過[!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]物件總管 中)，請選取**管理工具 — 基本**或是**管理工具 — 進階**當您安裝[!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]。  
  
## <a name="important-notes-on-using-includehek2includeshek-2-mdmd"></a>使用 [!INCLUDE[hek_2](../../../includes/hek-2-md.md)]的重要注意事項  
  
-   資料庫中所有持久資料表的記憶體中大小總計不應該超過 250 GB。 如需詳細資訊，請參閱 <<c0> [ 記憶體最佳化資料表的持久性](durability-for-memory-optimized-tables.md)。  
  
-   這個 [!INCLUDE[hek_2](../../../includes/hek-2-md.md)] 版本的目標是在含有 2 或 4 個通訊端且少於 60 個核心的系統上可以最佳化方式執行。  
  
-   檢查點檔案無法手動刪除。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會對不需要的檢查點檔案自動執行記憶體回收。 如需詳細資訊，請參閱討論在合併中的資料和差異檔案[記憶體最佳化資料表的持久性](durability-for-memory-optimized-tables.md)。  
  
-   在此第一版記憶體中 OLTP (在[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)])，移除記憶體最佳化檔案群組的唯一方式是卸除資料庫。  
  
-   如果您在嘗試刪除大批資料列時，有並行的插入或更新工作負載會影響您正嘗試刪除的資料列範圍，則刪除作業可能會失敗。 解決方法是先停止插入或更新工作負載，然後執行刪除。 或者，您也可以將交易設定為較小的交易，這樣做比較不容易受到並行工作負載所中斷。 如同所有寫入作業，記憶體最佳化資料表上的，使用重試邏輯 ([Guidelines for Retry Logic for Transactions on Memory-Optimized Tables](../../database-engine/guidelines-for-retry-logic-for-transactions-on-memory-optimized-tables.md))。  
  
-   如果您建立一個或多個具有記憶體最佳化資料表的資料庫，就應該針對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體啟用立即檔案初始化 (將 SE_MANAGE_VOLUME_NAME 使用者權限授與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務啟動帳戶)。 如果沒有立即檔案初始化，記憶體最佳化儲存體檔案 (資料和差異檔案) 將會在建立時初始化，而這樣可能會對工作負載的效能造成負面影響。 如需有關立即檔案初始化的詳細資訊，請參閱 [資料庫檔案初始化](http://msdn.microsoft.com/library/ms175935\(SQL.105\).aspx)。 如需有關如何啟用立即檔案初始化的詳細資訊，請參閱 [如何及為何啟用立即檔案初始化](http://blogs.msdn.com/b/sql_pfe_blog/archive/2009/12/23/how-and-why-to-enable-instant-file-initialization.aspx)。  
  
## <a name="did-this-article-help-you-were-listening"></a>這篇文章對您有幫助嗎？ 我們會持續聽取您的意見  
 您要尋找哪些資訊？找到了嗎？ 我們會持續聽取您的意見來改進內容。 請提交您的意見[ sqlfeedback@microsoft.com ](mailto:sqlfeedback@microsoft.com?subject=Your%20feedback%20about%20the%20Requirements%20for%20Using%20Memory-Optimized%20Tables%20page)。  
  
## <a name="see-also"></a>另請參閱  
 [記憶體內部 OLTP &#40;記憶體內部最佳化&#41;](in-memory-oltp-in-memory-optimization.md)  
  
  
