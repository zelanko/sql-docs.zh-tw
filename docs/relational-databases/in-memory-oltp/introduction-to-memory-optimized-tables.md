---
title: 記憶體最佳化的資料表簡介 | Microsoft Docs
ms.custom: ''
ms.date: 12/02/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: in-memory-oltp
ms.reviewer: ''
ms.suite: sql
ms.technology: in-memory-oltp
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: ef1cc7de-63be-4fa3-a622-6d93b440e3ac
caps.latest.revision: 22
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: e3edda9ebc4f356302c1e6a01c87d026bdb8f5e9
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/19/2018
---
# <a name="introduction-to-memory-optimized-tables"></a>記憶體最佳化的資料表簡介
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  記憶體最佳化資料表是使用 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md) 所建立。  
  
 記憶體最佳化資料表預設為完全持久。就像 (傳統) 磁碟資料表上的交易一樣，記憶體最佳化資料表上的交易為完全不可部分完成、一致、隔離且持久 (ACID)。 記憶體最佳化資料表和原生編譯的預存程序僅支援 [!INCLUDE[tsql](../../includes/tsql-md.md)] 功能的子集。
 
自 SQL Server 2016 開始，Azure SQL Database 中不限制針對記憶體內部 OLTP 的 [定序或字碼頁](../../relational-databases/collations/collation-and-unicode-support.md) 。
  
 記憶體最佳化資料表的主要存放區是主記憶體。 資料表中的資料列可從記憶體讀取，並且可寫入記憶體。 資料表資料的第二個副本保留在磁碟上，但僅做為持久性用途。 如需有關持久資料表的詳細資訊，請參閱 [建立及管理記憶體最佳化物件的儲存體](../../relational-databases/in-memory-oltp/creating-and-managing-storage-for-memory-optimized-objects.md) 。 記憶體最佳化資料表中的資料只會在資料庫復原時從磁碟中讀取 (例如 伺服器重新啟動後)。  
  
 為了更進一步提升效能，記憶體中 OLTP 支援延遲交易持久性的持久資料表。 延遲的持久交易會在交易被認可且將控制權傳回給用戶端之後，立即儲存至磁碟。 為了提升效能，付出的代價是在伺服器當機或容錯移轉時，遺失未儲存至磁碟的已認可交易。  
  
 除了預設持久的記憶體最佳化資料表之外， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 還支援非持久記憶體最佳化資料表，這些資料表不會記錄，且其資料不會保存在磁碟上。 這表示，這些資料表上的交易不需要任何磁碟 IO，但其資料在伺服器當機或容錯移轉後，將無法復原。  
  
 記憶體中 OLTP 的目標是與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 整合，以便在開發、部署、管理能力及支援能力等各方面提供完美無瑕的體驗。 資料庫可以包含位於記憶體中以及以磁碟為基礎的物件。  
  
 記憶體最佳化資料表中的資料列會建立版本。 這表示，資料表的每個資料列可能有多個版本。 所有資料列版本都是在相同資料表資料結構中維護。 只要使用資料列版本設定功能，就能在同一個資料列並行讀取和寫入。 如需並行讀取和寫入同一個資料列的詳細資訊，請參閱 [Transactions with Memory-Optimized Tables](../../relational-databases/in-memory-oltp/transactions-with-memory-optimized-tables.md)與記憶體最佳化資料表的交易。  
  
 下圖說明多重版本設定。 此圖顯示一個資料表包含三個資料列，每個資料列各有不同的版本。  
  
![多重版本設定。](../../relational-databases/in-memory-oltp/media/hekaton-tables-1.gif "多重版本設定。")  
  
 該資料表具有三個資料列：r1、r2 和 r3。 r1 有三個版本、r2 有兩個版本，而 r3 有四個版本。 請注意，相同資料列的不同版本不一定佔用連續記憶體位置。 不同的資料列版本可能分散在資料表資料結構中。  
  
 記憶體最佳化的資料表資料結構可以視為資料列版本的集合。 磁碟基礎的資料表中的資料列是以頁面與範圍方式組織，其中個別資料列使用頁碼和頁面位移來定址，而記憶體最佳化資料表中的資料列版本則是使用 8 位元組記憶體指標來定址。  
  
 記憶體最佳化資料表中的資料，可使用下列兩種方式的其中一種進行存取：  
  
-   透過原生編譯的預存程序。  
  
-   透過位於原生方式編譯之預存程序外部的解譯 [!INCLUDE[tsql](../../includes/tsql-md.md)]。 這些 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式可以位於解譯的預存程序內，也可以是特定 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式。  
  
## <a name="accessing-data-in-memory-optimized-tables"></a>存取記憶體最佳化資料表中的資料  

從原生編譯的預存程序可以最有效率地存取記憶體最佳化資料表 ([原生編譯預存程序](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md))。 使用 (傳統) 解譯的 [!INCLUDE[tsql](../../includes/tsql-md.md)]也可以存取記憶體最佳化資料表。 解譯的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 是指在不使用原生編譯之預存程序的情況下存取記憶體最佳化資料表。 解譯的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 存取範例包括從 DML 觸發程序、特定 [!INCLUDE[tsql](../../includes/tsql-md.md)] 批次、檢視和資料表值函式，存取記憶體最佳化資料表。  
  
 下表摘要說明各種物件的原生和解譯 [!INCLUDE[tsql](../../includes/tsql-md.md)] 存取。  
  
|功能|使用原生編譯的預存程序存取|解譯的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 存取|CLR 存取|  
|-------------|-------------------------------------------------------|-------------------------------------------|----------------|  
|記憶體最佳化資料表|是|是|否*|  
|記憶體最佳化資料表類型|是|是|否|  
|原生編譯的預存程序|現在支援原生編譯預存程序的巢狀項目。 只要參考的預存程序也是原生編譯的，您就可以在預存程序中使用 EXECUTE 語法。|是|否*|  
  
 *您無法從內容連線 (執行 CLR 模組時來自 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的連線) 存取記憶體最佳化資料表或原生編譯預存程序。 不過，您可以建立及開啟另一個連接，並從中存取記憶體最佳化資料表和原生編譯預存程序。  
  
## <a name="performance-and-scalability"></a>效能和延展性  

下列因素會影響記憶體中 OLTP 可達到的效能提升：  
  
*通訊：* 相較於具有較少呼叫而且每個預存程序中實作更多功能的應用程式，具有簡短預存程序的許多呼叫的應用程式可能會看到較少的效能增益。  
  
「[!INCLUDE[tsql](../../includes/tsql-md.md)]執行」：記憶體內部 OLTP 使用原生編譯的預存程序時可達到最佳效能，而不是使用解譯的預存程序或查詢執行時。 從這樣的預存程序存取記憶體最佳化資料表頗有助益。  
  
*範圍掃描與點查閱的比較︰* 記憶體最佳化非叢集索引可支援範圍掃描和排序的掃描。 對於點查閱而言，記憶體最佳化雜湊索引的效能比記憶體最佳化的非叢集索引更好。 記憶體最佳化非叢集索引的效能比以磁碟為基礎的索引更好。

- 自 SQL Server 2016 起，記憶體最佳化資料表的查詢計畫能以平行方式掃描資料表。 這可改善分析查詢的效能。
  - 雜湊索引在 SQL Server 2016 也能以平行方式掃描。
  - 非叢集索引在 SQL Server 2016 也能以平行方式掃描。
  - 資料行存放區索引自 SQL Server 2014 起始以來，即能以平行方式掃描。
  
「索引作業」： 索引作業不會記錄下來，且只存在於記憶體中。  
  
「並行」： 效能受到引擎層級並行影響的應用程式，如閂鎖競爭或封鎖，改用記憶體內部 OLTP 之後，將可大幅改善其效能。  
  
下表列出關聯式資料庫中經常發現的效能和延展性問題，以及記憶體中 OLTP 如何改善效能。  
  
|問題|記憶體中 OLTP 影響|  
|-----------|----------------------------|  
|效能<br /><br /> 高資源 (CPU、I/O、網路或記憶體) 使用量。|CPU<br /> 原生編譯的預存程序可大幅降低 CPU 使用量，因為它們執行 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式所需的指令比 (傳統) 解譯的預存程序少了許多。<br /><br /> 記憶體中 OLTP 有助於減少向外延展的工作負載中的硬體投資，因為一部伺服器具有提供五到十部伺服器輸送量的潛力。<br /><br /> I/O<br /> 如果處理資料或索引頁面時遭遇 I/O 瓶頸，記憶體中 OLTP 可減少瓶頸。 此外，記憶體中 OLTP 物件的檢查點是連續的，不會導致 I/O 作業突然增加。 不過，如果效能嚴重不足資料表的工作集無法納入記憶體中，記憶體中 OLTP 將無法改善效能，因為它要求資料必須是記憶體駐留。 如果在記錄時遭遇 I/O 瓶頸，記憶體中 OLTP 可減少瓶頸，因為它進行的記錄較少。 如果將一個或多個記憶體最佳化資料表設為非持久資料表，就可以消除記錄資料的作業。<br /><br /> 記憶體<br /> 記憶體中 OLTP 並未提供任何效能優勢。 此外，記憶體中 OLTP 可能會對記憶體造成額外的壓力，因為物件需駐留在記憶體中。<br /><br /> 網路<br /> 記憶體中 OLTP 並未提供任何效能優勢。 資料需要從資料層到應用程式層之間的通訊。|  
|延展性<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 應用程式中大多數的擴充問題都是由並行問題所造成，例如競爭鎖定、閂鎖和執行緒同步鎖定。|閂鎖競爭<br /> 典型的案例是以索引鍵順序並行插入資料列時，競爭索引的最後一頁。 由於記憶體中 OLTP 存取資料時不會採用閂鎖，因此可完全消除與執行緒同步鎖定競爭相關的延展性問題。<br /><br /> 執行緒同步鎖定競爭<br /> 由於記憶體中 OLTP 存取資料時不會採用閂鎖，因此可完全消除與同步鎖定競爭相關的延展性問題。<br /><br /> 鎖定相關的競爭<br /> 如果資料庫應用程式在讀取和寫入作業之間發生封鎖問題，記憶體中 OLTP 可解決封鎖問題，因為它使用新的開放式並行控制形式來實作所有交易隔離層級。 記憶體中 OLTP 不會使用 TempDB 儲存資料列版本。<br /><br /> 如果由於兩項寫入作業之間的衝突導致延展問題發生，例如兩項並行交易嘗試更新同一個資料列，記憶體中 OLTP 會讓其中一項交易成功，而讓另一項交易失敗。 失敗的交易必須以明確或隱含的方式重新送出，以重試交易。 不論是哪一種情況，您都必須變更應用程式。<br /><br /> 如果您的應用程式在兩個寫入作業之間遇到常見的衝突，開放式鎖定的值會減少。 此應用程式不適用 In-Memory OLTP。 大部分的 OLTP 應用程式都沒有寫入衝突，除非衝突是由鎖定擴大所引發。|  
  
##  <a name="rls"></a> 記憶體最佳化資料表中的資料列層級安全性  

記憶體最佳化資料表支援[資料列層級安全性](../../relational-databases/security/row-level-security.md) 。 將資料列層級安全性原則套用到記憶體最佳化資料表基本上與磁碟資料表相同，唯一差異在於當作安全性述詞使用的內嵌資料表值函式必須為原生編譯 (使用 WITH NATIVE_COMPILATION 選項建立)。 如需詳細資料，請參閱 [資料列層級安全性](../../relational-databases/security/row-level-security.md#Limitations) 主題中的 [跨功能的相容性](../../relational-databases/security/row-level-security.md) 一節。  
  
 記憶體內部資料表已啟用資料列層級安全性所需的各種內建功能。 如需詳細資料，請參閱 [Built-in Functions in Natively Compiled Modules](../../relational-databases/in-memory-oltp/supported-features-for-natively-compiled-t-sql-modules.md#bfncsp)(原生編譯模組中的內建函數)。  
  
 **EXECUTE AS CALLER** - 所有原生模組現在皆支援並預設使用 EXECUTE AS CALLER，即使未指定提示亦然。 這是因為所有資料列層級安全性述詞函數都應該使用 EXECUTE AS CALLER，以便在呼叫使用者的內容中評估函數 (及其中使用的任何內建函數)。   
對呼叫端進行權限檢查會造成 EXECUTE AS CALLER 的效能受到輕微 (大約 10%) 影響。 如果模組明確指定 EXECUTE AS OWNER 或 EXECUTE AS SELF，就能避免這些權限檢查及其相關效能成本。 不過，一併使用這兩種其中之一與上方內建函數，則會因為必要的環境切換而造成明顯較嚴重的效能影響。  
  
## <a name="scenarios"></a>案例

如需 [!INCLUDE[hek_1](../../includes/hek-1-md.md)] 可以改善效能之典型案例的簡短討論，請參閱 [記憶體內部 OLTP](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)。  
  
## <a name="see-also"></a>另請參閱

[記憶體內部 OLTP &#40;記憶體內部最佳化&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
