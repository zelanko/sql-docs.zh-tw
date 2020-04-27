---
title: 記憶體最佳化建議程式 | Microsoft Docs
ms.custom: ''
ms.date: 10/26/2015
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
f1_keywords:
- sql12.swb.memoryoptimizationwizard.f1
- swb.memoryoptimizationwizard.f1
ms.assetid: 181989c2-9636-415a-bd1d-d304fc920b8a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1d2fe137a21f2bd48113e65524b4315494f40a49
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "63157997"
---
# <a name="memory-optimization-advisor"></a>記憶體最佳化 Advisor
  交易效能報告工具 (請參閱＜ [Determining if a Table or Stored Procedure Should Be Ported to In-Memory OLTP](determining-if-a-table-or-stored-procedure-should-be-ported-to-in-memory-oltp.md)＞) 會通知您，匯出使用記憶體中 OLTP 時資料庫中哪些資料表有加分效果。 識別您要匯出使用記憶體中 OLTP 的資料表之後，即可使用 Memory Optimization Advisor，協助您將以磁碟為基礎的資料庫資料表移轉到記憶體中 OLTP。  
  
 開始時，請先連接至執行個體，其中包含以磁碟為基礎的資料庫資料表。 您可連接到 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 或 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 執行個體。 不過，如果您想要使用 Advisor 執行移轉作業，則必須連接到已啟用 In-Memory OLTP 功能的 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 執行個體。 如需有關記憶體中 OLTP 需求的詳細資訊，請參閱＜ [Requirements for Using Memory-Optimized Tables](memory-optimized-tables.md)＞。  
  
 如需移轉方法的資訊，請參閱 [In-Memory OLTP - 一般工作負載模式和移轉考量](https://msdn.microsoft.com/library/dn673538.aspx)。  
  
## <a name="walkthrough-using-the-memory-optimization-advisor"></a>使用記憶體最佳化 Advisor 的逐步解說  
 在 **[物件總管]** 中，以滑鼠右鍵按一下您想要轉換的資料表，然後選取 **[記憶體最佳化 Advisor]**。 隨即顯示 **[資料表記憶體最佳化 Advisor]** 的歡迎頁面。  
  
### <a name="memory-optimization-checklist"></a>記憶體最佳化檢查清單  
 按一下 **[資料表記憶體最佳化 Advisor]** 歡迎頁面中的 **[下一步]** 時，即會看到記憶體最佳化檢查清單。 記憶體最佳化的資料表不支援磁碟資料表的全部功能。 記憶體最佳化檢查清單會報告磁碟資料表是否使用任何與記憶體最佳化資料表不相容的功能。 **資料表記憶體最佳化 Advisor** 並不會修改磁碟資料表，以便將其移轉為使用 In-Memory OLTP。 您必須先進行變更才能繼續移轉。 針對每個發現的不相容狀況， **資料表記憶體最佳化 Advisor** 會顯示有助於修改以磁碟為基礎的資料表之相關資訊的連結。  
  
 如果您想要保留這些不相容狀況的清單以便規劃移轉，請按一下 **[產生報告]** ，即可產生 HTML 清單。  
  
 如果資料表沒有不相容的狀況，而且您已使用記憶體中 OLTP 連接到 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 執行個體，請按 **[下一步]**。  
  
### <a name="memory-optimization-warnings"></a>記憶體最佳化警告  
 在下一頁的記憶體最佳化警告中包含一份問題清單，這些問題對資料表移轉為使用記憶體中 OLTP 並無影響，但卻可能導致其他物件 (例如預存程序或 CLR 函數) 行為失敗或產生非預期的行為。  
  
 清單一開始出現的幾個警告都是參考用的，因此可能不適用於您的資料表。 資料表右邊資料行中的連結會帶領您前往詳細資訊。  
  
 這個警告表也會顯示您的資料表中尚未出現的潛在警告狀況。  
  
 可付諸行動的警告會在左邊資料行中出現一個黃色的三角形。 如果有可付諸行動的警告，您應該結束移轉、解決警告，然後重新啟動程序。 如果您沒有解決警告，移轉的資料表可能會導致失敗。  
  
 按一下 **[產生報告]** 即可產生這些警告的 HTML 報告。 按 **[下一步]** 以繼續。  
  
### <a name="review-optimization-options"></a>檢閱最佳化選項  
 下一個畫面可讓您修改選項以便移轉至 In-Memory OLTP：  
  
 記憶體最佳化的檔案群組  
 您的記憶體最佳化檔案群組名稱。 資料庫必須具備一個記憶體最佳化的檔案群組 (其中至少包含一個檔案)，才能建立記憶體最佳化的資料表。  
  
 如果您沒有記憶體最佳化的檔案群組，即可變更預設名稱。 不可刪除記憶體最佳化的檔案群組。 記憶體最佳化檔案群組的存在可能會停用某些資料庫層級功能 (例如 AUTO CLOSE 與資料庫鏡像)。  
  
 如果資料庫中已經有記憶體最佳化的檔案群組，這個欄位就會預先填入它的名稱，而且您無法變更此欄位的值。  
  
 邏輯檔案名稱和檔案路徑  
 將會包含記憶體最佳化資料表的檔案名稱。 資料庫必須具備一個記憶體最佳化的檔案群組 (其中至少包含一個檔案)，才能建立記憶體最佳化的資料表。  
  
 如果您不具備現有的記憶體最佳化檔案群組，則可在移轉程序結束時，變更要建立之檔案的預設名稱和路徑。  
  
 如果您具備現有的記憶體最佳化檔案群組，這些欄位會預先填入，而且您無法變更這些欄位的值。  
  
 將原始資料表重新命名為  
 在移轉程序結束時，會使用資料表目前的名稱建立新的記憶體最佳化資料表。 若要避免名稱衝突，您必須重新命名目前的資料表。 您可以在此欄位中變更名稱。  
  
 目前估計的記憶體成本 (MB)  
 記憶體最佳化 Advisor 會根據磁碟資料表的中繼資料，評估新的記憶體最佳化資料表將取用的記憶體數量。 [記憶體最佳化資料表中的資料表和資料列大小](table-and-row-size-in-memory-optimized-tables.md)中說明資料表大小的計算方式。  
  
 如果未分配足夠的記憶體，移轉程序可能會失敗。  
  
 請將資料表的資料複製到新的記憶體最佳化資料表  
 如果您想要將目前資料表的資料移至新的記憶體最佳化資料表，請選取此選項。 如果未選取此選項，建立新的記憶體最佳化資料表時不會有任何資料列。  
  
 根據預設將資料表移轉為持久性資料表  
 相較於持久性記憶體最佳化資料表，記憶體中 OLTP 可以優越效能支援非持久性資料表。 不過，在重新啟動伺服器時，非持久性資料表中的資料將會遺失。  
  
 如果選取此選項，記憶體最佳化 Advisor 將會建立非持久性的資料表 (而不是持久性資料表)。  
  
> [!WARNING]  
>  只有在您了解非持久性資料表的相關資料遺失風險時，才可選取此選項。  
  
 按 **[下一步]**，繼續進行。  
  
### <a name="review-primary-key-conversion"></a>檢閱主索引鍵轉換  
 下一個畫面是 **[檢閱主索引鍵轉換]**。 記憶體最佳化 Advisor 會偵測資料表中是否有一個或多個主索引鍵，並根據主索引鍵的中繼資料填入資料行的清單。 否則，如果您想要移轉至持久性記憶體最佳化資料表，就必須建立主索引鍵。  
  
 如果主索引鍵不存在，而且資料表正移轉至非持久性資料表，這個畫面將不會出現。  
  
 對於文字資料行 (`char`、`nchar`、`varchar` 和 `nvarchar` 類型的資料行)，您必須選取適當的定序。 記憶體中 OLTP 只支援記憶體最佳化資料表上的資料行之 BIN2 定序，而不支援附帶補充字元的定序。 如需支援的定序及定序變更之潛在影響的詳細資訊，請參閱＜ [Collations and Code Pages](../../database-engine/collations-and-code-pages.md) ＞。  
  
 您可以為主索引鍵設定下列參數：  
  
 為主要索引鍵選取新的名稱  
 此資料表的主索引鍵名稱在資料庫內必須是唯一的。 您可在此處變更主索引鍵的名稱。  
  
 選取主索引鍵的類型  
 記憶體中 OLTP 支援下列兩種記憶體最佳化資料表上的索引類型：  
  
-   非叢集雜湊索引。 此索引最適合具有許多點查閱的索引。 您可以在 **[值區計數]** 欄位中設定此索引的值區計數。  
  
-   非叢集索引。 此類型的索引最適合具有許多範圍查詢的索引。 您可以在 **[排序資料行和次序]** 清單中設定每個資料行的排序次序。  
  
 若要了解主索引鍵最適合的索引類型，請參閱 [雜湊索引](../../database-engine/hash-indexes.md)。  
  
 選定主索引鍵之後，請按 **[下一步]** 。  
  
### <a name="review-index-conversion"></a>檢閱索引轉換  
 下一頁是 **[檢閱索引轉換]**。 記憶體最佳化 Advisor 會偵測資料表中是否有一個或多個索引，並填入資料行與資料類型的清單。 您可在 **[檢閱索引轉換]** 頁面中設定的參數，與上一個 **[檢閱主索引鍵轉換]** 頁面類似。  
  
 如果資料表中僅有主索引鍵，而且資料表正移轉至持久性資料表，這個畫面就不會出現。  
  
 決定資料表中的每個索引之後，請按 **[下一步]**。  
  
### <a name="verify-migration-actions"></a>確認移轉動作  
 下一頁是 **[確認移轉動作]**。 若要編寫移轉作業的指令碼，請按一下 **[指令碼]** 產生 [!INCLUDE[tsql](../../includes/tsql-md.md)] 指令碼。 然後您可以修改和執行指令碼。 按一下 **[移轉]** 即可開始資料表移轉。  
  
 程序完成之後，請重新整理 **[物件總管]** 以查看新的記憶體最佳化資料表和舊的磁碟資料表。 您可保留舊資料表或隨時將其刪除。  
  
## <a name="see-also"></a>另請參閱  
 [移轉至 In-Memory OLTP](migrating-to-in-memory-oltp.md)  
  
  
