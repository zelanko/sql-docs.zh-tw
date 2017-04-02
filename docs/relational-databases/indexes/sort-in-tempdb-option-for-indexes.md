---
title: "索引的 SORT_IN_TEMPDB 選項 | Microsoft Docs"
ms.custom: ""
ms.date: "02/17/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-indexes"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "SORT_IN_TEMPDB 選項"
  - "磁碟空間 [SQL Server], 索引"
  - "空間 [SQL Server], 索引"
  - "tempdb 資料庫 [SQL Server], 索引"
  - "索引 [SQL Server], tempdb 資料庫"
  - "索引建立 [SQL Server], tempdb 資料庫"
ms.assetid: 754a003f-fe51-4d10-975a-f6b8c04ebd35
caps.latest.revision: 26
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 26
---
# 索引的 SORT_IN_TEMPDB 選項
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  當您建立或重建索引時，可將 SORT_IN_TEMPDB 選項設為 ON，以便指示 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 使用 **tempdb** 來儲存用來建立索引的中繼排序結果。 雖然此選項會增加建立索引所使用的暫存磁碟空間數量，但只要 **tempdb** 所在的磁碟集與使用者資料庫不同，該選項就會減少建立或重建索引所需的時間。 如需 **tempdb** 的詳細資訊，請參閱[設定 index create memory 伺服器組態選項](../../database-engine/configure-windows/configure-the-index-create-memory-server-configuration-option.md)。  
  
## 索引建立階段  
 當 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 建立索引時，它將經歷下列階段：  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)] 會先掃描基底資料表的資料頁來擷取索引鍵值，然後替每個資料列建立索引分葉資料列。 當內部的排序緩衝區已填滿分葉索引項目，這些項目將進行排序並寫至磁碟中，作為中間的排序結果。 接著 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 將繼續進行資料頁掃描，直到排序緩衝區再次填滿為止。 此掃描多重資料頁、再跟著排序與寫入排序結果的模式將持續進行，直到基底資料表的所有資料列都處理完畢為止。  
  
     在叢集索引中，索引的分葉資料列為資料表的資料列，因此中繼的排序結果將包含所有的資料列。 在非叢集索引中，雖然分葉資料列可能會包含非索引鍵資料行，但通常還是比叢集索引小。 如果索引鍵很大，或索引中包含數個非索引鍵資料行，則非叢集的排序結果可能會很大。 如需包含非索引鍵資料行的詳細資訊，請參閱[建立內含資料行的索引](../../relational-databases/indexes/create-indexes-with-included-columns.md)。  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)] 會將索引分葉資料列的排序結果，合併成一個排序好的資料流。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的排序合併元件將開始於每個排序結果的第一頁，找出所有頁面中的最低索引鍵，並將該分葉資料列傳送給索引建立元件。 接著處理第二低的索引鍵，然後處理第三低，其餘依此類推。 當最後一個分葉索引資料列從排序結果分頁中擷取出來之後，該處理序將切換到該排序結果的下一頁。 當排序結果範圍的所有分頁都處理好之後，該範圍將被釋出。 當每個分葉索引資料列被傳至索引建立元件之後，將被加入到緩衝區的分葉索引頁面中。 每個分葉分頁將在填滿時被寫入。 當分葉頁面被寫入時，[!INCLUDE[ssDE](../../includes/ssde-md.md)] 也會建立索引的上層。 每個上層索引分頁將在填滿時被寫入。  
  
## SORT_IN_TEMPDB 選項  
 若 SORT_IN_TEMPDB 設為 OFF，排序結果將儲存於目標檔案群組中。 在建立索引的第一階段中，交替的基底資料表頁面讀取作業與排序結果寫入作業，會將磁碟讀寫頭從一個磁碟區域移到另一個磁碟區域。 掃描資料頁時，讀寫頭將位於資料頁區域中。 當排序緩衝區已填滿，並且目前的排序結果必須寫入磁碟時，它們將移到可用空間的區域，接著當資料表頁面掃描繼續進行時，再移回資料頁區域。 第二階段中的讀寫頭移動量比較大。 這時候，排序處理序通常會交替讀取每個排序結果區域。 目標檔案群組中將會同時建立排序結果和新的索引頁面。 這表示 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 在將讀取分散到各排序結果的同時，還必須定期跳到索引範圍，以在索引頁面填滿時寫入新的索引頁面。  
  
 若 SORT_IN_TEMPDB 選項設定為 ON，並且 **tempdb** 所在的磁碟集與目標檔案群組不同，那麼在第一階段中，發生資料頁讀取的磁碟將與寫入 **tempdb** 中之排序工作區域的磁碟不同。 這代表資料索引鍵的磁碟讀取動作一般會繼續循序地穿過磁碟來進行處理，而寫入 **tempdb** 磁碟的動作一般也是循序，如同建立最後索引的寫入動作一樣。 即使其他使用者正在使用資料庫並存取個別的磁碟位址，讀取與寫入的整體模式也會因著指定了 SORT_IN_TEMPDB 而比沒有指定來得有效率。  
  
 SORT_IN_TEMPDB 選項可改善索引範圍的接近程度，特別是當 CREATE INDEX 作業並未平行處理時。 排序工作區域範圍就它們在資料庫中的位置而言，將以有些隨機的方式釋出。 若排序工作區域包含於目標檔案群組中，那麼當排序工作範圍釋出時，您可藉由要求來取得它們，以便在建立索引時，使用這些範圍來保存索引結構。 這可將索引範圍的位置隨機化到某個程度。 若排序範圍個別地放在 **tempdb** 中，它們的釋出順序將與索引範圍的位置無關。 此外，當中繼的排序結果儲存於 **tempdb** 中，而非目標檔案群組時，目標檔案群組中將有更多可用空間。 這可增加索引範圍連續的機會。  
  
 SORT_IN_TEMPDB 選項只會影響目前的陳述式。 沒有任何中繼資料記錄索引是否排序於 **tempdb** 中。 例如，若您使用 SORT_IN_TEMPDB 選項來建立非叢集的索引，之後又以未指定該選項的方式來建立叢集索引，當 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 重新建立非叢集索引時，並不會使用該選項。  
  
> [!NOTE]  
>  若沒有執行排序作業的必要，或排序可以直接在記憶體中執行，則系統會忽略 SORT_IN_TEMPDB 選項。  
  
## 磁碟空間需求  
 當您將 SORT_IN_TEMPDB 選項設定為 ON 時，**tempdb** 中必須擁有足夠的可用磁碟空間，才能保存中繼的排序結果，目標檔案群組中也要有足夠的可用磁碟空間才能保存新的索引。 若沒有足夠的可用空間，並且由於某個原因，資料庫無法自動成長來取得更多空間 (例如磁碟中沒有空間，或自動成長被關閉)，CREATE INDEX 陳述式將會失敗。  
  
 若 SORT_IN_TEMPDB 設定為 OFF，目標檔案群組中的可用磁碟空間必須大約為最後索引的大小。 在第一階段中，排序結果將被建立，並且要求大約與最後索引相同的空間數量。 在第二個階段中，每個排序結果範圍都會在處理過後釋出。 這代表該排序結果範圍釋出的速度約和範圍被要求去保存最後索引頁面的速度一樣，因此整體的空間需求並不會大幅超過最後索引的大小。 它的一個副作用是若可用空間的數量非常接近最後索引的大小，[!INCLUDE[ssDE](../../includes/ssde-md.md)] 一般將重複使用剛剛才釋出的排序結果範圍。 因為排序結果範圍會以有些隨機的方式釋出，這將會減少在此案例中的索引範圍接近程度。 若 SORT_IN_TEMPDB 設定為 OFF，當目標檔案群組中擁有足夠的可用空間時，索引範圍的接近程度將會改善，這是因為索引範圍可從連續的集區中配置而得，而不用從剛剛取消配置的排序結果範圍來取得。  
  
 當您建立非叢集的索引時，您必須擁有足夠的可用空間：  
  
-   若 SORT_IN_TEMPDB 設定為 ON，**tempdb** 中必須有足夠的可用空間來儲存排序結果，目標檔案群組中也必須有足夠的可用空間來儲存最後的索引結構。 排序結果包含了索引的分葉資料列。  
  
-   若 SORT_IN_TEMPDB 設定為 OFF，目標檔案群組中的可用空間必須足夠儲存最後的索引結構。 若有更多的可用空間，索引範圍的接近程度將可改善。  
  
 當您在沒有非叢集索引的資料表上建立叢集索引時，您必須擁有足夠的可用空間：  
  
-   若 SORT_IN_TEMPDB 設定為 ON，**tempdb** 中必須有足夠的可用空間來儲存排序結果。 這包括了資料表的資料列。 目標檔案群組中必須有足夠的空間來儲存最後的索引結構。 這包括了資料表的資料列，以及索引的 B 型樹狀目錄。 您可能必須調整一些因數的估計，例如使用較大型的索引鍵，或是使用較小值的填滿因數。  
  
-   若 SORT_IN_TEMPDB 設定為 OFF，目標檔案群組中的可用空間必須足夠儲存最後的資料表。 這包括了索引結構。 若有更多的可用空間，資料表與索引範圍的接近程度將可改善。  
  
 當您在具有非叢集索引的資料表上建立叢集索引時，您必須擁有足夠的可用空間：  
  
-   若 SORT_IN_TEMPDB 設定為 ON，**tempdb** 中必須有足夠的可用空間來儲存最大索引 (通常是叢集索引) 排序結果的集合，目標檔案群組中也必須有足夠的可用空間來儲存所有索引的最後結構。 這包括了包含資料表資料列的叢集索引。  
  
-   若 SORT_IN_TEMPDB 設定為 OFF，目標檔案群組中的可用空間必須足夠儲存最後的資料表。 這包括了所有索引的結構。 若有更多的可用空間，資料表與索引範圍的接近程度將可改善。  
  
## 相關工作  
 [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)  
  
 [重新組織與重建索引](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md)  
  
## 相關內容  
 [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)  
  
 [設定 index create memory 伺服器組態選項](../../database-engine/configure-windows/configure-the-index-create-memory-server-configuration-option.md)  
  
 [索引 DDL 作業的磁碟空間需求](../../relational-databases/indexes/disk-space-requirements-for-index-ddl-operations.md)  
  
  