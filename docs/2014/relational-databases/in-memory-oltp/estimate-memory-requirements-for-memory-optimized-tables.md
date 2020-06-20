---
title: 估計記憶體最佳化資料表的記憶體需求 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 5c5cc1fc-1fdf-4562-9443-272ad9ab5ba8
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 12fdb1a41ec764a0fee0817940f95a3d303777e4
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85050195"
---
# <a name="estimate-memory-requirements-for-memory-optimized-tables"></a>估計記憶體最佳化資料表的記憶體需求
  不論您是建立新的 [!INCLUDE[hek_2](../../includes/hek-2-md.md)] 記憶體優化資料表，或是將現有的磁片資料表遷移至記憶體優化資料表，都一定要有合理的估計值來滿足每個資料表的記憶體需求，讓您可以使用足夠的記憶體來布建伺服器。 本節描述如何估計保存記憶體最佳化資料表的資料所需的記憶體數目。  
  
 如果您想從磁碟資料表移轉至記憶體最佳化資料表，請在進行本主題之前，先參閱 [判斷是否應將資料表或預存程序匯出至記憶體中 OLTP](determining-if-a-table-or-stored-procedure-should-be-ported-to-in-memory-oltp.md) 主題，以取得最適合移轉之資料表的指引。 [移轉至 In-Memory OLTP](migrating-to-in-memory-oltp.md) 底下的所有主題，提供從磁碟資料表移轉至記憶體最佳化資料表的指引。  
  
## <a name="sections-in-this-topic"></a>本主題的章節  
  
-   [記憶體最佳化資料表範例](#bkmk_ExampleTable)  
  
-   [配置給資料表的記憶體](#bkmk_MemoryForTable)  
  
-   [配置給索引的記憶體](#bkmk_IndexMeemory)  
  
-   [配置給資料列版本設定的記憶體](#bkmk_MemoryForRowVersions)  
  
-   [配置給資料表變數的記憶體](#bkmk_TableVariables)  
  
-   [配置給成長的記憶體](#bkmk_MemoryForGrowth)  
  
##  <a name="example-memory-optimized-table"></a><a name="bkmk_ExampleTable"></a>記憶體優化資料表範例  
 請考慮下列記憶體最佳化資料表結構描述：  
  
```sql  
  
CREATE TABLE t_hk (  
col1 int NOT NULL PRIMARY KEY NONCLUSTERED,  
col2 int NOT NULL INDEX t1c2_index   
     HASH WITH (bucket_count = 5000000),  
col3 int NOT NULL INDEX t1c3_index   
     HASH WITH (bucket_count = 5000000),  
col4 int NOT NULL INDEX t1c4_index   
     HASH WITH (bucket_count = 5000000),  
col5 int NOT NULL INDEX t1c5_index NONCLUSTERED,  
col6 char (50) NOT NULL,  
col7 char (50) NOT NULL,   
col8 char (30) NOT NULL,   
col9 char (50) NOT NULL  
     WITH (memory_optimized = on)  
GO  
  
```  
  
 我們將透過此結構描述，來判斷此記憶體最佳化資料所需的最小記憶體。  
  
##  <a name="memory-for-the-table"></a><a name="bkmk_MemoryForTable"></a>資料表的記憶體  
 記憶體最佳化資料表資料列包含三個部分：  
  
-   **時間戳記**   
    資料列標頭/時間戳記 = 24 個位元組。  
  
-   **索引指標**   
    針對資料表中的每個雜湊索引，每個資料列具有 8 位元組位址指標，指向索引的下一個資料列。  由於有 4 個索引，因此每個資料列都會配置 32 個位元組給索引指標 (每個索引有 8 位元組指標)。  
  
-   **Data**   
    資料列的資料部分大小是由每個資料行的類型大小總和來判斷。  在資料表中，我們有五個 4 位元組整數、三個 50 位元組字元資料行，以及一個 30 位元組字元資料行。  因此，每個資料列的資料部分為 4 + 4 + 4 + 4 + 4 + 50 + 50 + 30 + 50 (或 200) 個位元組。  
  
 以下是記憶體最佳化資料表中 5,000,000 (5 百萬) 個資料列的大小計算。 資料列所使用的記憶體總數估計如下：  
  
 **配置給資料表資料列的記憶體**  
  
 從上述計算得知，記憶體最佳化資料表的每個資料列大小為 24 + 32 + 200 (或 256) 個位元組。  由於我們有 5 百萬個資料列，因此資料表會耗用 5,000,000 * 256 (或 1,280,000,000) 個位元組，大約是 1.28 GB。  
  
##  <a name="memory-for-indexes"></a><a name="bkmk_IndexMeemory"></a>索引的記憶體  
 **配置給每個雜湊索引的記憶體**  
  
 每個雜湊索引是 8 位元組位址指標的雜湊陣列。  陣列的大小是由該索引的唯一索引值數目來判斷；例如，t1c2_index 的陣列大小可以從唯一的 Col2 值數目開始。 雜湊陣列太大會浪費記憶體。  雜湊陣列太小會降低效能，因為雜湊處理至相同索引的索引值會引起太多衝突。  
  
 雜湊索引的等式查閱速度很快，例如：  
  
```sql  
  
SELECT * FROM t_hk  
   WHERE Col2 = 3  
  
```  
  
 非叢集索引的範圍查閱更快，例如：  
  
```sql  
  
SELECT * FROM t_hk  
   WHERE Col2 >= 3  
  
```  
  
 如果您想移轉磁碟資料表，您可以使用下列程式碼來判斷 index t1c2_index 的唯一值數目。  
  
```sql  
  
SELECT COUNT(DISTINCT [Col2])  
  FROM t_hk  
  
```  
  
 如果您想建立新的資料表，則需要估計陣列大小，或在部署前從測試收集資料。  
  
 如需雜湊索引在 [!INCLUDE[hek_2](../../includes/hek-2-md.md)] 記憶體最佳化資料表中運作方式的相關資訊，請參閱 [雜湊索引](../../database-engine/hash-indexes.md)。  
  
 **注意：** 您無法即時變更雜湊索引陣列大小。 若要變更雜湊索引陣列大小，您必須卸除資料表、變更 bucket_count 值，然後重新建立資料表。  
  
 **設定雜湊索引陣列大小**  
  
 雜湊陣列大小是由 `(bucket_count= <value>)` 設定，其中 \<value> 是大於零的整數值。 如果 \<value> 不是 2 的乘冪，實際的 bucket_count 會無條件進位到下一個最接近的 2 的乘冪。  在我們的範例資料表中（bucket_count = 5000000），因為5000000不是2的乘冪，所以實際的值區計數會無條件進位到8388608（2<sup>23</sup>）。  計算雜湊陣列所需的記憶體時，您必須使用此數值，而不是 5,000,000。  
  
 因此在此範例中，每個雜湊陣列所需的記憶體為：  
  
 8388608 * 8 = 2<sup>23</sup> \* 8 = 2<sup>23</sup> \* 2<sup>3</sup> = 2<sup>26</sup> = 67108864 或大約 64 MB。  
  
 由於我們有三個雜湊索引，因此雜湊索引所需的記憶體為 3 * 64MB = 192MB。  
  
 **非叢集索引的記憶體**  
  
 非叢集索引會以 BTree 實作，其內部節點包含索引值，以及指向後續節點的指標。  分葉節點包含索引值，以及一個指向記憶體中資料表資料列的指標。  
  
 不同於雜湊索引，非叢集索引沒有固定的貯體大小。 此索引會隨資料動態成長和壓縮。  
  
 非叢集索引所需的記憶體，計算方式如下：  
  
-   **配置給非分葉節點的記憶體**   
    在一般組態中，配置給非分葉節點的記憶體只佔索引所使用之整體記憶體的很小比例。 因為很小，所以可以放心忽略。  
  
-   **分葉節點的記憶體**   
    分葉節點中對於資料表內的每個唯一索引鍵都有一個資料列，指向該唯一索引鍵的資料列。  如果相同索引鍵有多個資料列 (亦即有非唯一的非叢集索引)，則索引分葉節點中只有一個資料列會指向其中一個資料列，而其他資料列會彼此連結。  因此，所需的總記憶體大約是：   
    memoryForNonClusteredIndex = (pointerSize + sum(keyColumnDataTypeSizes)) * rowsWithUniqueKeys  
  
 非叢集索引最適合用於範圍查閱，如下列查詢所示：  
  
```sql  
  
SELECT * FROM t_hk  
   WHERE c2 > 5  
```  
  
##  <a name="memory-for-row-versioning"></a><a name="bkmk_MemoryForRowVersions"></a>用於資料列版本設定的記憶體  
 更新或刪除資料列時，記憶體中 OLTP 會使用開放式並行存取來避免鎖定。 這表示當更新資料列時，會建立該資料列的其他版本。 在可能使用舊版本的所有交易完成執行之前，系統會保留舊版本可用。 刪除資料列時，系統會以類似更新的方式來執行，並保留版本可用，直到不再需要為止。 讀取和插入並不會建立額外的資料列版本資料。  
  
 由於等待記憶體回收循環釋放記憶體時，記憶體中可能會有許多其他的資料列，因此您必須有足夠的記憶體來容納這些其他的資料列。  
  
 您可以計算每秒更新和刪除的最大資料列數目，然後乘以最久的交易所需的秒數 (至少為 1)，來估計其他資料列的數目。  
  
 該值接著會乘以資料列大小，以取得設定資料列版本設定所需的位元組數目。  
  
 `rowVersions = durationOfLongestTransactionInSeconds * peakNumberOfRowUpdatesOrDeletesPerSecond`  
  
 接著會將過時資料列數目乘以記憶體優化資料表資料列的大小，來估計過時資料列的記憶體需求（請參閱上[表的記憶體](#bkmk_MemoryForTable)）。  
  
 `memoryForRowVersions = rowVersions * rowSize`  
  
##  <a name="memory-for-table-variables"></a><a name="bkmk_TableVariables"></a>資料表變數的記憶體  
 資料表變數所使用的記憶體只會在資料表變數超出範圍時釋出。 從資料表變數中刪除的資料列 (包括隨更新刪除的資料列) 則不受記憶體回收限制。 在資料表變數離開範圍之前，不會釋出記憶體。  
  
 在大型 SQL 批次中定義的資料表變數 (與程序範圍相反) 會在許多交易中使用，且可能會耗用大量的記憶體。 由於它們不會進行記憶體回收，因此資料表變數中已刪除的資料列可能會耗用大量記憶體並降低效能，因為讀取作業需要掃描已刪除的資料列。  
  
##  <a name="memory-for-growth"></a><a name="bkmk_MemoryForGrowth"></a>成長的記憶體  
 上述計算依資料表的現狀來估計資料表的記憶體需求。 除了此記憶體之外，您還需要估計資料表的成長，並提供足夠的記憶體來容納該成長幅度。  例如，如果您預期會成長 10%，則需要將上述結果乘以 1.1，以取得資料表所需的總記憶體。  
  
## <a name="see-also"></a>另請參閱  
 [移轉至 In-Memory OLTP](migrating-to-in-memory-oltp.md)  
  
  
