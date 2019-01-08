---
title: 全文檢索搜尋升級選項 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
f1_keywords:
- Full-Text Search
- Upgrade options, Full-Text Search
ms.assetid: 16c9376b-5fbb-4495-a429-06a2493849c9
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: abe169a69cd8c247ba74a24b8e80c3202fa2d5f5
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2018
ms.locfileid: "52511307"
---
# <a name="full-text-search-upgrade-options"></a>全文檢索搜尋升級選項
  您可以使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝精靈的 [全文檢索搜尋升級選項] 頁面，針對此時升級的資料庫選取要使用的全文檢索搜尋升級選項。  
  
 在 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 中，每個全文檢索索引都位於屬於檔案群組、具有實體路徑而且被視為資料庫檔案的全文檢索目錄中。 現在，全文檢索目錄是邏輯概念的虛擬物件-，這是指一組全文檢索索引。 因此，新的全文檢索目錄不會被視為具有實體路徑的資料庫檔案。 不過，在升級含有資料檔案的任何全文檢索目錄期間，系統會在相同的磁碟上建立新的檔案群組。 這會在升級之後保留舊磁碟 I/O 行為。 如果根路徑存在，則任何來自該目錄的全文檢索索引都會放置於新的檔案群組中。 如果舊的全文檢索目錄路徑無效，升級作業就會將全文檢索索引保留在與基底資料表相同的檔案群組中，或是保留在分割區資料表的主要檔案群組中。  
  
## <a name="options"></a>選項。  
 當您升級為 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]時，請選擇下列其中一個全文檢索升級選項。  
  
 **匯入**  
 匯入全文檢索目錄。 一般而言，匯入的速度明顯比重建的速度更快。 例如，只有使用一個 CPU 時，匯入的執行速度大約比重建的速度快 10 倍。 不過，從 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 匯入的全文檢索目錄並不會使用新增的強化斷詞工具，所以您最後可能會想要重建全文檢索目錄。  
  
> [!NOTE]  
>  重建可以在多執行緒模式中執行，而且如果有 10 個以上的 CPU 可用，當您允許重建使用所有 CPU 時，重建的執行速度可能會比匯入的速度更快。  
  
 如果無法使用全文檢索目錄，將會重建關聯的全文檢索索引。 只有針對 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 資料庫才可以使用此選項。  
  
 如需有關匯入全文檢索索引之影響的詳細資訊，請參閱本主題後面的「選擇全文檢索升級選項的考量」。  
  
 **Rebuild**  
 全文檢索目錄會使用新的增強斷詞工具重建。 重建索引可能需要很長的時間，而且在升級之後可能需要相當多的 CPU 和記憶體。  
  
 **重設**  
 重設全文檢索目錄。 從 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]進行升級時，全文檢索目錄檔案會遭到移除，但是全文檢索目錄和全文檢索索引的中繼資料則會保留。 在升級之後，所有的全文檢索索引都會停用變更追蹤，而且不會自動啟動搜耙。 當您在升級完成之後手動發出完整母體擴展之前，此目錄將會維持空白狀態。  
  
 所有的這些升級選項都可確保升級的資料庫可完全獲益於全文檢索效能增強功能。  
  
## <a name="considerations-for-choosing-a-full-text-upgrade-option"></a>選擇全文檢索升級選項的考量  
 當您為升級作業選擇升級選項時，請考慮下列事項：  
  
-   您如何使用斷詞工具？  
  
     [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中的全文檢索搜尋服務包括斷詞工具和字幹分析器。 這些項目可能會針對特定文字模式或狀況，變更從 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 全文檢索查詢的結果。 因此，在選擇適當的升級選項時，您如何使用斷詞工具便很重要：  
  
    -   如果您所使用之全文檢索語言的斷詞工具並未變更，或者重新叫用精確度對您不重要，則適合進行匯入。 之後，如果您遇到任何重新叫用的問題，只要透過重建全文檢索目錄，就可以升級為新的斷詞工具。  
  
    -   如果您很重視重新叫用精確度，並使用在 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]之後加入的其中一個斷詞工具，則適合進行重建。  
  
-   是否有任何全文檢索索引建立在整數全文檢索索引鍵資料行上？  
  
     重建會執行內部最佳化，以便在某些情況中改善已升級之全文檢索索引的查詢效能。 具體而言，如果您擁有包含全文檢索索引的全文檢索目錄，其中基底資料表的全文檢索索引鍵資料行是整數資料類型，則重建會在升級之後達到理想的全文檢索查詢效能。 在此情況中，我們強烈建議您使用 **[重建]** 選項。  
  
    > [!NOTE]  
    >  若為 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]中的全文檢索索引，我們建議當做全文檢索索引鍵的資料行必須是整數資料類型。 如需詳細資訊，請參閱 [改善全文檢索索引的效能](../../relational-databases/indexes/indexes.md)。  
  
-   將伺服器執行個體保持在線上狀態的優先權為何？  
  
     在升級期間匯入或重建會耗用大量 CPU 資源，因而延遲將其餘伺服器執行個體升級並保持在線上狀態的時間。 如果盡可能將伺服器執行個體保持在線上狀態很重要，而且您願意在升級之後執行手動母體擴展，則適合使用 **[重設]** 。  
  
## <a name="additional-resources"></a>其他資源  
  
