---
title: 建立及管理全文檢索索引 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- full-text indexes [SQL Server], about
ms.assetid: f8a98486-5438-44a8-b454-9e6ecbc74f83
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 164ddc7f11b37ce7b6325f177713e6d3eca8635b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63022492"
---
# <a name="create-and-manage-full-text-indexes"></a>建立及管理全文檢索索引
  全文檢索引擎會使用全文檢索索引中的資訊來編譯全文檢索查詢，以便快速地在資料表中搜尋特定字詞或字詞組合。 全文檢索索引會儲存重要單字及這些單字在資料庫資料表之一或多個資料行內位置的相關資訊。 全文檢索索引是一種特殊類型的 Token 式功能索引，由 Full-Text Engine for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]所建立與維護。 建立全文檢索索引的程序與建立其他索引類型的程序大不相同。 全文檢索引擎會根據個別 Token 從索引中的文字建立反向、堆疊以及壓縮的索引結構，而不是根據特定資料列中所儲存的值來建構 B 型樹狀結構。  全文檢索索引的大小只受限於執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體之電腦的可用記憶體資源。  
  
 從 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]開始，全文檢索索引會與 Database Engine 整合在一起，而非位於檔案系統中，如同舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 在新的資料庫中，全文檢索目錄現在是不屬於任何檔案群組的虛擬物件。它只是參考一組全文檢索索引的邏輯概念。 不過，請注意，在 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 資料庫 (含有資料檔案的任何全文檢索目錄) 的升級期間，系統會建立新的檔案群組。如需詳細資訊，請參閱 [升級全文檢索搜尋](upgrade-full-text-search.md)。  
  
> [!NOTE]  
>  在 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 及更新的版本中，全文檢索引擎位於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 處理序中，而非個別的服務中。 將全文檢索引擎整合到 Database Engine 可以改善全文檢索管理能力、混合式查詢的最佳化，以及整體效能。  
  
 每個資料表只允許有一個全文檢索索引。 若要對資料表建立全文檢索索引，該資料表必須有單一的非 Null 唯一資料行。 您可以針對 `char`、`varchar`、`nchar`、`nvarchar`、`text`、`ntext`、`image`、`xml`、`varbinary` 和 `varbinary(max)` 類型的資料行建立全文檢索索引，並且建立全文檢索搜尋的索引。 針對資料類型為 `varbinary`、`varbinary(max)`、`image` 或 `xml` 的資料行建立全文檢索索引會要求您指定類型資料行。 「類型資料行」是一個資料表資料行，您可以在每個資料列中儲存文件的副檔名 (.doc、.pdf 與 .xls 等)。  
  
 建立與維護全文檢索索引的程序稱為「母體擴展」，也稱為「搜耙」。 全文檢索索引母體擴展有三種類型：完整母體擴展、以變更追蹤為基礎的母體擴展，以及以時間戳記為基礎的累加母體擴展。 如需詳細資訊，請參閱 [擴展全文檢索索引](populate-full-text-indexes.md)。  
  
##  <a name="tasks"></a> 一般工作  
 **若要建立全文檢索索引**  
  
-   [CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-fulltext-index-transact-sql)  
  
 **改變全文檢索索引**  
  
-   [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-fulltext-index-transact-sql)  
  
 **若要卸除全文檢索索引**  
  
-   [DROP FULLTEXT INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-fulltext-index-transact-sql)  
  
 [本主題內容](#top)  
  
##  <a name="structure"></a> 全文檢索索引結構  
 若能充分了解全文檢索索引的結構，將有助於了解全文檢索引擎的運作方式。 本主題會使用下列 **之** Document [!INCLUDE[ssSampleDBCoShort](../../includes/sssampledbcoshort-md.md)] 資料表的摘錄當做範例資料表。 這個摘錄只會顯示該資料表中的兩個資料行 ( **DocumentID** 資料行和 **Title** 資料行) 和三個資料列。  
  
 就本例而言，我們會假設已經在 **Title** 資料行中建立了全文檢索索引。  
  
|DocumentID|標題|  
|----------------|-----------|  
|1|Crank Arm and Tire Maintenance|  
|2|Front Reflector Bracket and Reflector Assembly 3|  
|3|Front Reflector Bracket Installation|  
  
 例如，下表 (顯示片段 1) 會描述針對 **Document** 資料表之 **Title** 資料行所建立的全文檢索索引內容。 全文檢索索引所包含的資訊會比顯示在此資料表中的資訊還要多。 此資料表是全文檢索索引的邏輯表示法，僅針對示範目的提供。 這些資料列會以壓縮的格式儲存，以便最佳化磁碟使用量。  
  
 請注意，資料已經與原始文件相反。 因為關鍵字會對應至文件識別碼，所以會發生相反的情況。 因此，全文檢索索引通常稱為反向索引。  
  
 此外，請注意，關鍵字 "and" 已經從全文檢索索引中移除了。 進行此作業的原因是 "and" 是停用字詞，而且從全文檢索索引中移除停用字詞可能會大幅節省磁碟空間，進而改善查詢效能。 如需停用字詞的詳細資訊，請參閱 [設定及管理全文檢索搜尋的停用字詞與停用字詞表](configure-and-manage-stopwords-and-stoplists-for-full-text-search.md)。  
  
 **片段 1**  
  
|關鍵字|ColId|DocId|出現次數|  
|-------------|-----------|-----------|----------------|  
|Crank|1|1|1|  
|Arm|1|1|2|  
|Tire|1|1|4|  
|維護|1|1|5|  
|Front|1|2|1|  
|Front|1|3|1|  
|Reflector|1|2|2|  
|Reflector|1|2|5|  
|Reflector|1|3|2|  
|Bracket|1|2|3|  
|Bracket|1|3|3|  
|組件|1|2|6|  
|3|1|2|7|  
|安裝|1|3|4|  
  
 **Keyword** 資料行包含編列索引時所擷取的單一 Token 表示法。 文字分隔會決定 Token 的組成項目。  
  
 **ColId** 資料行所包含的值會對應到已建立全文檢索索引的特定資料行。  
  
 `DocId`資料行包含對應至特定全文檢索索引鍵值全文檢索索引資料表中的八位元組整數的值。 當全文檢索索引鍵不是整數資料類型時，這項對應就是必要的。 在此情況下，全文檢索停用字之間的對應索引鍵值和`DocId`會在稱為 DocId Mapping 資料表的個別資料表中保留的值。 若要查詢這些對應，請使用 [sp_fulltext_keymappings](/sql/relational-databases/system-stored-procedures/sp-fulltext-keymappings-transact-sql) 系統預存程序。 為了滿足搜尋條件，上述資料表中的 DocId 值必須與 DocId Mapping 資料表聯結，以便從查詢的基底資料表中擷取資料列。 如果基底資料表的全文檢索索引鍵值是整數類型，此值就會直接當做 DocId 而且不需要任何對應。 因此，使用整數全文檢索索引鍵值有助於最佳化全文檢索查詢。  
  
 **Occurrence** 資料行包含整數值。 針對每個 DocId 值，都會有一個對應到該 DocId 內特定關鍵字之相對單字位移的出現次數值清單。 出現次數值有助於決定詞句或相似的相符項目，例如，具有鄰近發生次數值的片語。 它們也有助於計算相關分數。例如，在 DocId 中的關鍵字出現次數可用來計分。  
  
 [本主題內容](#top)  
  
##  <a name="fragments"></a> 全文檢索索引片段  
 邏輯全文檢索索引通常會在多份內部資料表之間分割。 每份內部資料表會稱為全文檢索索引片段。 其中某些片段可能包含比其他片段更新的資料。 例如，如果使用者更新 DocId 為 3 的下列資料列，而且資料表已進行自動變更追蹤，就會建立新的片段。  
  
|DocumentID|標題|  
|----------------|-----------|  
|3|Rear Reflector|  
  
 在下列範例 (顯示片段 2) 中，此片段包含的 DocId 3 相關資料比片段 1 更新。 因此，當使用者查詢 "Rear Reflector" 時，片段 2 的資料就會用於 DocId 3。 每個片段都會以建立時間戳記標示，而且您可以使用 [sys.fulltext_index_fragments](/sql/relational-databases/system-catalog-views/sys-fulltext-index-fragments-transact-sql) 目錄檢視，查詢此時間戳記。  
  
 **片段 2**  
  
|關鍵字|ColId|DocId|Occ|  
|-------------|-----------|-----------|---------|  
|Rear|1|3|1|  
|Reflector|1|3|2|  
  
 如片段 2 所示，全文檢索查詢必須在內部查詢每個片段並捨棄較舊的項目。 因此，如果全文檢索索引包含過多全文檢索索引片段，可能會導致查詢效能大幅降低。 若要減少片段的數目，請使用 [ALTER FULLTEXT CATALOG](/sql/t-sql/statements/alter-fulltext-catalog-transact-sql)[!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式的 REORGANIZE 選項來重新組織全文檢索目錄。 這個陳述式會執行「主要合併」，將片段合併成較大的單一片段，然後從全文檢索索引中移除所有已過時的項目。  
  
 重新組織之後，範例索引就會包含下列資料列：  
  
|關鍵字|ColId|DocId|Occ|  
|-------------|-----------|-----------|---------|  
|Crank|1|1|1|  
|Arm|1|1|2|  
|Tire|1|1|4|  
|維護|1|1|5|  
|Front|1|2|1|  
|Rear|1|3|1|  
|Reflector|1|2|2|  
|Reflector|1|2|5|  
|Reflector|1|3|2|  
|Bracket|1|2|3|  
|組件|1|2|6|  
|3|1|2|7|  
  
 [本主題內容](#top)  
  
  
