---
title: 執行程序邏輯和實體運算子參考 | Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- sql12.swb.showplan.nestedloops.f1
- sql12.swb.showplan.dynamic.f1
- sql12.swb.showplan.tableinsert.f1
- sql12.swb.showplan.remoteinsert.f1
- sql12.swb.showplan.lazyspool.f1
- sql12.swb.showplan.RIDLookup
- sql12.swb.showplan.hashmatchteam.f1
- sql12.swb.showplan.tablespool.f1
- sql12.swb.showplan.print.f1
- sql12.swb.showplan.clusteredindexupdate.f1
- sql12.swb.showplan.assert.f1
- sql12.swb.showplan.columnstoreindexscan.f1
- sql12.swb.showplan.tablevaluedfunction.f1
- sql12.swb.showplan.split.f1
- sql12.swb.showplan.union.f1
- sql12.swb.showplan.clusteredindexseek.f1
- sql12.swb.showplan.indexspool.f1
- sql12.swb.showplan.indexinsert.f1
- sql12.swb.showplan.clusteredindexscan.f1
- sql12.swb.showplan.buildhash.f1
- sql12.swb.showplan.clusteredindexmerge.f1
- sql12.swb.showplan.sequence.f1
- sql12.swb.showplan.hashmatchroot.f1
- sql12.swb.showplan.columnstoreindexupdate.f1
- sql12.swb.showplan.rightsemijoin.f1
- sql12.swb.showplan.fetchquery.f1
- sql12.swb.showplan.distinct.f1
- sql12.swb.showplan.hashmatch.f1
- sql12.swb.showplan.segment.f1
- sql12.swb.showplan.top.f1
- sql12.swb.showplan.columnstoreindexdelete.f1
- sql12.swb.showplan.gatherstreams.f1
- sql12.swb.showplan.remotedelete.f1
- sql12.swb.showplan.insert.f1
- sql12.swb.showplan.declare.f1
- sql12.swb.showplan.snapshot.f1
- sql12.swb.showplan.assign.f1
- sql12.swb.showplan.intrinsic.f1
- sql12.swb.showplan.mergejoin.f1
- sql12.swb.showplan.concatenation.f1
- sql12.swb.showplan.rowcountspool.f1
- sql12.swb.showplan.parametertablescan.f1
- sql12.swb.showplan.indexscan.f1
- sql12.swb.showplan.while.f1
- sql12.swb.showplan.columnstoreindexinsert.f1
- sql12.swb.showplan.tablemerge.f1
- sql12.swb.showplan.spool.f1
- sql12.swb.showplan.streamaggregate.f1
- sql12.swb.showplan.update.f1
- sql12.swb.showplan.innerjoin.f1
- sql12.swb.showplan.flowdistinct.f1
- sql12.swb.showplan.tableupdate.f1
- sql12.swb.showplan.result.f1
- sql12.swb.showplan.bitmap.f1
- sql12.swb.showplan.remoteindexseek.f1
- sql12.swb.showplan.populationquery.f1
- sql12.swb.showplan.rightouterjoin.f1
- sql12.swb.showplan.columnstoreindexmerge.f1
- sql12.swb.showplan.remotescan.f1
- sql12.swb.showplan.remoteupdate.f1
- sql12.swb.showplan.keyset.f1
- sql12.swb.showplan.collapse.f1
- sql12.swb.showplan.arithmeticexpression.f1
- sql12.swb.showplan.clusteredindexinsert.f1
- sql12.swb.showplan.computescalar
- sql12.swb.showplan.sort.f1
- sql12.swb.showplan.locate.f1
- sql12.swb.showplan.constantscan.f1
- sql12.swb.showplan.computescalar.f1
- sql12.swb.showplan.indexseek.f1
- sql12.swb.showplan.leftsemijoin.f1
- sql12.swb.showplan.leftantisemijoin.f1
- sql12.swb.showplan.fullouterjoin.f1
- sql12.swb.showplan.filter.f1
- sql12.swb.showplan.indexdelete.f1
- sql12.swb.showplan.repartitionstreams.f1
- sql12.swb.showplan.crossjoin.f1
- sql12.swb.showplan.mergeinterval.f1
- sql12.swb.showplan.bookmarklookup.f1
- sql12.swb.showplan.convert.f1
- sql12.swb.showplan.refreshquery.f1
- sql12.swb.showplan.distinctsort.f1
- sql12.swb.showplan.leftouterjoin.f1
- sql12.swb.showplan.rightantisemijoin.f1
- sql12.swb.showplan.deletedscan.f1
- sql12.swb.showplan.udx.f1
- sql12.swb.showplan.broadcast.f1
- sql12.swb.showplan.delete.f1
- sql12.swb.showplan.aggregate.f1
- sql12.swb.showplan.setfunction.f1
- sql12.swb.showplan.switch.f1
- sql12.swb.showplan.remoteindexscan.f1
- sql12.swb.showplan.eagerspool.f1
- sql12.swb.showplan.indexupdate.f1
- sql12.swb.showplan.keylookup.f1
- sql12.swb.showplan.branchrepartition.f1
- sql12.swb.showplan.rank.f1
- sql12.swb.showplan.tablescan.f1
- sql12.swb.showplan.distributestreams.f1
- sql12.swb.showplan.logrowscan.f1
- sql12.swb.showplan.parallelism.f1
- sql12.swb.showplan.bitmapcreate.f1
- sql12.swb.showplan.insertedscan.f1
- sql12.swb.showplan.tabledelete.f1
- sql12.swb.showplan.clusteredindexdelete.f1
- sql12.swb.showplan.remotequery.f1
- sql12.swb.showplan.if.f1
- sql12.swb.showplan.cache.f1
- sql12.swb.showplan.partialaggregate.f1
- sql12.swb.showplan.sql.f1
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
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: e4e45de57f4ea1ea88b72df7190e5ec8c3a1f768
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "62627327"
---
# <a name="showplan-logical-and-physical-operators-reference"></a>執行程序邏輯和實體運算子參考
  運算子說明 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 如何執行查詢或資料操作語言 (DML) 陳述式。 查詢最佳化工具會使用運算子來建立查詢計畫，以便建立查詢所指定的結果，或執行 DML 陳述式所指定的作業。 查詢計畫是由實體運算子所組成的樹狀目錄。 您可使用 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]中的圖形執行計畫選項 SET SHOWPLAN 陳述式，以及 SQL Server Profiler Showplan 事件類別，檢視查詢計畫。  
  
 運算子可分為邏輯與實體運算子兩種。  
  
 **邏輯運算子**  
 邏輯運算子說明用來處理陳述式的關聯式代數作業。 換句話說，邏輯運算子可就概念上說明需要執行哪項作業。  
  
 **實體運算子**  
 實體運算子會實作邏輯運算子所描述的作業。 每個實體運算子都是執行作業的物件或常式。 例如，有些實體運算子會從資料表、索引或檢視表中存取資料行或資料列。 其他實體運算子則會執行其他操作，如計算、彙總、資料完整性檢查或聯結。 實體運算子會有上述項目的相關成本。  
  
 實體運算子可進行初始化、收集資料及關閉。 特別是，實體運算子可回應下列三種方法呼叫：  
  
-   **Init()** ： **Init()** 方法會使實體運算子自行初始化，並設定任何必要的資料結構。 實體運算子可接收許多 **Init()** 呼叫，但通常實體運算子只會接收一個。  
  
-   **GetNext()** ： **GetNext()** 方法會使實體運算子取得資料的第一個或下一個資料列。 實體運算子可能會接收零個或許多 **GetNext()** 呼叫。  
  
-   **Close()** ： **Close()** 方法會使實體運算子執行某些清除作業並自行關閉。 實體運算子只會接收一個 **Close()** 呼叫。  
  
 **GetNext()** 方法會傳回一列資料，而它被呼叫的次數會在使用 SET STATISTICS PROFILE ON or SET STATISTICS XML ON 所產生的「執行程序表」輸出中顯示為 **ActualRows**。 如需這些 SET 選項的詳細資訊，請參閱 [SET STATISTICS PROFILE &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-statistics-profile-transact-sql) 和 [SET STATISTICS XML &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-statistics-xml-transact-sql)。  
  
 「執行程序表」輸出中顯示的 **ActualRebinds** 和 **ActualRewinds** 計數代表 **Init()** 方法被呼叫的次數。 除非運算子位於迴圈聯結的內部，否則 **ActualRebinds** 會等於一，而 **ActualRewinds** 會等於零。 如果運算子位於迴圈聯結的內部，重新繫結和倒轉數目的總和應該會等於聯結外部所處理的資料列數目。 重新繫結是指聯結中有一或多個相互關聯的參數發生變更，而必須重新評估內部。 倒轉是指相互關聯的參數沒有發生變更，先前的內部結果集可供重複使用。  
  
 **ActualRebinds** 和 **ActualRewinds** 會顯示在使用 SET STATISTICS XML ON 產生的「XML 執行程序表」輸出中。 它們只會填入非叢集**索引**多工緩衝`Remote Query`處理、資料**列計數**多工緩衝處理、 `Sort`**資料表**多工緩衝處理和**資料表值函數**運算子。 當**StartupExpression**屬性設定為 TRUE 時`Assert` ， **ActualRebinds**和**ActualRewinds**也可能會填入和**篩選**運算子。  
  
 「XML 執行程序表」中有 **ActualRebinds** 和 **ActualRewinds** 時，您可將它們與 **EstimateRebinds** 和 **EstimateRewinds** 做比較。 如果沒有，則可將估計的資料列數目 (**EstimateRows**) 和實際資料列數目 (**ActualRows**) 做比較。 請注意，如果沒有實際重新繫結和實際倒轉，實際圖形「執行程序表」輸出便會顯示零。  
  
 只有當「執行程序表」輸出是以 SET STATISTICS XML ON 產生時，才可使用相關的計數器 **ActualEndOfScans**。 每當實體運算子存取至其資料流結尾時，此計數器就會累加 1。 實體運算子可存取其資料流結尾零次、一次或多次。 如同重新繫結和倒轉，只有當運算子位於迴圈聯結內部時，結尾掃描次數才能大於 1。 結尾掃描次數應小於或等於重新繫結和倒轉的數目總和。  
  
## <a name="mapping-physical-and-logical-operators"></a>對應實體與邏輯運算子  
 查詢最佳化工具會將查詢計畫建立為由邏輯運算子所組成的樹狀目錄。 在查詢最佳化工具建立計畫之後，它會為每個邏輯運算子選擇最有效率的實體運算子。 查詢最佳化工具會使用以成本為基礎的方法，判斷哪個實體運算子將實作邏輯運算子。  
  
 一個邏輯運算子通常可由多個實體運算子實作。 不過，在極少數的情況下，實體運算子也可以實作多個邏輯運算子。  
  
## <a name="operator-descriptions"></a>運算子描述  
 本節包含邏輯與實體運算子的說明：  
  
|圖形執行計畫圖示|Showplan 運算子|描述|  
|-----------------------------------|-----------------------|-----------------|  
|None|`Aggregate`|`Aggregate` 運算子會計算包含 MIN、MAX、SUM、COUNT 或 AVG 的運算式。 `Aggregate` 運算子可以是邏輯運算子或實體運算子。|  
|![算術運算式運算子圖示](../../2014/database-engine/media/arithmetic-expression-32x-2.gif "算術運算式運算子圖示")|`Arithmetic Expression`|`Arithmetic Expression` 運算子會從資料列中現有的值計算出新的值。 `Arithmetic Expression` 無法用於 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 中。|  
|![判斷提示運算子圖示](../../2014/database-engine/media/assert-32x.gif "判斷提示運算子圖示")|`Assert`|`Assert` 運算子會驗證條件。 例如，它會驗證參考完整性，或確定純量子查詢傳回一個資料列。 針對每個輸入資料`Assert` `Argument`列，運算子會評估執行計畫之資料行中的運算式。 如果這個運算式評估為 NULL，代表資料列通過 `Assert` 運算子的驗證，則查詢會繼續執行。 如果這個運算式得出非 Null 值，就會得出相對的錯誤。 `Assert` 運算子是實體運算子。|  
|![指派語言項目圖示](../../2014/database-engine/media/assign-32.gif "指派語言項目圖示")|`Assign`|`Assign` 運算子會將運算式的值或常數指派給變數。 `Assign` 是語言元素。|  
|None|`Asnyc Concat`|`Asnyc Concat` 運算子只能使用於遠端查詢 (分散式查詢)。 它有 *n* 個子節點和一個父節點。 一般來說，某些子節點是參與分散式查詢的遠端電腦。 `Asnyc Concat` 會同時對所有子節點發出 `open()` 呼叫，然後再將點陣圖套用到每個子節點。 `Async Concat` 會針對每一個是 1 的位元，視需要將輸出資料列傳送至父節點。|  
|![點陣圖運算子圖示](../../2014/database-engine/media/bitmap-32x.gif "點陣圖運算子圖示")|`Bitmap`|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]使用`Bitmap`運算子，在平行查詢計劃中執行點陣圖篩選。 點陣圖篩選會藉由刪除索引鍵值無法產生任何聯結記錄的資料列來加速查詢執行，然後再透過另一個運算子`Parallelism` （例如運算子）傳遞資料列。 點陣圖篩選會於運算子樹狀目錄的一部分，以精簡方式顯示資料表中的一組值，以便從此樹狀目錄的另一個部分篩選第二個資料表中的資料列。 藉由盡早移除查詢中的不必要資料列，後續的運算子需要處理的資料列就會更少，而查詢的整體效能也會提升。 最佳化工具會判斷點陣圖何時具有足夠的選擇性能夠充分運用以及將篩選套用到哪個運算子。 `Bitmap` 是實體運算子。|  
|![點陣圖運算子圖示](../../2014/database-engine/media/bitmap-32x.gif "點陣圖運算子圖示")|`Bitmap Create`|`Bitmap Create` 運算子會出現在建立點陣圖的 Showplan 輸出中。 `Bitmap Create` 是邏輯運算子。|  
|![書籤查閱運算子圖示](../../2014/database-engine/media/bookmark-lookup-32x.gif "書籤查閱運算子圖示")|`Bookmark Lookup`|`Bookmark Lookup` 運算子使用書籤 (資料列識別碼或叢集索引鍵) 在資料表或叢集索引中查閱對應的資料列。 資料`Argument`行包含書簽標籤，用來查閱資料表或叢集索引中的資料列。 此`Argument`資料行也包含查閱資料列所在之資料表或叢集索引的名稱。 如果資料`Argument`行中出現 WITH 預先提取子句，表示查詢處理器已決定在資料表或叢集索引中查閱書簽時，使用非同步預先提取（預先讀取）是最佳做法。<br /><br /> `Bookmark Lookup` 無法用於 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 中。 不過，`Clustered Index Seek` 和 `RID Lookup` 會提供書籤查閱功能。 `Key Lookup` 運算子也提供這項功能。|  
|None|`Branch Repartition`|在平行查詢計畫中，有時候會有 Iterator 的概念區。 在這種區域內的所有 Iterator，都可以由平行執行緒來執行。 區域本身必須連續執行。 個別區域內的一些 `Parallelism` Iterator，稱為 `Branch Repartition`。 在兩個這種區域的界限上的 `Parallelism` Iterator，稱為 `Segment Repartition`。 `Branch Repartition` 和 `Segment Repartition` 是邏輯運算子。|  
|None|`Broadcast`|`Broadcast`有一個子節點和*n*個父節點。 `Broadcast` 會依要求將其輸入資料列傳送至多位取用者。 每位取用者都會收到所有資料列。 例如，若所有取用者都是雜湊聯結的建立者，則會建立 *n* 份雜湊資料表。|  
|![建立雜湊運算子圖示](../../2014/database-engine/media/build-hash.gif "建立雜湊運算子圖示")|`Build Hash`|指示建立 xVelocity 記憶體最佳化的資料行存放區索引之批次雜湊資料表。|  
|None|`Cache`|`Cache`是多工**緩衝**處理運算子的特製化版本。 它只儲存一列資料。 `Cache` 是邏輯運算子。 `Cache` 無法用於 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 中。|  
|![叢集索引刪除運算子圖示](../../2014/database-engine/media/clustered-index-delete-32x.gif "叢集索引刪除運算子圖示")|`Clustered Index Delete`|`Clustered Index Delete` 運算子會從查詢執行計畫之 Argument 資料行所指定的叢集索引中刪除資料列。 如果 Argument 資料行中出現 WHERE:() 述詞，就只刪除滿足述詞的資料列。`Clustered Index Delete`  是實體運算子。|  
|![叢集索引插入運算子圖示](../../2014/database-engine/media/clustered-index-insert-32x.gif "叢集索引插入運算子圖示")|`Clustered Index Insert`|`Clustered Index Insert` 執行程序表運算子會將其輸入的資料列插入 Argument 資料行所指定的叢集索引中。 Argument 資料行也包含 SET:() 述詞，指出每一個資料行設定的值。 如果`Clustered Index Insert`沒有插入值的子系，則會從`Insert`運算子本身取得插入的資料列。`Clustered Index Insert`  是實體運算子。|  
|![叢集索引合併運算子](../../2014/database-engine/media/clustered-index-merge-32x.gif "叢集索引合併運算子")|**叢集索引合併**|「叢集索引合併」**** 運算子會將合併資料流套用到叢集索引。 運算子會從運算子的`Argument`資料行中指定的叢集索引中刪除、更新或插入資料列。 所執行的實際作業取決於運算子的`Argument`資料行中所指定之**動作**資料行的運行時間值。 「叢集索引合併」**** 是實體運算子。|  
|![叢集索引掃描運算子圖示](../../2014/database-engine/media/clustered-index-scan-32x.gif "叢集索引掃描運算子圖示")|`Clustered Index Scan`|`Clustered Index Scan` 運算子會掃描查詢執行計畫的 Argument 資料行中指定的叢集索引。 出現選擇性的 WHERE:() 述詞時，只會傳回滿足述詞的資料列。 如果 Argument 資料行中包含 ORDERED 子句，表示查詢處理器要求資料列的輸出須按叢集索引的排序次序傳回。 如果沒有 ORDERED 子句，儲存引擎會以最佳方式搜尋索引，而不需要排序輸出。 `Clustered Index Scan` 是邏輯與實體運算子。|  
|![叢集索引搜尋運算子圖示](../../2014/database-engine/media/clustered-index-seek-32x.gif "叢集索引搜尋運算子圖示")|`Clustered Index Seek`|`Clustered Index Seek` 運算子使用索引的搜尋能力，從叢集索引中擷取資料列。 資料`Argument`行包含所使用的叢集索引名稱和 seek：（）述詞。 儲存引擎會使用索引來處理滿足這個 SEEK:() 述詞的資料列。 也可以包含 WHERE:() 述詞，讓儲存引擎針對滿足 SEEK:() 述詞的所有資料列進行評估，但此為選擇性，且不使用索引來完成此程序。<br /><br /> 如果資料`Argument`行包含已排序的子句，則查詢處理器已判定資料列必須依照叢集索引已排序的順序傳回。 如果沒有 ORDERED 子句，儲存引擎會以最佳方式搜尋索引，不需要將輸出排序。 讓輸出維持次序會比產生不按次序的輸出更沒效率。 出現關鍵字 LOOKUP 時，表示正在執行書籤查閱。 在[!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]和更新版本中， `Key Lookup`運算子會提供書簽查閱功能。 `Clustered Index Seek` 是邏輯與實體運算子。|  
|![叢集索引更新運算子圖示](../../2014/database-engine/media/clustered-index-update-32x.gif "叢集索引更新運算子圖示")|`Clustered Index Update`|`Clustered Index Update`運算子會更新資料行中所指定之叢集索引內`Argument`的輸入資料列。如果出現 WHERE：（）述詞，則只會更新滿足這個述詞的資料列。 如果出現 SET:() 述詞，則每個更新的資料行都會設為這個值。 如果出現 DEFINE:() 述詞，就會列出這個運算子定義的數值。 在 SET 子句中或這個運算子中以及這個查詢中的其他位置，都可以參考這些數值。 `Clustered Index Update` 是邏輯與實體運算子。|  
|![摺疊運算子圖示](../../2014/database-engine/media/collapse-32x.gif "摺疊運算子圖示")|`Collapse`|`Collapse` 運算子可最佳化更新處理。 執行更新時，它可以分割成 (使用 `Split` 運算子) 刪除與插入。 資料`Argument`行包含指定索引鍵資料行清單的 GROUP BY：（）子句。 如果查詢處理器發現了刪除及插入相同索引鍵值的相鄰資料列，會以更有效率的單一更新作業來取代這些不同的作業。 `Collapse` 是邏輯與實體運算子。|  
|![資料行存放區索引掃描](../../2014/database-engine/media/columnstoreindexscan.gif "資料行存放區索引掃描")|`Columnstore Index Scan`|`Columnstore Index Scan`運算子會掃描查詢執行計畫之資料`Argument`行中所指定的資料行存放區索引。|  
|![計算純量運算子圖示](../../2014/database-engine/media/compute-scalar-32x.gif "計算純量運算子圖示")|`Compute Scalar`|`Compute Scalar`運算子會評估運算式，以產生計算的純量值。 然後可能會將此值傳回給使用者，或由查詢的其他地方來參考，或兩者皆是。 例如在篩選述詞或聯結述詞中，就會見到這兩種情況。 `Compute Scalar` 是邏輯與實體運算子。<br /><br /> `Compute Scalar`在 SET STATISTICS XML 產生的執行程式表中出現的運算子可能不包含`RunTimeInformation`元素。 在圖形化的執行程序表中，當選取 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 中的 [包括實際執行計畫]**** 選項時，[實際資料列]****、[實際重新繫結]**** 與 [實際倒轉]**** 可能不會顯示在 [屬性]**** 視窗中。 發生此情況時，表示這些運算子雖然用於編譯的執行計畫中，它們的作用是由即時查詢計畫中的其他運算子執行。 同時也請注意，由 SET STATISTICS PROFILE 產生的「執行程序表」輸出中的執行數目，等於由 SET STATISTICS XML 產生的「執行程序表」中重新繫結和倒轉的總和。|  
|![串連運算子圖示](../../2014/database-engine/media/concatenation-32x.gif "串連運算子圖示")|**運算**|「串連」**** 運算子會掃描多個輸入，並傳回每一個掃描的資料列。 「串連」**** 通常用來實作 [!INCLUDE[tsql](../includes/tsql-md.md)] UNION ALL 建構。 「串連」**** 實體運算子有兩個以上的輸入和一個輸出。 串連作業會將資料列從第一個輸入資料流複製到輸出資料流，再對其他每一個輸入資料流重複此作業。 「串連」**** 是邏輯與實體運算子。|  
|![固定掃描運算子圖示](../../2014/database-engine/media/constant-scan-32x.gif "固定掃描運算子圖示")|`Constant Scan`|`Constant Scan`運算子會在查詢中引進一或多個常數資料列。 `Compute Scalar`運算子通常會在之後用`Constant Scan`來將資料行加入至運算子所`Constant Scan`產生的資料列。|  
|![轉換 (資料庫引擎) 語言項目圖示](../../2014/database-engine/media/convert-32x.gif "轉換 (資料庫引擎) 語言項目圖示")|`Convert`|`Convert` 運算子可將某個純量資料類型轉換為另一個資料類型。 `Convert` 是語言元素。|  
|None|`Cross Join`|`Cross Join` 運算子會將第一個 (頂端) 輸入的每一列與第二個 (底部) 輸入的每一列相聯結。 `Cross Join` 是邏輯運算子。|  
|![資料指標 catchall 資料指標運算子圖示](../../2014/database-engine/media/cursor-catch-all.gif "資料指標 catchall 資料指標運算子圖示")|`catchall`|產生圖形執行程序表的邏輯若找不到適當的 Iterator 圖示，就會顯示 [雜物箱] 圖示。 [雜物箱] 圖示不一定會指出錯誤條件。 [雜物箱] 圖示有三種：藍色 (Iterator)、橙色 (資料指標) 與綠色 ( [!INCLUDE[tsql](../includes/tsql-md.md)] 語言項目)。|  
|None|**資料指標**|「資料指標」**** 邏輯與實體運算子可用來說明與資料指標作業有關的查詢或更新將如何執行。 實體運算子是說明用來處理資料指標的實體實作演算法，例如使用索引鍵集衍生資料指標。 資料指標執行的每個步驟都有一個實體運算子。 邏輯運算子會說明資料指標的屬性，如資料指標是唯讀的。<br /><br /> 邏輯運算子包括非同步、開放式、主要、唯讀、捲動鎖定及次要與同步。<br /><br /> 實體運算子包括動態、提取查詢、索引鍵集、母體擴展查詢、重新整理查詢與快照集。|  
|![宣告語言項目圖示](../../2014/database-engine/media/declare-32x.gif "宣告語言項目圖示")|`Declare`|`Declare`運算子會在查詢計劃中配置區域變數。 `Declare` 是語言元素。|  
|![刪除 (資料庫引擎) 運算子圖示](../../2014/database-engine/media/delete-32x.gif "刪除 (資料庫引擎) 運算子圖示")|`Delete`|`Delete`運算子會從符合資料行中選擇性述詞的物件資料`Argument`列中刪除。|  
|![刪除掃描運算子圖示](../../2014/database-engine/media/delete-scan-32x.gif "刪除掃描運算子圖示")|`Deleted Scan`|`Deleted Scan` 運算子會掃描觸發程序中已刪除的資料表。|  
|None|`Distinct`|`Distinct` 運算子可從資料列集或從值集合移除重複的項目。 `Distinct` 是邏輯運算子。|  
|None|`Distinct Sort`|`Distinct Sort`邏輯運算子會掃描輸入，移除重複項，並依資料`Argument`行的 DISTINCT ORDER by：（）述詞所指定的資料行排序。 `Distinct Sort` 是邏輯運算子。|  
|![散發資料流平行處理原則運算子圖示](../../2014/database-engine/media/parallelism-distribute-stream.gif "散發資料流平行處理原則運算子圖示")|**散發資料流**|「散發資料流」**** 運算子只用於平行查詢計畫。 「散發資料流」**** 運算子會採用記錄的單一輸入資料流，並產生多個輸出資料流。 記錄內容與格式不會變更。 輸入資料流中的每筆資料錄都會出現在一個輸出資料流中。 這個運算子會自動在輸出資料流中保留輸入資料錄的關聯次序。 通常是利用雜湊方式來決定特定輸入資料錄應屬於哪個輸出資料流。<br /><br /> 如果輸出已分割，則資料`Argument`行包含 PARTITION columns：（）述詞和分割資料行。 「散發資料流」**** 是邏輯運算子。|  
|![動態資料指標運算子圖示](../../2014/database-engine/media/dynamic-32x.gif "動態資料指標運算子圖示")|`Dynamic`|`Dynamic` 運算子採用的資料指標，可以看到其他人進行的所有變更。|  
|![多工緩衝處理運算子圖示](../../2014/database-engine/media/spool-32x.gif "多工緩衝處理運算子圖示")|**急切的多工緩衝處理**|積極式多工**緩衝**處理運算子會採用整個輸入，並將每個資料列儲存在`tempdb`資料庫所儲存的隱藏暫存物件中。 如果重新倒轉運算子（例如，由`Nested Loops`運算子），但是不需要重新系結，則會使用多工緩衝處理的資料，而不是重新掃描輸入。 如果必須重新繫結的話，就丟棄多工緩衝處理的資料，然後重新掃描 (重新繫結) 輸入以重建多工緩衝處理物件。 「急切的多工緩衝處理」**** 運算子會以「急切的」方式建立多工緩衝處理檔案：當多工緩衝處理的父系運算子要求第一列時，「多工緩衝處理」運算子會消耗其輸入運算子的所有資料列，並將它們儲存在多工緩衝處理中。 **急切的多工緩衝處理** 是邏輯運算子。|  
|![擷取查詢資料指標運算子圖示](../../2014/database-engine/media/fetch-query-32x.gif "擷取查詢資料指標運算子圖示")|`Fetch Query`|`Fetch Query` 運算子會在對資料指標發出提取時擷取資料列。|  
|![篩選 (資料庫引擎) 運算子圖示](../../2014/database-engine/media/filter-32x.gif "篩選 (資料庫引擎) 運算子圖示")|**Filter**|**篩選**運算子會掃描輸入，只傳回滿足出現在資料行中篩選運算式（述詞）的那些資料`Argument`列。|  
|None|`Flow Distinct`|`Flow Distinct` 邏輯運算子會掃描輸入，移除重複的項目。 `Distinct`運算子會在產生任何輸出之前耗用所有輸入，而**FlowDistinct**運算子會在從輸入取得時傳回每個資料列（除非該資料列是重複的，在此情況下會被捨棄）。|  
|None|`Full Outer Join`|`Full Outer Join` 邏輯運算子所傳回的每個資料列，皆滿足第一個 (上方) 輸入的聯結述詞與第二個 (下方) 輸入的每一個資料列相聯結。 它也會傳回以下資料列：<br /><br /> - 第一個輸入中與第二個輸入完全不符合者。<br /><br /> - 第二個輸入中與第一個輸入完全不符合者。<br /><br /> <br /><br /> 不包含相符值的輸入會以 Null 值傳回。 `Full Outer Join` 是邏輯運算子。|  
|![集中資料流平行處理原則運算子圖示](../../2014/database-engine/media/parallelism-32x.gif "集中資料流平行處理原則運算子圖示")|**蒐集資料流**|「蒐集資料流」**** 運算子僅用於平行查詢計畫中。 「蒐集資料流」**** 運算子會耗用數個輸入資料流，並將輸入資料流合併而產生記錄的單一輸出資料流。 記錄內容與格式不會變更。 若此運算子要保留順序，那麼所有輸入資料流都必須排序好。 如果輸出經過排序，則`Argument`資料行包含 ORDER BY：（）述詞，以及要排序的資料行名稱。 **蒐集資料流** 是邏輯運算子。|  
|![雜湊比對運算子圖示](../../2014/database-engine/media/hash-match-32x.gif "雜湊比對運算子圖示")|`Hash Match`|`Hash Match` 運算子會根據其建立的輸入，為每一資料列計算雜湊值，以建立雜湊資料表。 資料`Argument`行中會出現 hash：（）述詞，以及用來建立雜湊值的資料行清單。 然後它會為每個探查列 (視情況) 建立雜湊值 (使用相同的雜湊函數)，並在雜湊資料表中尋找符合者。 如果有剩餘的述詞（在資料行中由剩餘`Argument`的：（）識別），則也必須滿足該述詞，才能將資料列視為相符。 行為取決於正在執行的邏輯作業：<br /><br /> 對於任何聯結，使用第一個 (上方) 輸入來建立雜湊資料表，第二個輸入 (下方) 來探查雜湊資料表。 輸出相符 (或不符合) 由聯結類型規定。 如果多個聯結使用相同的聯結行，這些作業會組成一組成為雜湊群。<br /><br /> 對於相異運算子或彙總運算子，使用輸入來建立雜湊資料表 (移除重複項，並計算任何彙總運算式)。 建立雜湊資料表時，會掃描資料表並輸出所有項目。<br /><br /> 對於等位運算子，使用第一個輸入來建立雜湊資料表 (移除重複項)。 使用第二個輸入 (必須沒有重複項) 探查雜湊資料表，傳回不符合的所有資料列，然後掃描雜湊資料表，並傳回所有項目。<br /><br /> <br /><br /> `Hash Match` 是實體運算子。|  
|![If 語言項目圖示](../../2014/database-engine/media/if-32x.gif "If 語言項目圖示")|`If`|`If` 運算子會依據運算式執行條件式處理。 `If` 是語言元素。|  
|None|`Inner Join`|`Inner Join` 邏輯運算子所傳回的每個資料列，皆滿足第一個 (上方) 輸入與第二個 (下方) 輸入的聯結。|  
|![插入 (資料庫引擎) 運算子圖示](../../2014/database-engine/media/insert-32x.gif "插入 (資料庫引擎) 運算子圖示")|`Insert`|`Insert`邏輯運算子會將其輸入中的每個資料`Argument`列插入至資料行中指定的物件。 實體運算子是 `Table Insert`、`Index Insert` 或 `Clustered Index Insert` 運算子。|  
|![插入的掃描運算子圖示](../../2014/database-engine/media/inserted-scan-32x.gif "插入的掃描運算子圖示")|**插入的掃描**|「插入的掃描」**** 運算子會掃描 **inserted** 資料表。 「插入的掃描」**** 是邏輯與實體運算子。|  
|![內建語言項目圖示](../../2014/database-engine/media/intrinsic-32x.gif "內建語言項目圖示")|`Intrinsic`|`Intrinsic` 運算子會叫用內部 [!INCLUDE[tsql](../includes/tsql-md.md)] 函數。 `Intrinsic` 是語言元素。|  
|![迭代器 catchall 運算子圖示](../../2014/database-engine/media/iterator-catch-all.gif "迭代器 catchall 運算子圖示")|`Iterator`|產生圖形執行程序表的邏輯若找不到適當的 Iterator 圖示，就會顯示 `Iterator` 雜物箱圖示。 [雜物箱] 圖示不一定會指出錯誤條件。 [雜物箱] 圖示有三種：藍色 (Iterator)、橙色 (資料指標) 與綠色 ( [!INCLUDE[tsql](../includes/tsql-md.md)] 語言建構)。|  
|![書籤查閱運算子圖示](../../2014/database-engine/media/bookmark-lookup-32x.gif "書籤查閱運算子圖示")|`Key Lookup`|`Key Lookup`運算子是具有叢集索引之資料表上的書簽查閱。 `Argument`資料行包含叢集索引的名稱，以及用來查閱叢集索引中之資料列的叢集索引鍵。 `Key Lookup`一律會伴隨一個`Nested Loops`運算子。 如果資料`Argument`行中出現 WITH 預先提取子句，表示查詢處理器已決定在叢集索引中查閱書簽時，使用非同步預先提取（預先讀取）是最佳做法。<br /><br /> 在查詢計劃中`Key Lookup`使用運算子，表示查詢可能受益于效能調整。 例如，您可以加入涵蓋索引來提高查詢效能。|  
|![索引鍵集資料指標運算子圖示](../../2014/database-engine/media/keyset-32x.gif "索引鍵集資料指標運算子圖示")|`Keyset`|`Keyset` 運算子使用可以查看更新，但無法插入其他人所製作的資料指標。|  
|![語言項目 catchall 圖示](../../2014/database-engine/media/language-construct-catch-all.gif "語言項目 catchall 圖示")|`Language Element`|產生圖形執行程序表的邏輯若找不到適當的 Iterator 圖示，就會顯示 `Language Element` 雜物箱圖示。 [雜物箱] 圖示不一定會指出錯誤條件。 [雜物箱] 圖示有三種：藍色 (Iterator)、橙色 (資料指標) 與綠色 ( [!INCLUDE[tsql](../includes/tsql-md.md)] 語言建構)。|  
|![多工緩衝處理運算子圖示](../../2014/database-engine/media/spool-32x.gif "多工緩衝處理運算子圖示")|**延遲多工緩衝處理**|「**延遲**多工緩衝處理」邏輯運算子會將其輸入中的每個`tempdb`資料列，儲存在資料庫中儲存的隱藏暫存物件中。 如果重新倒轉運算子（例如，由`Nested Loops`運算子），但是不需要重新系結，則會使用多工緩衝處理的資料，而不是重新掃描輸入。 如果必須重新繫結的話，就丟棄多工緩衝處理的資料，然後重新掃描 (重新繫結) 輸入以重建多工緩衝處理物件。 「延遲多工緩衝處理」**** 運算子會以「延遲」方式建立它的多工緩衝處理檔案，也就是說，每次多工緩衝處理的父系運算子要求一個資料列時，多工緩衝處理運算子就會從它的輸入運算子取得一個資料列，然後將它儲存在多工緩衝處理內，而不是一次取用所有資料列。 Lazy Spool 是邏輯運算子。|  
|None|`Left Anti Semi Join`|當第二個 (下方) 輸入中沒有相符的資料列時，`Left Anti Semi Join` 運算子將會從第一個 (上方) 輸入傳回每一個資料列。 如果資料行中沒有聯結述`Argument`詞，則每個資料列都是相符的資料列。 `Left Anti Semi Join` 是邏輯運算子。|  
|None|`Left Outer Join`|`Left Outer Join` 運算子所傳回的每個資料列，皆滿足第一個 (上方) 輸入與第二個 (下方) 輸入的聯結。 它也會傳回第一個輸入中與第二個輸入完全不相符的任何資料列。 第二個輸入中的不符合資料列會以 null 值傳回。 如果資料行中沒有聯結述`Argument`詞，則每個資料列都是相符的資料列。 `Left Outer Join` 是邏輯運算子。|  
|None|`Left Semi Join`|當第二個 (下方) 輸入中有相符的資料列時，`Left Semi Join` 運算子將會從第一個 (上方) 輸入傳回每一個資料列。 如果資料行中沒有聯結述`Argument`詞，則每個資料列都是相符的資料列。 `Left Semi Join` 是邏輯運算子。|  
|![記錄資料列掃描運算子圖示](../../2014/database-engine/media/log-row-scan-32x.gif "記錄資料列掃描運算子圖示")|`Log Row Scan`|`Log Row Scan` 運算子會掃描交易記錄。 `Log Row Scan` 是邏輯與實體運算子。|  
|![合併間隔運算子圖示](../../2014/database-engine/media/merge-interval-32x.gif "合併間隔運算子圖示")|`Merge Interval`|`Merge Interval` 運算子會合併多個 (可能重疊) 間隔以產生最小的非重疊間隔，然後使用這些間隔，尋找索引項目。 這個運算子通常會出現在`Compute Scalar` `Constant Scan`一或多個運算子上方，而不是由運算子組成，這會在此運算子合併的間隔（以資料列中的資料行表示）。 `Merge Interval` 是邏輯與實體運算子。|  
|![合併聯結運算子圖示](../../2014/database-engine/media/merge-join-32x.gif "合併聯結運算子圖示")|**合併聯結**|「合併聯結」**** 運算子會執行內部聯結、左方外部聯結、左方半聯結、左方反半聯結、右方外部聯結、右方半聯結、右方反半聯結，以及等位邏輯作業。<br /><br /> 在資料`Argument`行中，如果作業正在執行多對多聯結，「**合併聯結**」運算子會包含 merge：（）述詞（如果作業正在執行一對多聯結）或「多對多 Merge：（）」述詞。 此`Argument`資料行也包含用來執行作業的資料行清單（以逗號分隔）。 「合併聯結」**** 運算子需要兩個輸入，依個別資料行排序，可能是利用在查詢計畫中明確地插入排序作業。 如果不需要明確的排序，合併聯結會特別有效；例如，如果資料庫中有合適的 B 型樹狀目錄索引，或如果排序次序可以由多個作業利用 (如合併聯結與含積存的分組功能)。 「合併聯結」**** 是實體運算子。|  
|![巢狀迴圈運算子圖示](../../2014/database-engine/media/nested-loops-32x.gif "巢狀迴圈運算子圖示")|`Nested Loops`|`Nested Loops` 運算子執行內部聯結、左方外部聯結、左方半聯結和左方反半聯結邏輯運算。 巢狀迴圈聯結通常會使用索引，在內部資料表中搜尋外部資料表的每個資料列。 查詢處理器會根據預期的成本，決定是否要排序外部輸入，以改進對內部輸入的索引搜尋位置。 在資料行中滿足（選擇性）述詞的`Argument`任何資料列，會根據所執行的邏輯作業傳回為適用。 `Nested Loops` 是實體運算子。|  
|![非叢集索引刪除運算子圖示](../../2014/database-engine/media/nonclust-index-delete-32x.gif "非叢集索引刪除運算子圖示")|`Nonclustered Index Delete`|`Nonclustered Index Delete`運算子會從資料行中指定的非叢集索引刪除`Argument`輸入資料列。 `Nonclustered Index Delete` 是實體運算子。|  
|![非叢集索引插入運算子圖示](../../2014/database-engine/media/nonclust-index-insert-32x.gif "非叢集索引插入運算子圖示")|`Index Insert`|運算子`Index Insert`會將其輸入的資料`Argument`列插入資料行中指定的非叢集索引。 `Argument` 資料行也包含 SET:() 述詞，指出每一個資料行設定的值。 `Index Insert` 是實體運算子。|  
|![非叢集索引掃描運算子圖示](../../2014/database-engine/media/nonclustered-index-scan-32x.gif "非叢集索引掃描運算子圖示")|`Index Scan`|`Index Scan`運算子會從資料行中指定的非叢集索引抓取`Argument`所有的資料列。 如果資料行中出現選擇性的 WHERE： `Argument` （）述詞，則只會傳回滿足述詞的資料列。 `Index Scan` 是邏輯與實體運算子。|  
|![非叢集索引搜尋運算子圖示](../../2014/database-engine/media/index-seek-32x.gif "非叢集索引搜尋運算子圖示")|`Index Seek`|`Index Seek` 運算子使用索引的搜尋能力，從非叢集索引中擷取資料列。 資料`Argument`行包含所使用之非叢集索引的名稱。 它也包含 SEEK:() 述詞。 儲存引擎會使用索引來處理滿足 SEEK:() 述詞的資料列。 它可以選擇包含 WHERE:() 述詞，讓儲存引擎比對所有滿足 SEEK:() 述詞的資料列 (這麼做時不使用索引)。 如果資料`Argument`行包含已排序的子句，則查詢處理器已判定資料列必須依照非叢集索引的排序次序傳回。 如果沒有 ORDERED 子句，儲存引擎會以最適當的方式搜尋索引 (不保證輸出會依序排列)。 讓輸出維持次序會比產生不按次序的輸出還要沒有效率。 `Index Seek` 是邏輯與實體運算子。|  
|![非叢集索引多工緩衝處理運算子圖示](../../2014/database-engine/media/index-spool-32x.gif "非叢集索引多工緩衝處理運算子圖示")|**索引多工緩衝處理**|「**索引**多工緩衝處理」實體運算子在資料`Argument`行中包含 seek：（）述詞。 「**索引**多工緩衝處理」運算子會掃描其輸入資料列，並將每個資料列的複本放`tempdb`入隱藏的多工緩衝處理檔案中（儲存在資料庫中，而且只存在於查詢的存留期間），並在資料列上建立非叢集索引。 這讓您可以使用索引的搜尋能力來輸出滿足 SEEK:() 述詞的資料列。 如果重新倒轉運算子（例如，由`Nested Loops`運算子），但是不需要重新系結，則會使用多工緩衝處理的資料，而不是重新掃描輸入。|  
|![非叢集索引更新運算子圖示](../../2014/database-engine/media/nonclust-index-update-32x.gif "非叢集索引更新運算子圖示")|`Nonclustered Index Update`|`Nonclustered Index Update`實體運算子會從資料行中指定的非叢集索引中的輸入`Argument`更新資料列。 如果出現 SET:() 述詞，則每個更新的資料行都會設為這個值。 `Nonclustered Index Update` 是實體運算子。|  
|![線上索引插入運算子圖示](../../2014/database-engine/media/online-index-32x.gif "線上索引插入運算子圖示")|**線上索引插入**|「線上索引插入」**** 實體運算子指出索引之建立、改變或卸除作業將於線上進行。 也就是說，基礎資料表資料在索引操作期間仍然可供使用者使用。|  
|None|`Parallelism`|`Parallelism`運算子會執行散發資料流程、搜集資料流程，以及重新分割資料流程的邏輯作業。 資料`Argument`行可以包含 PARTITION columns：（）述詞，以及要分割的資料行清單（以逗號分隔）。 資料`Argument`行也可以包含 ORDER BY：（）述詞，列出資料分割期間要保留排序次序的資料行。 `Parallelism` 是實體運算子。<br /><br /> 注意：如果查詢已經編譯為平行查詢，但在執行時間是以序列查詢的形式執行，則 SET STATISTICS XML 或使用中[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]的 [ **Include 實際執行計畫**] 選項所產生的執行程式表輸出將不會`RunTimeInformation`包含`Parallelism`運算子的元素。 在 [ `Parallelism`設定統計資料設定檔輸出] 中，運算子的實際資料列計數和實際執行次數會顯示零。 發生任一種狀況時，這表示`Parallelism`運算子只會在查詢編譯期間使用，而不是在執行時間查詢計劃中。 請注意，如果伺服器上有大量的並行載入，平行查詢計畫有時會以序列方式執行。|  
|![參數資料表掃描運算子圖示](../../2014/database-engine/media/parameter-table-scan-32x.gif "參數資料表掃描運算子圖示")|`Parameter Table Scan`|`Parameter Table Scan` 運算子會掃描在目前的查詢中當做參數使用的資料表。 一般而言，這是用於預存程序中的 INSERT 查詢。 `Parameter Table Scan` 是邏輯與實體運算子。|  
|None|**部分彙總**|「部分彙總」**** 用於平行計畫。 它將彙總函式套用至盡可能最多的輸入資料列，因此不需要寫入磁碟 (稱為「溢出」)。 `Hash Match`是唯一會執行資料分割匯總的實體運算子（iterator）。 **部分彙總** 是邏輯運算子。|  
|![母體擴展查詢資料指標運算子圖示](../../2014/database-engine/media/poulation-query-32x.gif "母體擴展查詢資料指標運算子圖示")|`Population Query`|`Population Query` 運算子會在開啟資料指標時，擴展資料指標的工作資料表。|  
|![重新整理查詢資料指標運算子圖示](../../2014/database-engine/media/refresh-query-32x.gif "重新整理查詢資料指標運算子圖示")|`Refresh Query`|`Refresh Query` 運算子會在提取緩衝區中提取資料列目前的資料。|  
|![遠端刪除運算子圖示](../../2014/database-engine/media/remote-delete-32x.gif "遠端刪除運算子圖示")|`Remote Delete`|`Remote Delete` 運算子會刪除遠端物件的輸入資料列。 `Remote Delete` 是邏輯與實體運算子。|  
|![遠端索引搜尋執行程序表運算子](../../2014/database-engine/media/remote-index-scan-32x.gif "遠端索引搜尋執行程序表運算子")|**遠端索引掃描**|「遠端索引掃描」**** 運算子會掃描 Argument 資料行中所指定的遠端索引。 「遠端索引掃描」**** 是邏輯與實體運算子。|  
|![遠端索引搜尋執行程序表運算子](../../2014/database-engine/media/remote-index-seek-32x.gif "遠端索引搜尋執行程序表運算子")|**遠端索引搜尋**|「遠端索引搜尋」**** 運算子會使用遠端索引物件的搜尋功能來擷取資料列。 資料`Argument`行包含所使用的遠端索引名稱及 seek：（）述詞。 「遠端索引搜尋」**** 是邏輯實體運算子。|  
|![遠端插入運算子圖示](../../2014/database-engine/media/remote-insert-32x.gif "遠端插入運算子圖示")|**遠端插入**|「遠端插入」**** 運算子會將輸入資料列插入遠端物件。 「遠端插入」**** 是邏輯與實體運算子。|  
|![遠端查詢運算子圖示](../../2014/database-engine/media/remote-query-32x.gif "遠端查詢運算子圖示")|`Remote Query`|`Remote Query` 運算子會對遠端來源送出查詢。 傳送到遠端伺服器的查詢文字會出現在資料`Argument`行中。 `Remote Query` 是邏輯與實體運算子。|  
|![遠端掃描運算子圖示](../../2014/database-engine/media/remote-scan-32x.gif "遠端掃描運算子圖示")|`Remote Scan`|`Remote Scan` 運算子會掃描遠端物件。 遠端物件的名稱會出現在資料`Argument`行中。 `Remote Scan` 是邏輯與實體運算子。|  
|![遠端更新運算子圖示](../../2014/database-engine/media/remote-update-32x.gif "遠端更新運算子圖示")|`Remote Update`|`Remote Update` 運算子會更新遠端物件中的輸入資料列。 `Remote Update` 是邏輯與實體運算子。|  
|![重新分割資料流平行處理原則運算子圖示](../../2014/database-engine/media/parallelism-repartition-stream.gif "重新分割資料流平行處理原則運算子圖示")|**重新分割資料流**|「重新分割資料流」**** 運算子會消耗多個資料流，並產生多個記錄的資料流。 記錄內容與格式不會變更。 如果查詢最佳化工具使用點陣圖篩選，輸出資料流中的資料列數會減少。 輸入資料流的每個資料錄會被放入一個輸出資料流。 如果這個運算子要保留次序，那麼所有輸入資料流都必須排序好，而且合併成數個排序的輸出資料流。 如果輸出已分割，則`Argument`資料行包含 PARTITION columns：（）述詞和分割資料行。如果輸出經過排序，則`Argument`資料行包含 ORDER BY：（）述詞，以及要排序的資料行。 **重新分割資料流** 是邏輯運算子。 此運算子只用於平行查詢計畫。|  
|![結果語言項目圖示](../../2014/database-engine/media/result-32x.gif "結果語言項目圖示")|`Result`|`Result` 運算子是在查詢計畫結束時所傳回的資料。 這通常是 Showplan 的根元素。 `Result` 是語言元素。|  
|![RID 查閱運算子圖示](../../2014/database-engine/media/rid-nonclust-locate-32x.gif "RID 查閱運算子圖示")|`RID Lookup`|`RID Lookup` 是堆積上的書籤查閱，它會使用提供的資料列識別碼 (RID)。 `Argument`資料行包含書簽標籤，可用來查閱資料表中的資料列，以及查閱資料列的資料表名稱。 `RID Lookup` 一律都會伴隨 NESTED LOOP JOIN。 `RID Lookup` 是實體運算子。 如需書籤查閱的詳細資訊，請參閱 MSDN SQL Server 部落格中的[書籤查閱](https://go.microsoft.com/fwlink/?LinkId=132568)。|  
|None|`Right Anti Semi Join`|`Right Anti Semi Join` 運算子會在第一個 (上方) 輸入中沒有符合資料列存在時，輸出第二個 (下方) 輸入中的每一列。 相符的資料`Argument`列定義為符合資料行中述詞的資料列（如果沒有述詞存在，每個資料列都是相符的資料列）。 `Right Anti Semi Join` 是邏輯運算子。|  
|None|`Right Outer Join`|`Right Outer Join` 運算子所傳回的每個資料列，皆滿足第二個 (下方) 輸入與第一個 (上方) 輸入之每個相符資料列的聯結。 它也會傳回第二個輸入中與第一個輸入完全不相符的任何資料列，以 NULL 相聯結。 如果資料行中沒有聯結述`Argument`詞，則每個資料列都是相符的資料列。 `Right Outer Join` 是邏輯運算子。|  
|None|`Right Semi Join`|當第一個 (頂端) 輸入有相符的資料列時，`Right Semi Join` 運算子會從第二個 (底端) 輸入傳回每一個資料列。 如果資料行中沒有聯結述`Argument`詞，則每個資料列都是相符的資料列。 `Right Semi Join` 是邏輯運算子。|  
|![資料列計數多工緩衝處理運算子圖示](../../2014/database-engine/media/remote-count-spool-32x.gif "資料列計數多工緩衝處理運算子圖示")|**資料列計數多工緩衝處理**|「資料列計數多工緩衝處理」**** 運算子會掃描輸入、計算共有多少資料列，然後傳回一樣多但不含任何資料的資料列。 如果重點是檢查資料列是否存在，而不是資料列中是否包含資料，就可以使用這個運算子。 例如，如果`Nested Loops`運算子執行左方半聯結作業，而且聯結述詞會套用至內部輸入，則資料列計數多工緩衝處理可能會放在`Nested Loops`運算子內部輸入的頂端。 然後， `Nested Loops`運算子可以判斷資料列計數多工緩衝處理輸出多少資料列（因為不需要內部的實際資料）來決定是否要傳回外部資料欄。 「資料列計數多工緩衝處理」**** 是實體運算子。|  
|![區段運算子圖示](../../2014/database-engine/media/segment-32x.gif "區段運算子圖示")|**區段**|「區段」**** 是實體和邏輯運算子。 它會根據一或多個資料行的值，將輸入集分割為區段。 這些資料行在「區段」**** 運算子中會顯示為引數。 然後運算子一次會輸出一個區段。|  
|None|`Segment Repartition`|在平行查詢計畫中，有時候會有 Iterator 的概念區。 在這種區域內的所有 Iterator，都可以由平行執行緒來執行。 區域本身必須連續執行。 個別區域內的一些 `Parallelism` Iterator，稱為 `Branch Repartition`。 在兩個這種區域的界限上的 `Parallelism` Iterator，稱為 `Segment Repartition`。 `Branch Repartition` 和 `Segment Repartition` 是邏輯運算子。|  
|![序列運算子圖示](../../2014/database-engine/media/sequence-32x.gif "順序運算子圖示")|`Sequence`|`Sequence` 運算子會驅動大範圍的更新計畫。 在功能上，它會依序執行每個輸入 (由上而下)。 每個輸入通常是更新不同的物件。 它只會傳回來自最後一個 (下方) 輸入的資料列。 `Sequence` 是邏輯與實體運算子。|  
|![順序專案運算子圖示](../../2014/database-engine/media/sequence-project-32x.gif "順序專案運算子圖示")|`Sequence Project`|`Sequence Project` 運算子會加入資料行以執行已排序集合的計算。 它會根據一或多個資料行的值，將輸入集分割為區段。 然後運算子一次會輸出一個區段。 這些資料行在 `Sequence Project` 運算子中會顯示為引數。 `Sequence Project` 是邏輯與實體運算子。|  
|![快照集資料指標運算子圖示](../../2014/database-engine/media/snapshot-32x.gif "快照集資料指標運算子圖示")|**快照式**|「快照式」**** 運算子會建立一個資料指標，而不會看到其他人所做的變更。|  
|![排序運算子圖示](../../2014/database-engine/media/sort-32x.gif "排序運算子圖示")|`Sort`|`Sort`運算子會排序所有傳入的資料列。 如果`Argument`此作業移除重複專案，或 order by：（）述詞包含要排序的資料行清單（以逗號分隔），則此資料行包含 DISTINCT ORDER by：（）述詞。 如果將資料行依遞增順序排序，資料行前會加上 ASC 值，如果將資料行依遞減順序排序，資料行前會加上 DESC 值。 `Sort` 是邏輯與實體運算子。|  
|![分割運算子圖示](../../2014/database-engine/media/split-32x.gif "分割運算子圖示")|`Split`|`Split`運算子是用來優化更新處理。 它會將每個更新分割成一個刪除和一個插入作業。 `Split` 是邏輯與實體運算子。|  
|![多工緩衝處理運算子圖示](../../2014/database-engine/media/spool-32x.gif "多工緩衝處理運算子圖示")|**Spool**|多工**緩衝**處理運算子會將中繼查詢結果`tempdb`儲存到資料庫。|  
|![資料流彙總運算子圖示](../../2014/database-engine/media/stream-aggregate-32x.gif "資料流彙總運算子圖示")|`Stream Aggregate`|`Stream Aggregate` 運算子會依據一個或多個資料行將資料列分組，然後計算查詢所傳回的一個或多個彙總運算式。 這個運算子的輸出可稍後由查詢中的運算子參考，並/或傳回到用戶端。 `Stream Aggregate` 運算子需要其群組內的輸入項目依資料行排列。 如果資料因為前面的 `Sort` 運算子或因為已排序索引搜尋或掃描，而尚未進行排序，最佳化工具就會在這個運算子之前使用 `Sort` 運算子。 在中的 SHOWPLAN_ALL 語句或圖形執行計畫中[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]，GROUP BY 述詞中的資料行會列在`Argument`資料行中，而匯總運算式則會列在 [**定義的值**] 欄位中。 `Stream Aggregate` 是實體運算子。|  
|![切換運算子圖示](../../2014/database-engine/media/switch-32x.gif "切換運算子圖示")|**參數**|「參數」**** 是一種特殊類型的串連 Iterator，它有 *n* 個輸入。 運算式與每一個「參數」**** 運算子相關聯。 根據運算式的傳回值 (介於 0 和 *n*-1 之間)，「參數」**** 會將適當的輸入資料流複製到輸出資料流。 「參數」**** 的用途之一是實作查詢計畫，包括利用某些運算子向前快轉資料指標，例如 **TOP** 運算子。 「參數」**** 同時為邏輯和實體運算子。|  
|![資料表刪除運算子圖示](../../2014/database-engine/media/table-delete-32x.gif "資料表刪除運算子圖示")|`Table Delete`|`Table Delete`實體運算子會從查詢執行計畫之資料行中`Argument`所指定的資料表中刪除資料列。|  
|![資料表插入運算子圖示](../../2014/database-engine/media/table-insert-32x.gif "資料表插入運算子圖示")|`Table Insert`|運算子`Table Insert`會將其輸入的資料`Argument`列插入查詢執行計畫之資料行中所指定的資料表。 `Argument` 資料行也包含 SET:() 述詞，指出每一個資料行設定的值。 如果 `Table Insert` 沒有插入值的子系，則會從插入運算子本身取得插入的資料列。 `Table Insert` 是實體運算子。|  
|![資料表合併運算子](../../2014/database-engine/media/table-merge-32x.gif "資料表合併運算子")|**資料表合併**|「資料表合併」**** 運算子會將合併資料流套用到堆積中。 運算子會在運算子的`Argument`資料行中所指定的資料表中刪除、更新或插入資料列。 所執行的實際作業取決於運算子的`Argument`資料行中所指定之**ACTION**資料行的運行時間值。 「資料表合併」**** 是實體運算子。|  
|![資料表掃描運算子圖示](../../2014/database-engine/media/table-scan-32x.gif "資料表掃描運算子圖示")|`Table Scan`|`Table Scan`運算子會從查詢執行計畫之資料行中所`Argument`指定的資料表，抓取所有的資料列。 如果資料行中出現 WHERE：（ `Argument` ）述詞，則只會傳回滿足述詞的資料列。 `Table Scan` 是邏輯與實體運算子。|  
|![資料表多工緩衝處理運算子圖示](../../2014/database-engine/media/table-spool-32x.gif "資料表多工緩衝處理運算子圖示")|**資料表多工緩衝處理**|「資料表多工緩衝處理」**** 運算子會掃描輸入，並將每個資料列的複本放入隱藏的多工緩衝資料表 (儲存在 [tempdb](../relational-databases/databases/tempdb-database.md) 資料庫，直到查詢結束就不再存在)。 如果重新倒轉運算子（例如，由`Nested Loops`運算子），但是不需要重新系結，則會使用多工緩衝處理的資料，而不是重新掃描輸入。 「資料表多工緩衝處理」**** 是實體運算子。|  
|![資料表更新運算子圖示](../../2014/database-engine/media/table-update-32x.gif "資料表更新運算子圖示")|`Table Update`|`Table Update`實體運算子會更新查詢執行計畫之資料行所指定`Argument`資料表中的輸入資料列。 SET:() 述詞決定每個更新資料行的值。 在 SET 子句中或這個運算子中，以及這個查詢中的其他位置，皆可參考這些數值。|  
|![資料表值函式運算子圖示](../../2014/database-engine/media/table-valued-function-32x.gif "資料表值函式運算子圖示")|**資料表值函式**|「資料表值函式」**** 運算子會評估資料表值函數 ([!INCLUDE[tsql](../includes/tsql-md.md)] 或 CLR)，並將產生的資料列儲存至 [tempdb](../relational-databases/databases/tempdb-database.md) 資料庫。 當父反覆運算器要求資料列時，**資料表值函式**會從`tempdb`傳回資料列。<br /><br /> 含有呼叫資料表值函數的查詢會產生內含「資料表值函式」**** Iterator 的查詢計畫。 「資料表值函式」**** 可以使用不同的參數值進行評估：<br /><br /> 「資料表值函式 XML 讀取器」**** 可輸入 XML BLOB 作為參數，並以 XML 文件的順序，產生代表 XML 節點的資料列集。 其他的輸入參數可能會限制傳回給 XML 文件子集的 XML 節點。<br /><br /> 「含 XPath 篩選的資料表值函式 XML 讀取器」**** 是一種特別的「XML 讀取器資料表值函式」****，可將輸出限制為滿足 XPath 運算式的 XML 節點。<br /><br /> <br /><br /> 「資料表值函式」**** 是邏輯與實體運算子。|  
|![Top 運算子圖示](../../2014/database-engine/media/top-32x.gif "Top 運算子圖示")|**返回頁首**|「頂端」**** 運算子會掃描輸入，可能會根據排序的先後順序，只傳回指定數目或百分比的資料列。 此`Argument`資料行可以包含要檢查系結的資料行清單。 在更新計畫中，可使用「頂端」**** 運算子強行限制資料列數。 「頂端」**** 是邏輯與實體運算子。 「頂端」**** 是邏輯與實體運算子。|  
|None|**前 N 個排序**|「**前 n 個排序**」類似`Sort`于 iterator，不同之處在于只需要前*n*個數據列，而不是整個結果集。 若 *N* 值較小，[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 查詢執行引擎會嘗試在記憶體中執行整個排序作業。 若 *N*的值較大，則查詢執行引擎會訴諸比較一般性的排序方法，而不採用 *N* 作為參數。|  
|![擴充運算子 (UDX) 圖示](../../2014/database-engine/media/udx-32x.gif "擴充運算子 (UDX) 圖示")|`UDX`|擴充運算子 (UDX) 會在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]中實作許多 XQuery 和 XPath 作業的其中一項。 所有 UDX 運算子都是邏輯和實體運算子。<br /><br /> 擴充運算子 (UDX) `FOR XML` 用於序列化關聯式資料列集，它會在單一輸出資料列的單一 BLOB 資料行中，以 XML 表示法輸入這個資料列集。 這是一個會區分順序的 XML 彙總運算子。<br /><br /> 擴充運算子 (UDX) `XML SERIALIZER` 是區分順序的 XML 彙總運算子， 會以 XML 文件順序來輸入用於表示 XML 節點或 XQuery 純量的資料列，並在單一輸出資料列的單一 XML 資料行中產生序列化的 XML BLOB。<br /><br /> 擴充運算子 (UDX) `XML FRAGMENT SERIALIZER` 是特殊類型的 `XML SERIALIZER`，可用於處理輸入資料列，而此輸入資料列用於表示要插入至 XQuery 插入資料修改延伸模組的 XML 片段。<br /><br /> 擴充運算子 (UDX) `XQUERY STRING` 會評估用於表示 XML 節點之輸入資料列的 XQuery 字串值。 這是一個區分順序的字串彙總運算子。 它會輸出一個資料列以及多個資料行，每個資料行都代表含有輸入字串值的 XQuery 純量。<br /><br /> 擴充運算子 (UDX) `XQUERY LIST DECOMPOSER` 是 XQuery 清單分解運算子。 針對代表 XML 節點的每一個輸入資料列，會產生代表 XQuery 純量的一或多個資料列，而如果輸入是 XSD 清單類型，則包含清單元素值。<br /><br /> 擴充運算子 (UDX) `XQUERY DATA` 會評估表示 XML 節點之輸入的 XQuery fn:data() 函數。 這是一個區分順序的字串彙總運算子。 它會輸出一個資料列以及多個資料行，每個資料行都代表含有 **fn:data()** 結果的 XQuery 純量。<br /><br /> 擴充運算子 `XQUERY CONTAINS` 會評估表示 XML 節點之輸入的 XQuery fn:contains() 函數。 這是一個區分順序的字串彙總運算子。 它會輸出一個資料列以及多個資料行，每個資料行都代表含有 **fn:contains()** 結果的 XQuery 純量。<br /><br /> 擴充運算子`UPDATE XML NODE`會在 xml 類型的**modify （）** 方法中，更新 XQuery 取代資料修改延伸模組中的 xml 節點。|  
|None|**Union**|**Union** 運算子會掃描多個輸入，輸出掃描的每一資料列，並移除重複項。 **Union** 是邏輯運算子。|  
|![更新 (資料庫引擎) 運算子圖示](../../2014/database-engine/media/update-32x.gif "更新 (資料庫引擎) 運算子圖示")|`Update`|`Update`運算子會從查詢執行計畫之資料行所指定物件中的`Argument`每個資料列，更新其輸入。 `Update` 是邏輯運算子。 實體運算子是 `Table Update`、`Index Update` 或 `Clustered Index Update`。|  
|![While 語言項目圖示](../../2014/database-engine/media/while-32x.gif "While 語言項目圖示")|`While`|`While` 運算子會實作 [!INCLUDE[tsql](../includes/tsql-md.md)] while 迴圈。 `While` 是語言元素。|  
|![資料表多工緩衝處理運算子圖示](../../2014/database-engine/media/table-spool-32x.gif "資料表多工緩衝處理運算子圖示")|`Window Spool`|`Window Spool` 運算子會將每一列展開成一組資料列，分別代表與其關聯的視窗。 查詢中的 OVER 子句會定義查詢結果集中的視窗，以及一個計算視窗中各資料列值的視窗函數。 `Window Spool` 是邏輯與實體運算子。|  
  
  
