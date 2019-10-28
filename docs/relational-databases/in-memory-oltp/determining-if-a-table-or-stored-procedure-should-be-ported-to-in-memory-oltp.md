---
title: 判斷是否應將資料表或預存程序移植至記憶體內部 OLTP | Microsoft Docs
ms.custom: ''
ms.date: 08/02/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
helpviewer_keywords:
- Analyze, Migrate, Report
- AMR
ms.assetid: c1ef96f1-290d-4952-8369-2f49f27afee2
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: a392904b378514bb22816a3c325535fbe94cbacf
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/25/2019
ms.locfileid: "72907854"
---
# <a name="determining-if-a-table-or-stored-procedure-should-be-ported-to-in-memory-oltp"></a>判斷是否應將資料表或預存程序匯出至記憶體中 OLTP
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中的交易效能分析報表，可協助您評估 In-Memory OLTP 是否能改善資料庫應用程式的效能。 此報表還能指出在應用程式中啟用記憶體內部 OLTP 所需執行的工作。 識別您要匯出至記憶體內部 OLTP 的磁碟資料表之後，即可使用 [記憶體最佳化建議程式](../../relational-databases/in-memory-oltp/memory-optimization-advisor.md)協助您遷移資料表。 同樣地， [Native Compilation Advisor](../../relational-databases/in-memory-oltp/native-compilation-advisor.md) 可協助您將預存程序匯出為原生編譯的預存程序。 如需移轉方法的資訊，請參閱 [In-Memory OLTP - 一般工作負載模式和移轉考量](https://msdn.microsoft.com/library/dn673538.aspx)。  
  
 直接針對生產資料庫，或是具有類似生產工作負載之作用中工作負載的測試資料庫，執行交易效能分析報表。  
  
 報表和移轉顧問可協助您完成下列工作︰  
  
-   分析您的工作負載，以判斷記憶體內部 OLTP 可能有助於改善效能的作用點。 交易效能分析報表接著會建議轉換成記憶體內部 OLTP 後獲益最多的資料表和預存程序。  
  
-   協助您規劃及執行移轉為記憶體中 OLTP 的作業。 從磁碟資料表移轉到記憶體最佳化資料表，其間的移轉路徑可能會很費時。 記憶體最佳化 Advisor 可協助您識別將資料表移至記憶體中 OLTP 之前必須先從資料表移除的不相容項目。 記憶體最佳化 Advisor 也可協助您了解將資料表移轉到記憶體最佳化的資料表時，將對應用程式造成什麼影響。  
  
     當您想要規劃移轉至記憶體中 OLTP 的作業，以及想要將部分資料表和預存程序移轉至記憶體中 OLTP 時，都可以檢查您的應用程式能否獲益於記憶體中 OLTP。  
  
    > [!IMPORTANT]  
    >  資料庫系統的效能取決於各種不同的因素，並不是所有因素都可由交易效能收集器來觀察和測量。 因此，交易效能分析報表不保證實際的效能增益將會符合預測 (如果進行了任何預測)。  
  
 若您在安裝 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 或[下載 SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) 時，選取 [管理工具 - 基本]  或 [管理工具 - 進階]  ，則會安裝交易效能分析報表和移轉建議程式作為 SQL Server Management Studio (SSMS) 的一部分。    
  
## <a name="transaction-performance-analysis-reports"></a>交易效能分析報表  
 若要在**物件總管**中產生交易效能分析報表，請以滑鼠右鍵按一下資料庫，依序選取 [報表]  、[標準報表]  和 [交易效能分析概觀]  。 資料庫必須具有作用中的工作負載或是最近執行的工作負載，以產生有意義的分析報表。  
  
### <a name="tables"></a>資料表
  
 資料表的詳細報表包含三個部分：  
  
-   掃描統計資料部分  
  
     此部分包含單一資料表，將顯示所收集有關資料庫資料表上掃描次數的統計資料。 資料行如下：  
  
    -   總存取數百分比。 整個資料庫活動中，此資料表上掃描次數與搜尋次數百分比。 此百分比愈高，表示與資料庫中的其他資料表相較下，較大量使用此資料表。  
  
    -   查閱統計資料/範圍掃描統計資料。 此資料行記錄分析期間，資料表上執行的點查閱及範圍掃描 (索引掃描及資料表掃描) 數。 每筆交易的平均值為預估。  
    
-   競爭統計資料部分  
  
     此部分包含在資料庫資料表上顯示競爭的資料表。 如需有關資料庫閂鎖和鎖定的詳細資訊，請參閱＜鎖定架構＞。 資料行如下：  
  
    -   總等候次數百分比。 與資料庫活動相比，此資料庫資料表上閂鎖和鎖定等候數的百分比。 此百分比愈高，表示與資料庫中的其他資料表相較下，較大量使用此資料表。  
  
    -   閂鎖統計資料。 這些資料行記錄關於此資料表查詢的閂鎖等候數。 如需有關閂鎖的詳細資訊，請參閱＜閂鎖＞。 此數字越高，表示資料表有越多閂鎖競爭。  
  
    -   鎖定統計資料。 此資料行群組記錄頁面鎖定取得數以及查詢此資料表的等候數。 如需鎖定的詳細資訊，請參閱＜了解 SQL Server 中的鎖定＞。 等候數越多，表示資料表上越多鎖定競爭。  
  
-   移轉難度部分  
  
     此部分包含顯示將此資料庫資料表轉換成記憶體最佳化資料表之難度的資料表。 較高的難度評等表示較難轉換資料表。 若要查看轉換此資料庫資料表的詳細資料，請使用記憶體最佳化建議程式。  
  
資料表詳細資料報表的掃描與競爭統計資料，是從 sys.dm_db_index_operational_stats (Transact-SQL) 收集和彙總。  

### <a name="stored-procedures"></a>預存程序

 CPU 時間與經過時間的比率較高的預存程序就是移轉作業的候選。 報表會顯示所有資料表參考，因為原生方式編譯預存程序只能參考記憶體最佳化資料表，而這些資料表可能會增加移轉成本。  
  
 預存程序的詳細資料報表包含兩個部分：  
  
-   執行統計資料部分  
  
     此部分包含的資料表將顯示所收集有關預存程序之執行的統計資料。 資料行如下：  
  
    -   快取的時間。 此執行計畫快取的時間。 如果預存程序從計畫快取卸除並重新輸入，每個快取都需要時間。  
  
    -   總 CPU 時間。 在分析期間，預存程序所耗用的總 CPU 時間。 此數字愈高，預存程序使用的 CPU 越多。  
  
    -   總執行時間。 在分析期間，預存程序使用的總執行時間量。 此數字和 CPU 時間之間的差異愈高，預存程序使用 CPU 的效率越低。  
  
    -   快取遺漏總數。 在分析期間，預存程序的執行所導致的快取遺漏數 (從實體儲存體讀取)。  
  
    -   執行計數。 在分析期間，此預存程序執行的次數。  
  
-   資料表參考部分  
  
     此部分包含的資料表是顯示此預存程序所參考的資料表。 將預存程序轉換至原生方式編譯預存程序之前，必須將所有這些資料表轉換為記憶體最佳化資料表，且必須放置在相同的伺服器和資料庫上。  
  
 預存程序詳細資料報表的執行統計資料，是從 sys.dm_exec_procedure_stats (Transact-SQL) 收集和彙總。 參考是從 sys.sql_expression_dependencies (Transact-SQL) 取得。  
  
 若要查看有關如何將預存程序轉換成原生編譯預存程序的詳細資料，請參閱＜原生編譯建議程式＞。  
  
## <a name="generating-in-memory-oltp-migration-checklists"></a>產生記憶體內部 OLTP 移轉檢查清單  
 移轉檢查清單可識別不受記憶體最佳化資料表或原生編譯預存程序支援的任何資料表或預存程序功能。 記憶體最佳化和原生編譯建議程式，可產生針對單一磁碟基礎資料表或或解譯 T-SQL 預存程序的檢查清單。 此外，它亦可為資料庫中的多個資料表和預存程序產生移轉檢查清單。  
  
 若要在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中產生移轉檢查清單，您可使用 **產生記憶體內 OLTP 移轉檢查清單** 命令或 PowerShell。  
  
**使用 UI 命令產生移轉檢查清單**  
  
1.  在**物件總管**中，以滑鼠右鍵按一下非系統資料庫的資料庫，按一下 [工作]  ，然後按一下 [產生記憶體內 OLTP 移轉檢查清單]  。  
  
2.  在 [產生記憶體內 OLTP 移轉檢查清單] 對話方塊中，按一下 [下一步] 巡覽至 [設定檢查清單產生選項]  頁面。 在頁面上執行下列動作。  
  
    1.  在 [將檢查清單儲存至]  方塊中，輸入資料夾路徑。  
  
    2.  確認選取 [為特定資料表及預存程序產生檢查清單]  。  
  
    3.  在區段方塊中展開 [資料表]  與 [預存程序]  節點。  
  
    4.  在選取方塊中選取幾個物件。  
  
3.  按一下 [下一步]  ，然後確認工作清單符合位於 [設定檢查清單產生選項]  頁面的設定。  
  
4.  按一下 [完成]  ，然後確認僅針對您選取的物件產生移轉檢查清單報表。  

 您可將這些報表與記憶體最佳化建議程式工具和原生編譯建議程式工具產生的報表加以比較，以確認報表的精確度。 如需相關資訊，請參閱 [Memory Optimization Advisor](../../relational-databases/in-memory-oltp/memory-optimization-advisor.md) 及 [Native Compilation Advisor](../../relational-databases/in-memory-oltp/native-compilation-advisor.md)。  
  
**使用 SQL Server PowerShell 產生移轉檢查清單**  
  
1.  在 [物件總管]  中，按一下資料庫然後再按一下 [啟動 PowerShell]  。 確認顯示下列提示。  
  
    ```  
    PS SQLSERVER: \SQL\{Instance Name}\DEFAULT\Databases\{two-part DB Name}>  
    ```  
  
2.  輸入下列命令。  
  
    ```  
    Save-SqlMigrationReport -FolderPath "<folder_path>"  
    ```  
  
3.  驗證下列項目。  
  
    -   建立資料夾路徑 (若其不存在)。  
  
    -   系統會針對資料庫中的所有資料表和預存程序產生移轉檢查清單報表，且報表會位於 folder_path 中的指定位置。  
  
**使用 Windows PowerShell 產生移轉檢查清單**  
  
1.  啟動更高權限的 Windows PowerShell 工作階段。  
  
2.  輸入下列命令。 物件可以是資料表或預存程序。  
  
    ```  
    [System.Reflection.Assembly]::LoadWithPartialName('Microsoft.SqlServer.SMO')  
  
    ```  
  
    ```  
    Save-SqlMigrationReport -Server "<instance_name>" -Database "<db_name>" -FolderPath "<folder_path1>"  
  
    ```  
  
    ```  
    Save-SqlMigrationReport -Server "<instance_name>" -Database "<db_name>" -Object <object_name> -FolderPath "<folder_path2>"  
  
    ```  
  
3.  驗證下列項目。  
  
    -   系統會針對資料庫中的所有資料表和預存程序產生移轉檢查清單報表，且報表會位於 folder_path 中的指定位置。  
  
    -   <object_name> 的移轉檢查清單報表，是 folder_path2 所指定位置中的唯一報表。  
  
## <a name="see-also"></a>另請參閱  
 [移轉至 In-Memory OLTP](../../relational-databases/in-memory-oltp/migrating-to-in-memory-oltp.md)  
  
  
