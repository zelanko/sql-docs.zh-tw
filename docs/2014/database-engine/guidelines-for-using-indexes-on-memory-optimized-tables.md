---
title: 使用記憶體最佳化資料表上的索引指導方針 |Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
helpviewer_keywords:
- hash indexes
ms.assetid: 16ef63a4-367a-46ac-917d-9eebc81ab29b
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 514b6c8fedb50417b8c4060cb45e73bfa88fdddb
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48094360"
---
# <a name="guidelines-for-using-indexes-on-memory-optimized-tables"></a>使用記憶體最佳化資料表索引的方針
  索引是用來有效率地存取 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 資料表中的資料。 指定正確的索引可以大幅提高查詢效能。 假設有以下的查詢範例：  
  
```tsql  
SELECT c1, c2 FROM t WHERE c1 = 1;  
```  
  
 如果 c1 資料行上沒有索引，[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 將必須掃描整個資料表 t，然後篩選滿足 c1=1 條件的資料列。 不過，如果資料行 c1 上有索引，[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 可以直接搜尋 1 的值並擷取資料列。  
  
 當搜尋具有特定值或值範圍的記錄來找出資料表中的一個或多個資料行時，[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 可以使用這些資料行上的索引來快速尋找對應的記錄。 以磁碟為基礎的資料表及記憶體最佳化的資料表都受益於索引。 但是，當使用記憶體最佳化資料表時，必須考量索引架構之間的一些差異。 (記憶體最佳化資料表的索引，稱為記憶體最佳化索引。)某些主要差異在於：  
  
-   必須使用建立記憶體最佳化的索引[CREATE TABLE &#40;TRANSACT-SQL&#41;](/sql/t-sql/statements/create-table-transact-sql)。 以磁碟為基礎的索引可以使用 `CREATE TABLE` 和 `CREATE INDEX` 建立。  
  
-   記憶體最佳化的索引只存在於記憶體中。 索引結構不會保存到磁碟，且索引作業不會記錄在交易記錄中。 在記憶體中建立記憶體最佳化的資料表時 (在 CREATE TABLE 期間及資料庫啟動期間)，便會建立索引結構。  
  
-   記憶體最佳化的索引本質上為涵蓋。 涵蓋表示所有資料行幾乎都包含在索引中，且記憶體最佳化資料表不需要書籤查閱。 記憶體最佳化的索引只會包含指向資料表資料結構中實際資料列的記憶體指標，而不是主索引鍵的參考。  
  
-   片段和填滿因數不適用於記憶體最佳化索引。 在以磁碟為基礎的索引中，片段指的是未按順序寫入磁碟的 B 型樹狀目錄中的頁面。 記憶體最佳化的索引不會寫入磁碟或從磁碟讀取。 以磁碟為基礎的 B 型樹狀目錄索引中的填滿因數指的是實體頁面結構填滿實際資料的程度。 記憶體最佳化的索引結構沒有固定大小的頁面。  
  
 記憶體最佳化索引有兩種類型︰  
  
-   非叢集雜湊索引，適用於點查閱。 如需有關雜湊索引的詳細資訊，請參閱 <<c0> [ 雜湊索引](hash-indexes.md)。  
  
-   非叢集索引，適用於範圍掃描和依序掃描。  
  
 有了雜湊索引，便會透過記憶體中的雜湊表來存取資料。 雜湊索引沒有頁面，而且一定有固定的大小。 不過，雜湊索引可以有空的雜湊值區，這樣會造成有限的空間浪費。 使用雜湊索引從查詢傳回的值，不會進行排序。 雜湊索引已為相等述詞進行索引搜尋最佳化，同時支援完整的索引掃描。  
  
 非叢集索引 (不是雜湊索引) 支援雜湊索引所支援的所有項目，而且還可在不等述詞 (例如大於或小於，以及排序順序) 上進行搜尋作業。 您可以根據索引建立時的指定順序進行資料列擷取。 如果索引的排序次序符合特定查詢所需的排序次序 (例如，索引鍵符合 ORDER BY 子句)，在查詢執行期間就不需要排序資料列。 記憶體最佳化的非叢集索引是單向索引，因此進行資料列擷取時，不支援與索引排序次序反向的排序次序。 例如，若將索引指定為 (c1 ASC)，您就無法以反向順序 (c1 DESC) 掃描索引。  
  
 每個索引都會耗用記憶體。 雜湊索引會耗用固定數量的記憶體，也就是值區計數的函數。 對於非叢集索引，記憶體耗用量是資料列計數和索引鍵資料行大小的函式，並視工作負載之不同，還有一些額外的負擔。 進行記憶體最佳化索引的記憶體，是除了用以儲存記憶體最佳化資料表中資料列的記憶體之外，額外的個別記憶體。  
  
 重複的鍵值一律會共用相同的雜湊值區。 如果雜湊索引包含許多重複的鍵值，所產生的長雜湊鏈結將危害到效能。 在這個案例中，發生在任何雜湊索引中的雜湊衝突將進一步降低效能。 基於這個理由，如果唯一索引鍵的數目小於至少 100 倍的資料列計數，您可以減少雜湊衝突的風險讓值區計數較大 (至少八次唯一的索引鍵的數目，請參閱[判斷雜湊索引的正確貯體計數](../../2014/database-engine/determining-the-correct-bucket-count-for-hash-indexes.md)如需詳細資訊) 或您可以使用非叢集索引來完全消除雜湊衝突。  
  
## <a name="determining-which-indexes-to-use-for-a-memory-optimized-table"></a>判斷哪些索引要用於記憶體最佳化的資料表  
 每個記憶體最佳化資料表至少必須有一個索引。 請注意，每個 PRIMARY KEY 條件約束都會隱含地建立索引。 因此，如果資料表有主索引鍵，就表示它有索引。 持久的記憶體最佳化的資料表需要主索引鍵。  
  
 查詢記憶體最佳化資料表時，雜湊索引在述詞子句只包含相等述詞時的效能更佳。 述詞必須包含雜湊索引鍵中的所有資料行。 若是不相等的述詞，雜湊索引會還原至掃描。  
  
 記憶體最佳化資料表中的資料行，可以是雜湊索引和非叢集索引的一部分。  
  
 利用不相等述詞查詢記憶體最佳化資料表時，非叢集索引的效能比非叢集雜湊索引的效能好。  
  
 雜湊索引需要索引鍵 (進行雜湊) 以在索引中尋找。 如果索引鍵包含兩個資料行，而您只提供了第一個資料行，[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 不會有完整的索引鍵可進行雜湊。 如此會導致索引掃描查詢計劃。 使用方法會決定應對哪些資料行編製索引。  
  
 非叢集索引的資料行若有許多資料列具有相同的值 (索引鍵資料行有許多重複的值)，效能可能會因為更新、插入及刪除而降低。  在此情況下，改善效能的其中一種方法就是在非叢集索引中加入其他資料行。  
  
### <a name="operations-on-memory-optimized-and-disk-based-indexes"></a>針對記憶體最佳化的索引以及以磁碟為基礎的索引所執行的作業。  
  
|作業|記憶體最佳化、非叢集雜湊、索引|記憶體最佳化的非叢集索引|磁碟型索引|  
|---------------|-------------------------------------------------|------------------------------------------|-----------------------|  
|索引掃描，擷取所有資料表資料列。|是|是|是|  
|等號比較述詞 (=) 的索引搜尋。|是<br /><br /> (需要完整金鑰。)|是 <sup>1</sup>|是|  
|索引搜尋不相等述詞 (>，<， \<=、 > =、 BETWEEN)。|否 (產生索引掃描)|是 <sup>1</sup>|是|  
|依照排序次序擷取符合索引定義的資料列。|否|是|是|  
|依照排序次序擷取符合相反索引定義的資料列。|否|否|是|  
  
 在表格中，「是」表示索引可以適當地為要求提供服務，「否」則表示無法順利使用索引來滿足要求。  
  
 <sup>1</sup>為非叢集記憶體最佳化的索引，完整的索引鍵不需要執行索引搜尋。 即使索引鍵有資料行順序，如果資料行的值出現在遺漏的資料行之後，仍會發生掃描。  
  
## <a name="index-count"></a>索引計數  
 記憶體最佳化的資料表最多可以有 8 個索引，包括使用主索引鍵建立的索引。  
  
 有關記憶體最佳化的資料表上建立的索引數目，請考慮以下事項：  
  
-   當您建立資料表時，指定您需要的索引。 在建立記憶體最佳化的資料表之後，您就無法為此資料表建立索引。 如果您想要在記憶體最佳化的資料表中加入索引，請卸除該資料表並重新建立。  
  
-   請勿建立您很少使用的索引：  
  
     如果資料表上的索引都經常使用，記憶體回收的效果最好。 很少使用的索引可能會造成記憶體回收系統對舊的資料列版本無法達到最佳執行效果。  
  
## <a name="creating-a-memory-optimized-index-code-samples"></a>建立記憶體最佳化索引：程式碼範例  
 資料行層級雜湊索引：  
  
```tsql  
CREATE TABLE t1   
   (c1 INT NOT NULL INDEX idx HASH WITH (BUCKET_COUNT = 100))   
   WITH (MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_ONLY)  
```  
  
 資料表層級雜湊索引：  
  
```tsql  
CREATE TABLE t1_1   
   (c1 INT NOT NULL,   
   INDEX IDX HASH (c1) WITH (BUCKET_COUNT = 100))   
   WITH (MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_ONLY)  
```  
  
 資料行層級主索引鍵雜湊索引：  
  
```tsql  
CREATE TABLE t2   
   (c1 INT NOT NULL PRIMARY KEY NONCLUSTERED HASH WITH (BUCKET_COUNT = 100))   
   WITH (MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_AND_DATA)  
```  
  
 資料表層級主索引鍵雜湊索引：  
  
```tsql  
CREATE TABLE t2_2   
   (c1 INT NOT NULL,   
   PRIMARY KEY NONCLUSTERED HASH (c1) WITH (BUCKET_COUNT = 100))   
   WITH (MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_AND_DATA)  
```  
  
 資料行層級非叢集索引：  
  
```tsql  
CREATE TABLE t3   
   (c1 INT NOT NULL INDEX ID)   
   WITH (MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_ONLY)  
```  
  
 資料表層級非叢集索引：  
  
```tsql  
CREATE TABLE t3_3   
   (c1 INT NOT NULL,   
   INDEX IDX NONCLUSTERED (c1))   
   WITH (MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_ONLY)  
```  
  
 資料行層級主索引鍵非叢集索引：  
  
```tsql  
CREATE TABLE t4   
   (c1 INT NOT NULL PRIMARY KEY NONCLUSTERED)   
   WITH (MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_AND_DATA)  
```  
  
 資料表層級主索引鍵非叢集索引：  
  
```tsql  
CREATE TABLE t4_4   
   (c1 INT NOT NULL,   
   PRIMARY KEY NONCLUSTERED (c1))   
   WITH (MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_AND_DATA)  
```  
  
 定義資料行之後所定義的多資料行索引：  
  
```tsql  
create table t (  
       a int not null constraint ta primary key nonclustered,  
       b int not null,  
       c int not null,  
       d int not null,  
       index idx_t_b_c_d nonclustered (b, c asc, d desc)  
) with (memory_optimized = on, durability = SCHEMA_AND_DATA)  
go  
```  
  
## <a name="see-also"></a>另請參閱  
 [記憶體最佳化資料表上的索引](../relational-databases/in-memory-oltp/memory-optimized-tables.md)   
 [判斷雜湊索引的正確貯體計數](../../2014/database-engine/determining-the-correct-bucket-count-for-hash-indexes.md)   
 [雜湊索引](hash-indexes.md)  
  
  
