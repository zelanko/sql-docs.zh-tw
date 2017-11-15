---
title: "執行程序邏輯和實體運算子參考 | Microsoft 文件"
ms.custom: 
ms.date: 10/12/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.showplan.leftouterjoin.f1
- sql13.swb.showplan.remotedelete.f1
- sql13.swb.showplan.parallelism.f1
- sql13.swb.showplan.indexspool.f1
- sql13.swb.showplan.result.f1
- sql13.swb.showplan.bitmapcreate.f1
- sql13.swb.showplan.remotescan.f1
- sql13.swb.showplan.union.f1
- sql13.swb.showplan.bitmap.f1
- sql13.swb.showplan.RIDLookup
- sql13.swb.showplan.innerjoin.f1
- sql13.swb.showplan.dynamic.f1
- sql13.swb.showplan.distributestreams.f1
- sql13.swb.showplan.clusteredindexdelete.f1
- sql13.swb.showplan.keylookup.f1
- sql13.swb.showplan.partialaggregate.f1
- sql13.swb.showplan.distinctsort.f1
- sql13.swb.showplan.collapse.f1
- sql13.swb.showplan.print.f1
- sql13.swb.showplan.crossjoin.f1
- sql13.swb.showplan.convert.f1
- sql13.swb.showplan.split.f1
- sql13.swb.showplan.top.f1
- sql13.swb.showplan.update.f1
- sql13.swb.showplan.keyset.f1
- sql13.swb.showplan.fetchquery.f1
- sql13.swb.showplan.mergejoin.f1
- sql13.swb.showplan.branchrepartition.f1
- sql13.swb.showplan.tableinsert.f1
- sql13.swb.showplan.clusteredindexseek.f1
- sql13.swb.showplan.indexupdate.f1
- sql13.swb.showplan.indexinsert.f1
- sql13.swb.showplan.clusteredindexupdate.f1
- sql13.swb.showplan.streamaggregate.f1
- sql13.swb.showplan.columnstoreindexdelete.f1
- sql13.swb.showplan.snapshot.f1
- sql13.swb.showplan.remotequery.f1
- sql13.swb.showplan.constantscan.f1
- sql13.swb.showplan.rank.f1
- sql13.swb.showplan.rightsemijoin.f1
- sql13.swb.showplan.delete.f1
- sql13.swb.showplan.sequence.f1
- sql13.swb.showplan.locate.f1
- sql13.swb.showplan.aggregate.f1
- sql13.swb.showplan.rightouterjoin.f1
- sql13.swb.showplan.columnstoreindexupdate.f1
- sql13.swb.showplan.clusteredindexinsert.f1
- sql13.swb.showplan.rowcountspool.f1
- sql13.swb.showplan.columnstoreindexscan.f1
- sql13.swb.showplan.leftantisemijoin.f1
- sql13.swb.showplan.sort.f1
- sql13.swb.showplan.leftsemijoin.f1
- sql13.swb.showplan.columnstoreindexinsert.f1
- sql13.swb.showplan.indexscan.f1
- sql13.swb.showplan.columnstoreindexmerge.f1
- sql13.swb.showplan.lazyspool.f1
- sql13.swb.showplan.rightantisemijoin.f1
- sql13.swb.showplan.bookmarklookup.f1
- sql13.swb.showplan.remoteinsert.f1
- sql13.swb.showplan.intrinsic.f1
- sql13.swb.showplan.arithmeticexpression.f1
- sql13.swb.showplan.populationquery.f1
- sql13.swb.showplan.filter.f1
- sql13.swb.showplan.if.f1
- sql13.swb.showplan.hashmatchteam.f1
- sql13.swb.showplan.tablevaluedfunction.f1
- sql13.swb.showplan.assign.f1
- sql13.swb.showplan.nestedloops.f1
- sql13.swb.showplan.buildhash.f1
- sql13.swb.showplan.mergeinterval.f1
- sql13.swb.showplan.hashmatch.f1
- sql13.swb.showplan.parametertablescan.f1
- sql13.swb.showplan.tablemerge.f1
- sql13.swb.showplan.switch.f1
- sql13.swb.showplan.sql.f1
- sql13.swb.showplan.repartitionstreams.f1
- sql13.swb.showplan.logrowscan.f1
- sql13.swb.showplan.assert.f1
- sql13.swb.showplan.computescalar.f1
- sql13.swb.showplan.broadcast.f1
- sql13.swb.showplan.indexseek.f1
- sql13.swb.showplan.gatherstreams.f1
- sql13.swb.showplan.remoteindexscan.f1
- sql13.swb.showplan.segment.f1
- sql13.swb.showplan.tableupdate.f1
- sql13.swb.showplan.clusteredindexscan.f1
- sql13.swb.showplan.cache.f1
- sql13.swb.showplan.spool.f1
- sql13.swb.showplan.indexdelete.f1
- sql13.swb.showplan.distinct.f1
- sql13.swb.showplan.deletedscan.f1
- sql13.swb.showplan.eagerspool.f1
- sql13.swb.showplan.hashmatchroot.f1
- sql13.swb.showplan.setfunction.f1
- sql13.swb.showplan.clusteredindexmerge.f1
- sql13.swb.showplan.flowdistinct.f1
- sql13.swb.showplan.tabledelete.f1
- sql13.swb.showplan.tablescan.f1
- sql13.swb.showplan.refreshquery.f1
- sql13.swb.showplan.tablespool.f1
- sql13.swb.showplan.insertedscan.f1
- sql13.swb.showplan.insert.f1
- sql13.swb.showplan.remoteindexseek.f1
- sql13.swb.showplan.fullouterjoin.f1
- sql13.swb.showplan.declare.f1
- sql13.swb.showplan.udx.f1
- sql13.swb.showplan.while.f1
- sql13.swb.showplan.remoteupdate.f1
- sql13.swb.showplan.concatenation.f1
- sql13.swb.showplan.computescalar
helpviewer_keywords:
- execution plans [SQL Server], operators
- ActualRows attribute
- reading execution plan output
- ActualRewinds attribute
- ActualEndOfScans attribute
- query tuning [SQL Server]
- mapping operators [SQL Server]
- operators [Database Engine query tuning]
- logical operators [SQL Server], execution plans
- logical operators [SQL Server], listed
- physical operators [SQL Server]
- ActualRebinds attribute
- execution plans [SQL Server], reading output
ms.assetid: e43fd0fe-5ea7-4ffe-8d52-759ef6a7c361
caps.latest.revision: "51"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 80ad5d780193ef6a540dccb2f78fd2e5002a3eb7
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="showplan-logical-and-physical-operators-reference"></a>執行程序邏輯和實體運算子參考
  運算子說明 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 如何執行查詢或資料操作語言 (DML) 陳述式。 查詢最佳化工具會使用運算子來建立查詢計畫，以便建立查詢所指定的結果，或執行 DML 陳述式所指定的作業。 查詢計畫是由實體運算子所組成的樹狀目錄。 您可使用 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]中的圖形執行計畫選項 SET SHOWPLAN 陳述式，以及 SQL Server Profiler Showplan 事件類別，檢視查詢計畫。  
  
 運算子可分為邏輯與實體運算子兩種。  
  
 **邏輯運算子**  
 邏輯運算子說明用來處理陳述式的關聯式代數作業。 換句話說，邏輯運算子可就概念上說明需要執行哪項作業。  
  
 **實體運算子**  
 實體運算子會實作邏輯運算子所描述的作業。 每個實體運算子都是執行作業的物件或常式。 例如，有些實體運算子會從資料表、索引或檢視表中存取資料行或資料列。 其他實體運算子則會執行其他操作，如計算、彙總、資料完整性檢查或聯結。 實體運算子會有上述項目的相關成本。  
  
 實體運算子可進行初始化、收集資料及關閉。 特別是，實體運算子可回應下列三種方法呼叫：  
  
-   **Init()**： **Init()** 方法會使實體運算子自行初始化，並設定任何必要的資料結構。 實體運算子可接收許多 **Init()** 呼叫，但通常實體運算子只會接收一個。  
  
-   **GetNext()**： **GetNext()** 方法會使實體運算子取得資料的第一個或下一個資料列。 實體運算子可能會接收零個或許多 **GetNext()** 呼叫。  
  
-   **Close()**： **Close()** 方法會使實體運算子執行某些清除作業並自行關閉。 實體運算子只會接收一個 **Close()** 呼叫。  
  
 **GetNext()** 方法會傳回一列資料，而它被呼叫的次數會在使用 SET STATISTICS PROFILE ON or SET STATISTICS XML ON 所產生的「執行程序表」輸出中顯示為 **ActualRows**。 如需這些 SET 選項的詳細資訊，請參閱 [SET STATISTICS PROFILE &#40;Transact-SQL&#41;](../t-sql/statements/set-statistics-profile-transact-sql.md) 和 [SET STATISTICS XML &#40;Transact-SQL&#41;](../t-sql/statements/set-statistics-xml-transact-sql.md)。  
  
 「執行程序表」輸出中顯示的 **ActualRebinds** 和 **ActualRewinds** 計數代表 **Init()** 方法被呼叫的次數。 除非運算子位於迴圈聯結的內部，否則 **ActualRebinds** 會等於一，而 **ActualRewinds** 會等於零。 如果運算子位於迴圈聯結的內部，重新繫結和倒轉數目的總和應該會等於聯結外部所處理的資料列數目。 重新繫結是指聯結中有一或多個相互關聯的參數發生變更，而必須重新評估內部。 倒轉是指相互關聯的參數沒有發生變更，先前的內部結果集可供重複使用。  
  
 **ActualRebinds** 和 **ActualRewinds** 會顯示在使用 SET STATISTICS XML ON 產生的「XML 執行程序表」輸出中。 他們只會填入「非叢集索引多工緩衝處理」、「選端查詢」、「資料列計數多工緩衝處理」、「排序」、「資料表多工緩衝處理」以及「資料表值函式」運算子中。 當 **StartupExpression** 屬性設為 TRUE 時，**ActualRebinds** 和 **ActualRewinds** 也會填入「判斷」和「篩選」運算子。  
  
 「XML 執行程序表」中有 **ActualRebinds** 和 **ActualRewinds** 時，您可將它們與 **EstimateRebinds** 和 **EstimateRewinds** 做比較。 如果沒有，則可將估計的資料列數目 (**EstimateRows**) 和實際資料列數目 (**ActualRows**) 做比較。 請注意，如果沒有實際重新繫結和實際倒轉，實際圖形「執行程序表」輸出便會顯示零。  
  
 只有當「執行程序表」輸出是以 SET STATISTICS XML ON 產生時，才可使用相關的計數器 **ActualEndOfScans**。 每當實體運算子存取至其資料流結尾時，此計數器就會累加 1。 實體運算子可存取其資料流結尾零次、一次或多次。 如同重新繫結和倒轉，只有當運算子位於迴圈聯結內部時，結尾掃描次數才能大於 1。 結尾掃描次數應小於或等於重新繫結和倒轉的數目總和。  
  
## <a name="mapping-physical-and-logical-operators"></a>對應實體與邏輯運算子  
 查詢最佳化工具會將查詢計畫建立為由邏輯運算子所組成的樹狀目錄。 在查詢最佳化工具建立計畫之後，它會為每個邏輯運算子選擇最有效率的實體運算子。 查詢最佳化工具會使用以成本為基礎的方法，判斷哪個實體運算子將實作邏輯運算子。  
  
 一個邏輯運算子通常可由多個實體運算子實作。 不過，在極少數的情況下，實體運算子也可以實作多個邏輯運算子。  
  
## <a name="operator-descriptions"></a>運算子描述  
 本節包含邏輯與實體運算子的說明：  
  
|圖形執行計畫圖示|Showplan 運算子|Description|  
|-----------------------------------|-----------------------|-----------------|  
|![自適性聯結運算子圖示](../relational-databases/media/AdaptiveJoin.gif "自適性聯結運算子圖示")|**自適性聯結**|**自適性聯結**運算子可讓選擇的雜湊聯結或巢狀迴圈聯結方法，延後到已掃描的第一個輸入之後。 | 
|無|**Aggregate**|**Aggregate** 運算子會計算包含 MIN、MAX、SUM、COUNT 或 AVG 的運算式。 **Aggregate** 運算子可以是邏輯運算子或實體運算子。|  
|![算術運算式運算子圖示](../relational-databases/media/arithmetic-expression-32x-2.gif "算術運算式運算子圖示")|**算術運算式**|「算術運算式」運算子會從資料列中現有的值計算出新的值。 「算術運算式」無法用於 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 中。|  
|![判斷提示運算子圖示](../relational-databases/media/assert-32x.gif "判斷提示運算子圖示")|**判斷提示**|「判斷提示」運算子會驗證條件。 例如，它會驗證參考完整性，或確定純量子查詢傳回一個資料列。 「判斷提示」運算子會針對每個輸入資料列來評估執行計畫之 **Argument** 資料行中的運算式。 如果這個運算式評估為 NULL，代表資料列通過「判斷提示」運算子的驗證，則查詢會繼續執行。 如果這個運算式得出非 Null 值，就會得出相對的錯誤。 「判斷提示」運算子是實體運算子。|  
|![指派語言項目圖示](../relational-databases/media/assign-32.gif "指派語言項目圖示")|**指派**|「指派」運算子會將運算式的值或常數指派給變數。 「指派」是語言元素。|  
|無|**Asnyc Concat**|**Asnyc Concat** 運算子只能使用於遠端查詢 (分散式查詢)。 它有 *n* 個子節點和一個父節點。 一般來說，某些子節點是參與分散式查詢的遠端電腦。 **Asnyc Concat** 會同時向所有子節點發出 `open()` 呼叫，然後再將點陣圖套用到每個子節點。 **Async Concat** 會針對每一個是 1 的位元，視需要將輸出資料列傳送給父節點。|  
|![點陣圖運算子圖示](../relational-databases/media/bitmap-32x.gif "點陣圖運算子圖示")|**點陣圖**|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 會使用「點陣圖」運算子來實作平行查詢計畫中的點陣圖篩選。 點陣圖篩選可先透過消除其索引鍵值無法產生任何聯結記錄的資料列來加速執行查詢，然後再透過另一個運算子 (如「平行處理原則」運算子) 傳遞資料列。 點陣圖篩選會於運算子樹狀目錄的一部分，以精簡方式顯示資料表中的一組值，以便從此樹狀目錄的另一個部分篩選第二個資料表中的資料列。 藉由盡早移除查詢中的不必要資料列，後續的運算子需要處理的資料列就會更少，而查詢的整體效能也會提升。 最佳化工具會判斷點陣圖何時具有足夠的選擇性能夠充分運用以及將篩選套用到哪個運算子。 「點陣圖」是實體運算子。|  
|![點陣圖運算子圖示](../relational-databases/media/bitmap-32x.gif "點陣圖運算子圖示")|**點陣圖建立**|「點陣圖建立」運算子會出現在建立點陣圖的 Showplan 輸出中。 **點陣圖建立** 是邏輯運算子。|  
|![書籤查閱運算子圖示](../relational-databases/media/bookmark-lookup-32x.gif "書籤查閱運算子圖示")|**書籤查閱**|「書籤查閱」運算子使用書籤 (資料列識別碼或叢集索引鍵) 在資料表或叢集索引中查詢對應的資料列。 **Argument** 資料行中包含用來在資料表或叢集索引中查詢資料列的書籤標記。 **Argument** 資料行中也包含查詢資料列的資料表或叢集索引的名稱。 如果 **Argument** 資料行中出現 WITH PREFETCH 子句，表示查詢處理器已決定在資料表或叢集索引中查詢書籤時，使用非同步預先提取 (預先讀取) 是最佳方法。<br /><br /> 「書籤查閱」無法用於 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 中。 不過，[叢集索引搜尋] 和 [RID 查閱] 會提供書籤查閱功能。 「索引鍵查閱」運算子也提供這項功能。|  
|無|**分支重新分割**|在平行查詢計畫中，有時候會有 Iterator 的概念區。 在這種區域內的所有 Iterator，都可以由平行執行緒來執行。 區域本身必須連續執行。 個別區域內的一些「平行處理原則」Iterator，稱作「分支重新分割」。 在兩個這種區域的界限上的「平行處理原則」Iterator，稱作「區段重新分割」。 「分支重新分割」和「區段重新分割」都是邏輯運算子。|  
|無|**廣播**|**廣播**有一個子節點及 *n* 個父節點。 「廣播」會依要求將其輸入資料列傳送至多位取用者。 每位取用者都會收到所有資料列。 例如，若所有取用者都是雜湊聯結的建立者，則會建立 *n* 份雜湊資料表。|  
|![建立雜湊運算子圖示](../relational-databases/media/build-hash.gif "建立雜湊運算子圖示")|**建立雜湊**|指示建立 xVelocity 記憶體最佳化的資料行存放區索引之批次雜湊資料表。|  
|無|**Cache**|「快取」是特殊版的「多工緩衝處理」運算子。 它只儲存一列資料。 「快取」是邏輯運算子。 「快取」無法用於 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 中。|  
|![叢集索引刪除運算子圖示](../relational-databases/media/clustered-index-delete-32x.gif "叢集索引刪除運算子圖示")|**叢集索引刪除**|「叢集索引刪除」運算子會從查詢執行計畫之 Argument 資料行所指定的叢集索引中刪除資料列。 如果 Argument 資料行中出現 WHERE:() 述詞，就只會刪除滿足述詞的資料列。「叢集索引刪除」是實體運算子。|  
|![叢集索引插入運算子圖示](../relational-databases/media/clustered-index-insert-32x.gif "叢集索引插入運算子圖示")|**叢集索引插入**|「叢集索引插入」執行程序表運算子會將其輸入的資料列插入 Argument 資料行所指定的叢集索引中。 Argument 資料行也包含 SET:() 述詞，指出每一個資料行設定的值。 如果「叢集索引插入」沒有插入值的子系，則會從「插入」運算子本身取得插入的資料列。「叢集索引插入」是實體運算子。|  
|![叢集索引合併運算子](../relational-databases/media/clustered-index-merge-32x.gif "叢集索引合併運算子")|**叢集索引合併**|「叢集索引合併」運算子會將合併資料流套用到叢集索引。 此運算子會從運算子之 **Argument** 資料行內所指定的叢集索引中刪除、更新或插入資料列。 所執行的實際作業取決於運算子之 **Argument** 資料行內指定之 **ACTION** 資料行的執行階段值。 「叢集索引合併」是實體運算子。|  
|![叢集索引掃描運算子圖示](../relational-databases/media/clustered-index-scan-32x.gif "叢集索引掃描運算子圖示")|**叢集索引掃描**|「叢集索引掃描」運算子會掃描查詢執行計畫的 Argument 資料行中指定的叢集索引。 出現選擇性的 WHERE:() 述詞時，只會傳回滿足述詞的資料列。 如果 Argument 資料行中包含 ORDERED 子句，表示查詢處理器要求資料列的輸出須按叢集索引的排序次序傳回。 如果沒有 ORDERED 子句，儲存引擎會以最佳方式搜尋索引，而不需要排序輸出。 「叢集索引掃描」是邏輯與實體運算子。|  
|![叢集索引搜尋運算子圖示](../relational-databases/media/clustered-index-seek-32x.gif "叢集索引搜尋運算子圖示")|**叢集索引搜尋**|「叢集索引搜尋」運算子使用索引的搜尋能力，從叢集索引中擷取資料列。 **Argument** 資料行包含所使用的叢集索引名稱，及 SEEK:() 述詞。 儲存引擎會使用索引來處理滿足這個 SEEK:() 述詞的資料列。 也可以包含 WHERE:() 述詞，讓儲存引擎針對滿足 SEEK:() 述詞的所有資料列進行評估，但此為選擇性，且不使用索引來完成此程序。<br /><br /> 如果 **Argument** 資料行包含 ORDERED 子句，表示查詢處理器已決定，資料列的傳回順序必須依叢集索引的排序次序。 如果沒有 ORDERED 子句，儲存引擎會以最佳方式搜尋索引，不需要將輸出排序。 讓輸出維持次序會比產生不按次序的輸出更沒效率。 出現關鍵字 LOOKUP 時，表示正在執行書籤查閱。 在 [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] 和更新版本中，「索引鍵查閱」運算子會提供書籤查閱功能。 「叢集索引搜尋」是邏輯與實體運算子。|  
|![叢集索引更新運算子圖示](../relational-databases/media/clustered-index-update-32x.gif "叢集索引更新運算子圖示")|**叢集索引更新**|「叢集索引更新」運算子會更新 **Argument** 資料行中所指定之叢集索引內的輸入資料列。如果出現 WHERE:() 述詞，就只會更新滿足這個述詞的資料列。 如果出現 SET:() 述詞，則每個更新的資料行都會設為這個值。 如果出現 DEFINE:() 述詞，就會列出這個運算子定義的數值。 在 SET 子句中或這個運算子中以及這個查詢中的其他位置，都可以參考這些數值。 「叢集索引更新」是邏輯與實體運算子。|  
|![摺疊運算子圖示](../relational-databases/media/collapse-32x.gif "摺疊運算子圖示")|**摺疊**|「摺疊」運算子可最佳化更新處理。 執行更新時，它可以分割成 (使用「分割」運算子) 刪除與插入。 **Argument** 資料行包含指定索引鍵資料行清單的 GROUP BY:() 子句。 如果查詢處理器發現了刪除及插入相同索引鍵值的相鄰資料列，會以更有效率的單一更新作業來取代這些不同的作業。 「摺疊」是邏輯與實體運算子。|  
|![資料行存放區索引掃描](../relational-databases/media/columnstoreindexscan.gif "資料行存放區索引掃描")|**資料行存放區索引掃描**|「資料行存放區索引掃描」運算子會掃描查詢執行計畫之 **Argument** 資料行中所指定的資料行存放區索引。|  
|![計算純量運算子圖示](../relational-databases/media/compute-scalar-32x.gif "計算純量運算子圖示")|**Compute Scalar**|「計算純量」運算子會評估運算式，以產生計算的純量值。 然後可能會將此值傳回給使用者，或由查詢的其他地方來參考，或兩者皆是。 例如在篩選述詞或聯結述詞中，就會見到這兩種情況。 「計算純量」是邏輯與實體運算子。<br /><br /> 執行程序表中出現的「計算純量」運算子可能不會包含 **RunTimeInformation** 元素。 在圖形化的執行程序表中，當選取 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 中的 [包括實際執行計畫] 選項時，[實際資料列]、[實際重新繫結] 與 [實際倒轉] 可能不會顯示在 [屬性] 視窗中。 發生此情況時，表示這些運算子雖然用於編譯的執行計畫中，它們的作用是由即時查詢計畫中的其他運算子執行。 同時也請注意，由 SET STATISTICS PROFILE 產生的「執行程序表」輸出中的執行數目，等於由 SET STATISTICS XML 產生的「執行程序表」中重新繫結和倒轉的總和。|  
|![串連運算子圖示](../relational-databases/media/concatenation-32x.gif "串連運算子圖示")|**串連**|「串連」運算子會掃描多個輸入，並傳回每一個掃描的資料列。 「串連」通常用來實作 [!INCLUDE[tsql](../includes/tsql-md.md)] UNION ALL 建構。 「串連」實體運算子有兩個以上的輸入和一個輸出。 串連作業會將資料列從第一個輸入資料流複製到輸出資料流，再對其他每一個輸入資料流重複此作業。 「串連」是邏輯與實體運算子。|  
|![固定掃描運算子圖示](../relational-databases/media/constant-scan-32x.gif "固定掃描運算子圖示")|**固定掃描**|「固定掃描」運算子會在查詢中加入固定的一列或多列。 「計算純量」運算子通常用於「固定掃描」之後，可以將資料行加入由「固定掃描」運算子所產生的資料列。|  
|![轉換 (資料庫引擎) 語言項目圖示](../relational-databases/media/convert-32x.gif "轉換 (資料庫引擎) 語言項目圖示")|**轉換**|「轉換」運算子可將某個純量資料類型轉換為另一個資料類型。 「轉換」是語言元素。|  
|無|**交叉聯結**|「交叉聯結」運算子會將第一個 (頂端) 輸入的每一列與第二個 (底部) 輸入的每一列相聯結。 **交叉聯結** 是邏輯運算子。|  
|![資料指標 catchall 資料指標運算子圖示](../relational-databases/media/cursor-catch-all.gif "資料指標 catchall 資料指標運算子圖示")|**雜物箱**|產生圖形執行程序表的邏輯若找不到適當的 Iterator 圖示，就會顯示 [雜物箱] 圖示。 [雜物箱] 圖示不一定會指出錯誤條件。 [雜物箱] 圖示有三種：藍色 (Iterator)、橙色 (資料指標) 與綠色 ( [!INCLUDE[tsql](../includes/tsql-md.md)] 語言項目)。|  
|無|**資料指標**|「資料指標」邏輯與實體運算子可用來說明與資料指標作業有關的查詢或更新將如何執行。 實體運算子是說明用來處理資料指標的實體實作演算法，例如使用索引鍵集衍生資料指標。 資料指標執行的每個步驟都有一個實體運算子。 邏輯運算子會說明資料指標的屬性，如資料指標是唯讀的。<br /><br /> 邏輯運算子包括非同步、開放式、主要、唯讀、捲動鎖定及次要與同步。<br /><br /> 實體運算子包括動態、提取查詢、索引鍵集、母體擴展查詢、重新整理查詢與快照集。|  
|![宣告語言項目圖示](../relational-databases/media/declare-32x.gif "宣告語言項目圖示")|**宣告**|「宣告」運算子會在查詢計畫中配置區域變數。 「宣告」是語言元素。|  
|![刪除 (資料庫引擎) 運算子圖示](../relational-databases/media/delete-32x.gif "刪除 (資料庫引擎) 運算子圖示")|**Delete**|會從滿足 **Argument** 資料行之選擇性述詞的物件資料列，刪除「刪除」運算子。|  
|![刪除掃描運算子圖示](../relational-databases/media/delete-scan-32x.gif "刪除掃描運算子圖示")|**刪除的掃描**|「刪除的掃描」運算子會掃描觸發程序中已刪除的資料表。|  
|無|**Distinct**|「相異」運算子可從資料列集或從值集合移除重複的項目。 「相異」是邏輯運算子。|  
|無|**相異排序**|「相異排序」邏輯運算子會掃描輸入，移除重複項，並依 **Argument** 資料行中 DISTINCT ORDER BY:() 述詞所指定的資料行排序。 **相異排序** 是邏輯運算子。|  
|![散發資料流平行處理原則運算子圖示](../relational-databases/media/parallelism-distribute-stream.gif "散發資料流平行處理原則運算子圖示")|**散發資料流**|「散發資料流」運算子只用於平行查詢計畫。 「散發資料流」運算子會採用記錄的單一輸入資料流，並產生多個輸出資料流。 記錄內容與格式不會變更。 輸入資料流中的每筆資料錄都會出現在一個輸出資料流中。 這個運算子會自動在輸出資料流中保留輸入資料錄的關聯次序。 通常是利用雜湊方式來決定特定輸入資料錄應屬於哪個輸出資料流。<br /><br /> 如果輸出經過分割的話，**Argument** 資料行中會包含 PARTITION COLUMNS:() 述詞與分割資料行。 「散發資料流」是邏輯運算子。|  
|![動態資料指標運算子圖示](../relational-databases/media/dynamic-32x.gif "動態資料指標運算子圖示")|**動態**|「動態」運算子採用的資料指標，可以看到其他人進行的所有變更。|  
|![多工緩衝處理運算子圖示](../relational-databases/media/spool-32x.gif "多工緩衝處理運算子圖示")|**急切的多工緩衝處理**|「急切的多工緩衝處理」運算子會取用整個輸入，將每一列儲存在 **tempdb** 資料庫的隱藏暫存物件中。 如果倒轉運算子 (例如，利用「巢狀迴圈」運算子)，但是不需要重新繫結，會使用多工緩衝處理資料，而非重新掃描輸入。 如果必須重新繫結的話，就丟棄多工緩衝處理的資料，然後重新掃描 (重新繫結) 輸入以重建多工緩衝處理物件。 「急切的多工緩衝處理」運算子會以「急切的」方式建立多工緩衝處理檔案：當多工緩衝處理的父系運算子要求第一列時，「多工緩衝處理」運算子會消耗其輸入運算子的所有資料列，並將它們儲存在多工緩衝處理中。 **急切的多工緩衝處理** 是邏輯運算子。|  
|![提取查詢資料指標運算子圖示](../relational-databases/media/fetch-query-32x.gif "提取查詢資料指標運算子圖示")|**提取查詢**|「提取查詢」運算子會在對資料指標發出提取時擷取資料列。|  
|![篩選 (資料庫引擎) 運算子圖示](../relational-databases/media/filter-32x.gif "篩選 (資料庫引擎) 運算子圖示")|**篩選**|「篩選」運算子會掃描輸入，只傳回滿足 **Argument** 資料行中篩選運算式 (述詞) 的資料列。|  
|無|**流程相異**|「流程相異」邏輯運算子會掃描輸入，移除重複的項目。 「相異」運算子會在產生任何輸出之前就先取用所有輸入，「流程相異」運算子則會每取得一個輸入資料列就傳回一列 (除非該資料列重複，若遇到這種情況，則會將其捨棄)。|  
|無|**完整外部聯結**|「完整外部聯結」邏輯運算子所傳回的每個資料列，皆滿足第一個 (上方) 輸入的聯結述詞與第二個 (下方) 輸入的每一個資料列相聯結。 它也會傳回以下資料列：<br /><br /> - 第一個輸入中與第二個輸入完全不符合者。<br /><br /> - 第二個輸入中與第一個輸入完全不符合者。<br /><br /> 不包含相符值的輸入會以 Null 值傳回。 **完整外部聯結** 是邏輯運算子。|  
|![蒐集資料流平行處理原則運算子圖示](../relational-databases/media/parallelism-32x.gif "蒐集資料流平行處理原則運算子圖示")|**蒐集資料流**|「蒐集資料流」運算子僅用於平行查詢計畫中。 「蒐集資料流」運算子會耗用數個輸入資料流，並將輸入資料流合併而產生記錄的單一輸出資料流。 記錄內容與格式不會變更。 若此運算子要保留順序，那麼所有輸入資料流都必須排序好。 若輸出經過排序，則 **Argument** 資料行中會包含 ORDER BY:() 述詞，以及要排序的資料行名稱。 **蒐集資料流** 是邏輯運算子。|  
|![雜湊比對運算子圖示](../relational-databases/media/hash-match-32x.gif "雜湊比對運算子圖示")|**雜湊比對**|「雜湊比對」運算子會根據其建立的輸入，為每一資料列計算雜湊值，以建立雜湊資料表。 **Argument** 資料行會出現 HASH:() 述詞，以及用來建立雜湊值的資料行清單。 然後它會為每個探查列 (視情況) 建立雜湊值 (使用相同的雜湊函數)，並在雜湊資料表中尋找符合者。 如果出現殘餘述詞 (由 **Argument** 資料行中的 RESIDUAL:() 識別)，那麼也必須滿足該述詞，這樣該資料列才算符合。 行為取決於正在執行的邏輯作業：<br /><br /> - 若為任何聯結，則使用第一個 (頂端) 輸入來建立雜湊資料表，使用第二個 (底端) 輸入來探查雜湊資料表。 輸出相符 (或不符合) 由聯結類型規定。 如果多個聯結使用相同的聯結行，這些作業會組成一組成為雜湊群。<br /><br /> - 若為相異運算子或彙總運算子，則使用輸入來建立雜湊資料表 (移除重複項，並計算任何彙總運算式)。 建立雜湊資料表時，會掃描資料表並輸出所有項目。<br /><br /> - 若為等位運算子，則使用第一個輸入來建立雜湊資料表 (移除重複項)。 使用第二個輸入 (必須沒有重複項) 探查雜湊資料表，傳回不符合的所有資料列，然後掃描雜湊資料表，並傳回所有項目。<br /><br /> 「點陣圖」是實體運算子。|  
|![如果語言項目圖示](../relational-databases/media/if-32x.gif "如果語言項目圖示")|**如果**|「如果」運算子會依據運算式執行條件式處理。 「如果」是語言元素。|  
|無|**內部聯結**|「內部聯結」邏輯運算子所傳回的每個資料列，皆滿足第一個 (上方) 輸入與第二個 (下方) 輸入的聯結。|  
|![插入 (資料庫引擎) 運算子圖示](../relational-databases/media/insert-32x.gif "插入 (資料庫引擎) 運算子圖示")|**Insert**|「插入」邏輯運算子會將輸入的每一個資料列，插入 **Argument** 資料行中指定的物件。 實體運算子是「資料表插入」、「索引插入」或「叢集索引插入」運算子。|  
|![插入的掃描運算子圖示](../relational-databases/media/inserted-scan-32x.gif "插入的掃描運算子圖示")|**插入的掃描**|「插入的掃描」運算子會掃描 **inserted** 資料表。 「插入的掃描」是邏輯與實體運算子。|  
|![內建語言項目圖示](../relational-databases/media/intrinsic-32x.gif "內建語言項目圖示")|**內建**|「內建」運算子會叫用內部 [!INCLUDE[tsql](../includes/tsql-md.md)] 函數。 「內建」是語言元素。|  
![迭代器 catchall 運算子圖示](../relational-databases/media/iterator-catch-all.gif "迭代器 catchall 運算子圖示")|**Iterator**|產生圖形執行程序表的邏輯若找不到適當的 Iterator 圖示，就會顯示 **Iterator** 雜物箱圖示。 [雜物箱] 圖示不一定會指出錯誤條件。 [雜物箱] 圖示有三種：藍色 (Iterator)、橙色 (資料指標) 與綠色 ( [!INCLUDE[tsql](../includes/tsql-md.md)] 語言建構)。|  
|![書籤查閱運算子圖示](../relational-databases/media/bookmark-lookup-32x.gif "書籤查閱運算子圖示")|**索引鍵查閱**|「索引鍵查閱」運算子可在包含叢集索引的資料行上進行書籤查閱。 **Argument** 資料行包含叢集索引的名稱和叢集索引鍵，可用來查閱叢集索引中的資料列。 「索引鍵查閱」一律都會伴隨「巢狀迴圈」運算子。 如果 **Argument** 資料行中出現 WITH PREFETCH 子句，表示查詢處理器已決定在叢集索引中查詢書籤時，使用非同步預先提取 (預先讀取) 是最佳方法。<br /><br /> 在查詢計畫中使用「索引鍵查閱」運算子，表示查詢可以進行效能微調。 例如，您可以加入涵蓋索引來提高查詢效能。|  
|![索引鍵集資料指標運算子圖示](../relational-databases/media/keyset-32x.gif "索引鍵集資料指標運算子圖示")|**索引鍵集**|「索引鍵集」運算子使用可以查看更新，但無法插入其他人所製作的資料指標。|  
|![語言項目 catchall 圖示](../relational-databases/media/language-construct-catch-all.gif "語言項目 catchall 圖示")|**Language 元素**|「執行程序表」輸出中顯示的 **Language 元素** 雜物箱圖示。 [雜物箱] 圖示不一定會指出錯誤條件。 [雜物箱] 圖示有三種：藍色 (Iterator)、橙色 (資料指標) 與綠色 ( [!INCLUDE[tsql](../includes/tsql-md.md)] 語言建構)。|  
|![多工緩衝處理運算子圖示](../relational-databases/media/spool-32x.gif "多工緩衝處理運算子圖示")|**延遲多工緩衝處理**|「延遲多工緩衝處理」邏輯運算子會將其輸入的每一個資料列，都儲存在 **tempdb** 資料庫內隱藏的暫存物件中。 如果倒轉運算子 (例如，利用「巢狀迴圈」運算子)，但是不需要重新繫結，會使用多工緩衝處理資料，而非重新掃描輸入。 如果必須重新繫結的話，就丟棄多工緩衝處理的資料，然後重新掃描 (重新繫結) 輸入以重建多工緩衝處理物件。 「延遲多工緩衝處理」運算子會以「延遲」方式建立它的多工緩衝處理檔案，也就是說，每次多工緩衝處理的父系運算子要求一個資料列時，多工緩衝處理運算子就會從它的輸入運算子取得一個資料列，然後將它儲存在多工緩衝處理內，而不是一次取用所有資料列。 Lazy Spool 是邏輯運算子。|  
|無|**左方反半聯結**|當第二個 (下方) 輸入中沒有相符的資料列時，「左方反半聯結」運算子將會從第一個 (上方) 輸入傳回每一個資料列。 如果 **Argument** 資料行中沒有聯結述詞，則每一資料列就是一個符合資料列。 **左方反半聯結** 是邏輯運算子。|  
|無|**左外部聯結**|「左外部聯結」邏輯運算子所傳回的每個資料列，皆滿足第一個 (上方) 輸入與第二個 (下方) 輸入的聯結。 它也會傳回第一個輸入中與第二個輸入完全不相符的任何資料列。 第二個輸入中的不符合資料列會以 null 值傳回。 如果 **Argument** 資料行中沒有聯結述詞，則每一資料列就是一個符合資料列。 **左外部聯結** 是邏輯運算子。|  
|無|**左方半聯結**|當第二個 (下方) 輸入中有相符的資料列時，「左方半聯結」運算子將會從第一個 (上方) 輸入傳回每一個資料列。 如果 **Argument** 資料行中沒有聯結述詞，則每一資料列就是一個符合資料列。 **左方半聯結** 是邏輯運算子。|  
|![記錄檔資料列掃描運算子圖示](../relational-databases/media/log-row-scan-32x.gif "記錄檔資料列掃描運算子圖示")|**記錄檔資料列掃描**|「記錄檔資料列掃描」運算子會掃描交易記錄。 「記錄檔資料列掃描」是邏輯與實體運算子。|  
|![合併間隔運算子圖示](../relational-databases/media/merge-interval-32x.gif "合併間隔運算子圖示")|**合併間隔**|「合併間隔」運算子會合併多個 (可能重疊) 間隔以產生最小的非重疊間隔，然後使用這些間隔，尋找索引項目。 這個運算子一般會出現在一或多個「計算純量」運算子上方，重疊在「固定掃描」運算子之上，後者會建構這個運算子所合併的間隔 (以資料列中的資料行代表)。 「合併間隔」是邏輯與實體運算子。|  
|![合併聯結運算子圖示](../relational-databases/media/merge-join-32x.gif "合併聯結運算子圖示")|**合併聯結**|「合併聯結」運算子會執行內部聯結、左方外部聯結、左方半聯結、左方反半聯結、右方外部聯結、右方半聯結、右方反半聯結，以及等位邏輯作業。<br /><br /> 在 **Argument** 資料行中，若要執行一對多的聯結運算，「合併聯結」運算子就要包含 MERGE:() 述詞，若要執行多對多的聯結運算，則要包含 MANY-TO-MANY MERGE:() 述詞。 **Argument** 資料行也包含用來執行運算的逗點分隔資料行清單。 「合併聯結」運算子需要兩個輸入，依個別資料行排序，可能是利用在查詢計畫中明確地插入排序作業。 如果不需要明確的排序，合併聯結會特別有效；例如，如果資料庫中有合適的 B 型樹狀目錄索引，或如果排序次序可以由多個作業利用 (如合併聯結與含積存的分組功能)。 「合併聯結」是實體運算子。|  
|![巢狀迴圈運算子圖示](../relational-databases/media/nested-loops-32x.gif "巢狀迴圈運算子圖示")|**巢狀迴圈**|「巢狀迴圈」運算子執行內部聯結、左方外部聯結、左方半聯結和左方反半聯結邏輯運算。 巢狀迴圈聯結通常會使用索引，在內部資料表中搜尋外部資料表的每個資料列。 查詢處理器會根據預期的成本，決定是否要排序外部輸入，以改進對內部輸入的索引搜尋位置。 任何滿足 **Argument** 資料行中的選擇性述詞的資料列，會根據所執行的邏輯運算而適當地傳回。 「巢狀迴圈」是實體運算子。|  
|![非叢集索引刪除運算子圖示](../relational-databases/media/nonclust-index-delete-32x.gif "非叢集索引刪除運算子圖示")|**非叢集索引刪除**|「非叢集索引刪除」運算子會從 **Argument** 資料行中指定的非叢集索引刪除輸入資料列。 「非叢集索引刪除」是實體運算子。|  
|![非叢集索引插入運算子圖示](../relational-databases/media/nonclust-index-insert-32x.gif "非叢集索引插入運算子圖示")|**索引插入**|「索引插入」運算子會將輸入資料列插入 **Argument** 資料行所指定的非叢集索引中。 **Argument** 資料行也包含 SET:() 述詞，指出每一個資料行設定的值。 「索引插入」是實體運算子。|  
|![非叢集索引掃描運算子圖示](../relational-databases/media/nonclustered-index-scan-32x.gif "非叢集索引掃描運算子圖示")|**索引掃描**|「索引掃描」運算子會擷取 **Argument** 資料行中所指定之非叢集索引的所有資料列。 如果 **Argument** 資料行出現選擇性的 WHERE:() 述詞，就只傳回滿足述詞的資料列。 「索引掃描」是邏輯與實體運算子。|  
|![非叢集索引搜尋運算子圖示](../relational-databases/media/index-seek-32x.gif "非叢集索引搜尋運算子圖示")|**索引搜尋**|「索引搜尋」運算子使用索引的搜尋能力，從非叢集索引中擷取資料列。 **Argument** 資料行中包含所使用的非叢集索引名稱。 它也包含 SEEK:() 述詞。 儲存引擎會使用索引來處理滿足 SEEK:() 述詞的資料列。 它可以選擇包含 WHERE:() 述詞，讓儲存引擎比對所有滿足 SEEK:() 述詞的資料列 (這麼做時不使用索引)。 如果 **Argument** 資料行必須包含 ORDERED 子句，表示查詢處理器已決定傳回的資料列必須依照非叢集索引的排序次序。 如果沒有 ORDERED 子句，儲存引擎會以最適當的方式搜尋索引 (不保證輸出會依序排列)。 讓輸出維持次序會比產生不按次序的輸出還要沒有效率。 「索引搜尋」是邏輯與實體運算子。|  
|![非叢集索引多工緩衝處理運算子圖示](../relational-databases/media/index-spool-32x.gif "非叢集索引多工緩衝處理運算子圖示")|**索引多工緩衝處理**|「索引多工緩衝處理」實體運算子在 **Argument** 資料行中包含 SEEK:() 述詞。 「索引多工緩衝處理」運算子會掃描其輸入資料列，將每一列的副本放入隱藏的多工緩衝處理檔中 (儲存在 **tempdb** 資料庫中，直到查詢結束就不再存在)，並對資料列建立非叢集索引。 這讓您可以使用索引的搜尋能力來輸出滿足 SEEK:() 述詞的資料列。 如果倒轉運算子 (例如，利用「巢狀迴圈」運算子)，但是不需要重新繫結，會使用多工緩衝處理資料，而非重新掃描輸入。|  
|![非叢集索引更新運算子圖示](../relational-databases/media/nonclust-index-update-32x.gif "非叢集索引更新運算子圖示")|**非叢集索引更新**|「非叢集索引更新」實體運算子會在 **Argument** 資料行中指定的非叢集索引內，從它的輸入更新資料列。 如果出現 SET:() 述詞，則每個更新的資料行都會設為這個值。 「非叢集索引更新」是實體運算子。|  
|![線上索引插入運算子圖示](../relational-databases/media/online-index-32x.gif "線上索引插入運算子圖示")|**線上索引插入**|「線上索引插入」實體運算子指出索引之建立、改變或卸除作業將於線上進行。 也就是說，基礎資料表資料在索引操作期間仍然可供使用者使用。|  
|無|**平行處理原則**|**平行處理原則**運算子 (或交換迭代器) 會執行散發資料流、蒐集資料流及重新分割資料流的邏輯作業。 **Argument** 資料行可以包含 PARTITION COLUMNS:() 述詞，以及被分割的資料行清單 (以逗點分隔)。 **Argument** 資料行也可以包含 ORDER BY:() 述詞，用以列出分割期間要保留排序順序的資料行。 「平行處理原則」是實體運算子。 如需平行處理原則運算子的詳細資訊，請參閱 [Craig Freedman 的部落格系列](http://blogs.msdn.microsoft.com/craigfr/tag/parallelism/) \(英文\)。<br /><br />**注意：**如果查詢已經編譯為平行查詢，但在執行階段是以序列查詢的方式執行，則由 SET STATISTICS XML 或使用 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 之 [包括實際執行計劃] 選項所產生的「執行程序表」輸出中，將不會包含**平行處理原則**運算子的 **RunTimeInformation** 元素。 在 SET STATISTICS PROFILE 輸出中，「平行處理原則」運算子的實際資料列計數和實際執行次數會顯示為零。 不論發生的情況為何，都表示「平行處理原則」運算子只用於查詢編譯期間，而不用於執行階段查詢計畫。 請注意，如果伺服器上有大量的並行載入，平行查詢計畫有時會以序列方式執行。|  
|![參數資料表掃描運算子圖示](../relational-databases/media/parameter-table-scan-32x.gif "參數資料表掃描運算子圖示")|**參數資料表掃描**|「參數資料表掃描」運算子會掃描在目前的查詢中當做參數使用的資料表。 一般而言，這是用於預存程序中的 INSERT 查詢。 「參數資料表掃描」是邏輯與實體運算子。|  
|無|**部分彙總**|「部分彙總」用於平行計畫。 它將彙總函式套用至盡可能最多的輸入資料列，因此不需要寫入磁碟 (稱為「溢出」)。 「雜湊比對」是唯一可以實作資料分割彙總的實體運算子 (Iterator)。 **部分彙總** 是邏輯運算子。|  
|![母體擴展查詢資料指標運算子圖示](../relational-databases/media/poulation-query-32x.gif "母體擴展查詢資料指標運算子圖示")|**母體擴展查詢**|「母體擴展查詢」運算子會在開啟資料指標時，擴展資料指標的工作資料表。|  
|![重新整理查詢資料指標運算子圖示](../relational-databases/media/refresh-query-32x.gif "重新整理查詢資料指標運算子圖示")|**重新整理查詢**|「重新整理查詢」運算子會在提取緩衝區中提取資料列目前的資料。|  
|![遠端刪除運算子圖示](../relational-databases/media/remote-delete-32x.gif "遠端刪除運算子圖示")|**遠端刪除**|「遠端刪除」運算子會刪除遠端物件的輸入資料列。 「遠端刪除」是邏輯與實體運算子。|  
|![遠端索引搜尋執行程序表運算子](../relational-databases/media/remote-index-scan-32x.gif "遠端索引搜尋執行程序表運算子")|**遠端索引掃描**|「遠端索引掃描」運算子會掃描 Argument 資料行中所指定的遠端索引。 「遠端索引掃描」是邏輯與實體運算子。|  
|![遠端索引搜尋執行程序表運算子](../relational-databases/media/remote-index-seek-32x.gif "遠端索引搜尋執行程序表運算子")|**遠端索引搜尋**|「遠端索引搜尋」運算子會使用遠端索引物件的搜尋功能來擷取資料列。 **Argument** 資料行包含所使用的遠端索引名稱及 SEEK:() 述詞。 「遠端索引搜尋」是邏輯實體運算子。|  
|![遠端插入運算子圖示](../relational-databases/media/remote-insert-32x.gif "遠端插入運算子圖示")|**遠端插入**|「遠端插入」運算子會將輸入資料列插入遠端物件。 「遠端插入」是邏輯與實體運算子。|  
|![遠端查詢運算子圖示](../relational-databases/media/remote-query-32x.gif "遠端查詢運算子圖示")|**遠端查詢**|「遠端查詢」運算子會對遠端來源送出查詢。 傳給遠端伺服器的查詢文字會出現在 **Argument** 資料行中。 「遠端查詢」是邏輯與實體運算子。|  
|![遠端掃描運算子圖示](../relational-databases/media/remote-scan-32x.gif "遠端掃描運算子圖示")|**遠端掃描**|「遠端掃描」運算子會掃描遠端物件。 遠端物件的名稱會出現在 **Argument** 資料行中。 「遠端掃描」是邏輯與實體運算子。|  
|![遠端更新運算子圖示](../relational-databases/media/remote-update-32x.gif "遠端更新運算子圖示")|**遠端更新**|「遠端更新」運算子會更新遠端物件中的輸入資料列。 「遠端更新」是邏輯與實體運算子。|  
|![重新分割資料流平行處理原則運算子圖示](../relational-databases/media/parallelism-repartition-stream.gif "重新分割資料流平行處理原則運算子圖示")|**重新分割資料流**|**重新分割資料流**運算子 (或交換迭代器) 會消耗多個資料流，並產生多個記錄的資料流。 記錄內容與格式不會變更。 如果查詢最佳化工具使用點陣圖篩選，輸出資料流中的資料列數會減少。 輸入資料流的每個資料錄會被放入一個輸出資料流。 如果這個運算子要保留次序，那麼所有輸入資料流都必須排序好，而且合併成數個排序的輸出資料流。 如果輸出經過分割，則 **Argument** 資料行中會包含 PARTITION COLUMNS:() 述詞與分割資料行。如果輸出經過排序，則 **Argument** 資料行中會包含 ORDER BY:() 述詞，以及要排序的資料行。 **重新分割資料流** 是邏輯運算子。 此運算子只用於平行查詢計畫。| 
|![結果語言項目圖示](../relational-databases/media/result-32x.gif "結果語言項目圖示")|**結果**|「結果」運算子是在查詢計畫結束時所傳回的資料。 這通常是 Showplan 的根元素。 「結果」是語言元素。|  
|![RID 查閱運算子圖示](../relational-databases/media/rid-nonclust-locate-32x.gif "RID 查閱運算子圖示")|**RID 查閱**|「RID 查閱」是堆積上的書籤查閱，它會使用提供的資料列識別碼 (RID)。 **Argument** 資料行包含書籤標籤，可用以查閱資料表中的資料列，以及已查閱過之資料列的資料表名稱。 「RID 查閱」一律都會伴隨 NESTED LOOP JOIN。 「RID 查閱」是實體運算子。 如需書籤查閱的詳細資訊，請參閱 MSDN SQL Server 部落格中的[書籤查閱](http://go.microsoft.com/fwlink/?LinkId=132568)。|  
|無|**右方反半聯結**|「右方反半聯結」運算子會在第一個 (上方) 輸入中沒有符合資料列存在時，輸出第二個 (下方) 輸入中的每一列。 相符合的資料列定義是滿足 **Argument** 資料行中述詞的資料列 (如果沒有任何述詞，則每一列都是相符列)。 **右方反半聯結** 是邏輯運算子。|  
|無|**右外部聯結**|「右外部聯結」運算子所傳回的每個資料列，皆滿足第二個 (下方) 輸入與第一個 (上方) 輸入之每個相符資料列的聯結。 它也會傳回第二個輸入中與第一個輸入完全不相符的任何資料列，以 NULL 相聯結。 如果 **Argument** 資料行中沒有聯結述詞，則每一資料列就是一個符合資料列。 **右外部聯結** 是邏輯運算子。|  
|無|**右方半聯結**|當第一個 (頂端) 輸入有相符的資料列時，「右方半聯結」運算子會從第二個 (底端) 輸入傳回每一個資料列。 如果 **Argument** 資料行中沒有聯結述詞，則每一資料列就是一個符合資料列。 **右方半聯結** 是邏輯運算子。|  
|![資料列計數多工緩衝處理運算子圖示](../relational-databases/media/remote-count-spool-32x.gif "資料列計數多工緩衝處理運算子圖示")|**資料列計數多工緩衝處理**|「資料列計數多工緩衝處理」運算子會掃描輸入、計算共有多少資料列，然後傳回一樣多但不含任何資料的資料列。 如果重點是檢查資料列是否存在，而不是資料列中是否包含資料，就可以使用這個運算子。 例如，如果「巢狀迴圈」運算子執行左方半聯結作業，而且聯結述詞會套用到內部輸入，就可以在「巢狀迴圈」運算子的內部輸入上面放「資料列計數多工緩衝處理」。 接著，「巢狀迴圈」運算子可以看看「資料列計數多工緩衝處理」會輸出多少資料列 (因為不需要內部的實際資料)，決定是否要傳回外部資料列。 「資料列計數多工緩衝處理」是實體運算子。|  
|![區段運算子圖示](../relational-databases/media/segment-32x.gif "區段運算子圖示")|**區段**|「區段」是實體和邏輯運算子。 它會根據一或多個資料行的值，將輸入集分割為區段。 這些資料行在「區段」運算子中會顯示為引數。 然後運算子一次會輸出一個區段。|  
|無|**區段重新分割**|在平行查詢計畫中，有時候會有 Iterator 的概念區。 在這種區域內的所有 Iterator，都可以由平行執行緒來執行。 區域本身必須連續執行。 個別區域內的一些「平行處理原則」Iterator，稱作「分支重新分割」。 在兩個這種區域的界限上的「平行處理原則」Iterator，稱作「區段重新分割」。 「分支重新分割」和「區段重新分割」都是邏輯運算子。|  
|![序列運算子圖示](../relational-databases/media/sequence-32x.gif "序列運算子圖示")|**序列**|「序列」運算子會驅動大範圍的更新計畫。 在功能上，它會依序執行每個輸入 (由上而下)。 每個輸入通常是更新不同的物件。 它只會傳回來自最後一個 (下方) 輸入的資料列。 「序列」是邏輯與實體運算子。|  
|![序列專案運算子圖示](../relational-databases/media/sequence-project-32x.gif "序列專案運算子圖示")|**順序專案**|「順序專案」運算子會加入資料行以執行已排序集合的計算。 它會根據一或多個資料行的值，將輸入集分割為區段。 然後運算子一次會輸出一個區段。 這些資料行在「順序專案」運算子中會顯示為引數。 「順序專案」是邏輯與實體運算子。|  
|![快照集資料指標運算子圖示](../relational-databases/media/snapshot-32x.gif "快照集資料指標運算子圖示")|**快照式**|「快照式」運算子會建立一個資料指標，而不會看到其他人所做的變更。|  
|![排序運算子圖示](../relational-databases/media/sort-32x.gif "排序運算子圖示")|**排序**|「排序」運算子會排序所有內送的資料列。 如果這個作業會移除重複的項目，則 **Argument** 資料行中會包含 DISTINCT ORDER BY:() 述詞，或包含 ORDER BY:() 述詞以及將會排序的資料行清單 (以逗號分隔)。 如果將資料行依遞增順序排序，資料行前會加上 ASC 值，如果將資料行依遞減順序排序，資料行前會加上 DESC 值。 「排序」是邏輯與實體運算子。|  
|![分割運算子圖示](../relational-databases/media/split-32x.gif "分割運算子圖示")|**分割**|「分割」運算子可用以最佳化更新處理。 它會將每個更新分割成一個刪除和一個插入作業。 「分割」是邏輯與實體運算子。|  
|![多工緩衝處理運算子圖示](../relational-databases/media/spool-32x.gif "多工緩衝處理運算子圖示")|**多工緩衝處理**|「多工緩衝處理」運算子會將中繼查詢結果儲存到 **tempdb** 資料庫。|  
|![資料流彙總運算子圖示](../relational-databases/media/stream-aggregate-32x.gif "資料流彙總運算子圖示")|**Stream Aggregate**|「資料流彙總」運算子會依據一個或多個資料行將資料列分組，然後計算查詢所傳回的一個或多個彙總運算式。 這個運算子的輸出可稍後由查詢中的運算子參考，並/或傳回到用戶端。 「資料流彙總」運算子需要其群組內的輸入項目依資料行排列。 如果資料因為前面的「排序」運算子或因為已排序索引搜尋或掃描，而尚未排序，最佳化工具就會在這個運算子之前使用「排序」運算子。 在 SHOWPLAN_ALL 陳述式或 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 的圖形執行計畫中，GROUP BY 述詞中的資料行會列於 **Argument** 資料行中，而彙總運算式則會列在 **Defined Values** 資料行中。 「資料流彙總」是實體運算子。|  
|![參數運算子圖示](../relational-databases/media/switch-32x.gif "參數運算子圖示")|**參數**|**參數**是一種特殊類型的串連 Iterator，它有 *n* 個輸入。 運算式與每一個「參數」運算子相關聯。 根據運算式的傳回值 (介於 0 和 *n*-1 之間)，**參數**會將適當的輸入資料流複製到輸出資料流。 「參數」的用途之一是實作查詢計畫，包括利用某些運算子向前快轉資料指標，例如 **TOP** 運算子。 「參數」同時為邏輯和實體運算子。|  
|![資料表刪除運算子圖示](../relational-databases/media/table-delete-32x.gif "資料表刪除運算子圖示")|**資料表刪除**|「資料表刪除」實體運算子會從查詢執行計畫之 **Argument** 資料行所指定的資料表中刪除資料列。|  
|![資料表插入運算子圖示](../relational-databases/media/table-insert-32x.gif "資料表插入運算子圖示")|**資料表插入**|「資料表插入」運算子會從輸入將資料列插入查詢執行計畫之 **Argument** 資料行所指定的資料表中。 **Argument** 資料行也包含 SET:() 述詞，指出每一個資料行設定的值。 如果「資料表插入」沒有插入值的子系，則會從插入運算子本身取得插入的資料列。 「資料表插入」是實體運算子。|  
|![資料表合併運算子](../relational-databases/media/table-merge-32x.gif "資料表合併運算子")|**資料表合併**|「資料表合併」運算子會將合併資料流套用到堆積中。 此運算子會從運算子之 **Argument** 資料行內所指定的資料表中刪除、更新或插入資料列。 所執行的實際作業取決於運算子之 **Argument** 資料行內指定之 **ACTION** 資料行的執行階段值。 「資料表合併」是實體運算子。|  
|![資料表掃描運算子圖示](../relational-databases/media/table-scan-32x.gif "資料表掃描運算子圖示")|**資料表掃描**|「資料表掃描」運算子會從查詢執行計畫之 **Argument** 資料行所指定的資料表中擷取所有資料列。 如果 **Argument** 資料行中出現 WHERE:() 述詞，就只會傳回滿足述詞的那些資料列。 「資料表掃描」是邏輯與實體運算子。|  
|![資料表多工緩衝處理運算子圖示](../relational-databases/media/table-spool-32x.gif "資料表多工緩衝處理運算子圖示")|**資料表多工緩衝處理**|「資料表多工緩衝處理」運算子會掃描輸入，並將每個資料列的複本放入隱藏的多工緩衝資料表 (儲存在 [tempdb](../relational-databases/databases/tempdb-database.md) 資料庫，直到查詢結束就不再存在)。 如果倒轉運算子 (例如，利用「巢狀迴圈」運算子)，但是不需要重新繫結，會使用多工緩衝處理資料，而非重新掃描輸入。 「資料表多工緩衝處理」是實體運算子。|  
|![資料表更新運算子圖示](../relational-databases/media/table-update-32x.gif "資料表更新運算子圖示")|**資料表更新**|「資料表更新」實體運算子會更新查詢執行計畫之 **Argument** 資料行所指定資料表中的輸入資料列。 SET:() 述詞決定每個更新資料行的值。 在 SET 子句中或這個運算子中，以及這個查詢中的其他位置，皆可參考這些數值。|  
|![資料表值函式運算子圖示](../relational-databases/media/table-valued-function-32x.gif "資料表值函式運算子圖示")|**資料表值函式**|「資料表值函式」運算子會評估資料表值函數 ([!INCLUDE[tsql](../includes/tsql-md.md)] 或 CLR)，並將產生的資料列儲存至 [tempdb](../relational-databases/databases/tempdb-database.md) 資料庫。 如果父系 Iterator 要求資料列，「資料表值函式」便會從 **tempdb** 傳回資料列。<br /><br /> 含有呼叫資料表值函數的查詢會產生內含「資料表值函式」Iterator 的查詢計畫。 「資料表值函式」可以使用不同的參數值進行評估：<br /><br /> -<br />                    「資料表值函式 XML 讀取器」可輸入 XML BLOB 作為參數，並以 XML 文件的順序，產生代表 XML 節點的資料列集。 其他的輸入參數可能會限制傳回給 XML 文件子集的 XML 節點。<br /><br /> -「含 XPath 篩選的資料表值函式 XML 讀取器」是一種特別的 **XML 讀取器資料表值函式**，可將輸出限制為滿足 XPath 運算式的 XML 節點。<br /><br /> 「資料表值函式」是邏輯與實體運算子。|  
|![頂端運算子圖示](../relational-databases/media/top-32x.gif "頂端運算子圖示")|**頂端**|「頂端」運算子會掃描輸入，可能會根據排序的先後順序，只傳回指定數目或百分比的資料列。 **Argument** 資料行可以包含要檢查繫結的資料行清單。 在更新計畫中，可使用「頂端」運算子強行限制資料列數。 「頂端」是邏輯與實體運算子。|  
|無|**前 N 個排序**|「前 N 個排序」與「排序」Iterator 類似，只不過它只需要前 *N* 個資料列，而不是整個結果集。 若 *N* 值較小，[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 查詢執行引擎會嘗試在記憶體中執行整個排序作業。 若 *N*的值較大，則查詢執行引擎會訴諸比較一般性的排序方法，而不採用 *N* 作為參數。|  
|![擴充運算子 (UDX) 圖示](../relational-databases/media/udx-32x.gif "擴充運算子 (UDX) 圖示")|**UDX**|擴充運算子 (UDX) 會在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]中實作許多 XQuery 和 XPath 作業的其中一項。 所有 UDX 運算子都是邏輯和實體運算子。<br /><br /> 擴充運算子 (UDX) **FOR XML** 用於序列化關聯式資料列集，它會在單一輸出資料列的單一 BLOB 資料行中，以 XML 表示法輸入這個資料列集。 這是一個會區分順序的 XML 彙總運算子。<br /><br /> 擴充運算子 (UDX) **XML SERIALIZER** 是區分順序的 XML 彙總運算子， 會以 XML 文件順序來輸入用於表示 XML 節點或 XQuery 純量的資料列，並在單一輸出資料列的單一 XML 資料行中產生序列化的 XML BLOB。<br /><br /> 擴充運算子 (UDX) **XML FRAGMENT SERIALIZER** 是特殊類型的 **XML SERIALIZER** ，可用於處理輸入資料列，而此輸入資料列用於表示要插入至 XQuery 插入資料修改延伸模組的 XML 片段。<br /><br /> 擴充運算子 (UDX) **XQUERY STRING** 會評估用於表示 XML 節點之輸入資料列的 XQuery 字串值。 這是一個區分順序的字串彙總運算子。 它會輸出一個資料列以及多個資料行，每個資料行都代表含有輸入字串值的 XQuery 純量。<br /><br /> 擴充運算子 (UDX) **XQUERY LIST DECOMPOSER** 是 XQuery 清單分解運算子。 針對代表 XML 節點的每一個輸入資料列，會產生代表 XQuery 純量的一或多個資料列，而如果輸入是 XSD 清單類型，則包含清單元素值。<br /><br /> 擴充運算子 (UDX) **XQUERY DATA** 會評估表示 XML 節點之輸入的 XQuery fn:data() 函數。 這是一個區分順序的字串彙總運算子。 它會輸出一個資料列以及多個資料行，每個資料行都代表含有 **fn:data()**結果的 XQuery 純量。<br /><br /> 擴充運算子 (UDX) **XQUERY CONTAINS** 會評估表示 XML 節點之輸入的 XQuery fn:data() 函數。 這是一個區分順序的字串彙總運算子。 它會輸出一個資料列以及多個資料行，每個資料行都代表含有 **fn:contains()**結果的 XQuery 純量。<br /><br /> 擴充運算子 **UPDATE XML NODE** 會更新 XML 類型之 **modify()** 方法中，XQuery 取代資料修改延伸模組內的 XML 節點。|  
|無|**Union**|**Union** 運算子會掃描多個輸入，輸出掃描的每一資料列，並移除重複項。 **Union** 是邏輯運算子。|  
|![更新 (資料庫引擎) 運算子圖示](../relational-databases/media/update-32x.gif "更新 (資料庫引擎) 運算子圖示")|**Update**|「更新」運算子會在查詢執行計畫之 **Argument** 資料行所指定的物件上，從其輸入中更新每一個資料列。 「更新」是邏輯運算子。 實體運算子是「資料表更新」、「索引更新」或「叢集索引更新」。|  
|![While 語言項目圖示](../relational-databases/media/while-32x.gif "While 語言項目圖示")|**While**|**While** 運算子會實作 [!INCLUDE[tsql](../includes/tsql-md.md)] while 迴圈。 **While** 是語言元素。|  
|![資料表多工緩衝處理運算子圖示](../relational-databases/media/table-spool-32x.gif "資料表多工緩衝處理運算子圖示")|**視窗多工緩衝處理**|「視窗多工緩衝處理」運算子會將每一列展開成一組資料列，分別代表與其關聯的視窗。 查詢中的 OVER 子句會定義查詢結果集中的視窗，以及一個計算視窗中各資料列值的視窗函數。 「視窗多工緩衝處理」是邏輯與實體運算子。|  
  
  
