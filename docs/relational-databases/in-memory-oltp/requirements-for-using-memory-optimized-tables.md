---
title: "使用記憶體最佳化資料表的需求 | Microsoft 文件"
ms.custom: SQL2016_New_Updated
ms.date: 11/16/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 47d9a7e8-c597-4b95-a58a-dcf66df8e572
caps.latest.revision: "65"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: de8c79ca45f7b02e25a893afd017c38c25340f2d
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="requirements-for-using-memory-optimized-tables"></a>使用記憶體最佳化資料表的需求
[!INCLUDE[tsql-appliesto-ss2014-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2014-xxxx-xxxx-xxx-md.md)]

  若要在 Azure DB 中使用記憶體內部 OLTP，請參閱[在 SQL Database 中開始使用 In-Memory](http://azure.microsoft.com/documentation/articles/sql-database-in-memory/)。  
  
 除了 [安裝 SQL Server 2016 的硬體與軟體需求](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)以外，以下還有使用記憶體內部 OLTP 的需求：  
  
-   SQL Server 2016 SP1 (或更新版本) 任何版本。 SQL Server 2014 及 SQL Server 2016 RTM (SP1 以前的版本) 需要 Enterprise、Developer 或 Evaluation 版本。
    - 請注意︰記憶體內部 OLTP 需要 64 位元版本的 SQL Server。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 需要有足夠的記憶體來容納記憶體最佳化資料表和索引中的資料，以及額外的記憶體來支援線上工作負載。 如需詳細資訊，請參閱 [估計記憶體最佳化資料表的記憶體需求](../../relational-databases/in-memory-oltp/estimate-memory-requirements-for-memory-optimized-tables.md) 。  

-   在虛擬機器 (VM) 中執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 時，請確定配置給 VM 的記憶體足以支援記憶體最佳化資料表和索引所需的記憶體。 視 VM 主應用程式而定，保證配置記憶體給 VM 的組態選項可稱為「保留的記憶體」；使用動態記憶體時，則稱為「RAM 下限」。 請確定這些設定對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中的資料庫需求已足夠。
  
-   釋放持久的記憶體最佳化資料表大小的兩倍磁碟空間。  
  
-   處理器需要支援指令 **cmpxchg16b** 以使用記憶體內部 OLTP。 所有新型 64 位元處理器都支援 **cmpxchg16b**。  
  
     如果您使用虛擬機器，而 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 顯示較舊處理器造成的錯誤，請查看 VM 主應用程式是否有允許 **cmpxchg16b**的組態選項。 如果沒有，您可以使用 Hyper-V，它可以支援 **cmpxchg16b** ，而不需要修改組態選項。  
  
-   記憶體內部 OLTP 會安裝為 **Database Engine Services**的一部分。  
  
     若要安裝報表產生 ([判斷是否應將資料表或預存程序匯出至記憶體內部 OLTP](../../relational-databases/in-memory-oltp/determining-if-a-table-or-stored-procedure-should-be-ported-to-in-memory-oltp.md)) 和 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (透過 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 物件總管來管理記憶體內部 OLTP)，請 [下載 SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/mt238290.aspx)。   
  
## <a name="important-notes-on-using-includehek2includeshek-2-mdmd"></a>使用 [!INCLUDE[hek_2](../../includes/hek-2-md.md)]的重要注意事項  
  
-   自 SQL Server 2016 起，記憶體最佳化資料表除了可用的記憶體之外，沒有大小限制。 在 SQL Server 2014 中，資料庫中所有持久資料表的記憶體內部大小總計，若為 SQL Server 2014 資料庫則不應該超過 250 GB。 如需詳細資訊，請參閱 [估計記憶體最佳化資料表的記憶體需求](../../relational-databases/in-memory-oltp/estimate-memory-requirements-for-memory-optimized-tables.md)。  
    - 請注意︰自 SQL Server 2016 SP1 開始，Standard 和 Express 版本支援記憶體內部 OLTP，但它們會徵用可以用在指定資料庫的記憶體最佳化資料表記憶體數量的配額。 Standard 版本是每個資料庫 32 GB，Express 版本是每個資料庫 352 MB。 
  
-   如果您建立一個或多個具有記憶體最佳化資料表的資料庫，就應該針對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體啟用立即檔案初始化 (將 SE_MANAGE_VOLUME_NAME 使用者權限授與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務啟動帳戶)。 如果沒有立即檔案初始化，記憶體最佳化儲存體檔案 (資料和差異檔案) 將會在建立時初始化，而這樣可能會對工作負載的效能造成負面影響。 如需有關立即檔案初始化的詳細資訊，請參閱 [資料庫檔案初始化](http://msdn.microsoft.com/library/ms175935\(SQL.105\).aspx)。 如需有關如何啟用立即檔案初始化的詳細資訊，請參閱 [如何及為何啟用立即檔案初始化](http://blogs.msdn.com/b/sql_pfe_blog/archive/2009/12/23/how-and-why-to-enable-instant-file-initialization.aspx)。  
  
## <a name="see-also"></a>另請參閱  
 [記憶體內部 OLTP &#40;記憶體內部最佳化&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
