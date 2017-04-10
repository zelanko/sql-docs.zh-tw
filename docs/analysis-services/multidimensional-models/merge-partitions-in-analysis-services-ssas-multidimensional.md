---
title: "在 Analysis Services 中合併分割區 (SSAS - 多維度) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "分割區 [Analysis Services], 合併"
  - "合併分割區 [Analysis Services]"
ms.assetid: b3857b9b-de43-4911-989d-d14da0196f89
caps.latest.revision: 34
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 34
---
# 在 Analysis Services 中合併分割區 (SSAS - 多維度)
  您可以合併現有 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫中的資料分割，以合併相同量值群組中之多個資料分割的事實資料。  
  
 [常見的案例](#bkmk_Scenario)  
  
 [需求](#bkmk_prereq)  
  
 [合併分割區之後更新分割區來源](#bkmk_Where)  
  
 [依事實資料表或具名查詢分割分割區的特殊考量](#bkmk_fact)  
  
 [如何使用 SSMS 合併分割區](#bkmk_partitionSSMS)  
  
 [如何使用 XMLA 合併分割區](#bkmk_partitionsXMLA)  
  
##  <a name="bkmk_Scenario"></a> 常見的案例  
 針對分割區使用的單一最常見組態，牽涉到跨時間維度的資料分離。 視專案特定的商務需求而定，與每個分割區相關聯的時間資料粒度會有所不同。 例如，分割可能是依年份，並依月份分割最近的年份，再加上使用中之月份的個別分割區。 使用中月份分割區會定期顯示新資料。  
  
 當使用中的月份完成時，該分割區會合併回年初至今分割區中的月份，然後繼續進行。 在年份結束時，就會形成完整的新年度分割區。  
  
 如此案例所示，合併分割區可成為定期執行的例行工作，以提供漸進的方法來合併及組織歷程記錄資料。  
  
##  <a name="bkmk_prereq"></a> 需求  
 只能合併符合下列所有準則的分割區：  
  
-   它們有相同的量值群組。  
  
-   它們有相同的結構。  
  
-   它們必須處於已處理的狀態。  
  
-   它們有相同的儲存模式。  
  
-   它們包含相同的彙總設計。  
  
-   它們共用相同的字串存放相容性層級 (僅適用於已分割的相異計數量值群組)。  
  
 如果目標分割區是空的 (亦即具有彙總設計但沒有彙總)，合併會卸除來源分割區的彙總。 您必須對分割區執行處理索引、完整處理或處理預設，以建立彙總。  
  
 遠端資料分割只能與相同的遠端 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體所定義的其他遠端資料分割合併。  
  
> [!NOTE]  
>  如果使用本機和遠端分割區的組合，替代方式是建立包含合併資料的新分割區，並刪除您不再使用的分割區。  
  
 若要建立未來適合進行合併的分割區，當您在分割區精靈中建立分割區時，您可以選擇從 Cube 的另一個分割區來複製彙總設計。 這樣可以確保這些分割區具有相同的彙總設計。 進行合併時，來源分割區的彙總會與目標分割區中的彙總結合。  
  
##  <a name="bkmk_Where"></a> 合併分割區之後更新分割區來源  
 分割區會依查詢 (例如用於處理資料之 SQL 查詢的 WHERE 子句) 分割，或依資料表或具名查詢分割，以提供資料給分割區。 資料分割的 **Source** 屬性指出資料分割繫結至查詢或資料表。  
  
 當您合併資料分割時，會合併資料分割的內容，但不會更新 **Source** 屬性以反映資料分割的其他範圍。 這表示如果您後續重新處理保留其原始 **Source** 的資料分割，會從該資料分割取得不正確的資料。 分割區會錯誤地在父層級彙總資料。 下列範例說明此行為。  
  
 **問題**  
  
 假設您有包含關於 3 種飲料產品之資訊的 Cube。 其有 3 個使用相同事實資料表的分割區。 這些分割區已依產品分割。 資料分割 1 包含關於 [ColaFull] 的資料，資料分割 2 包含關於 [ColaDecaf] 的資料，資料分割 3 包含關於 [ColaDiet] 的資料。 如果資料分割 3 合併到資料分割 2，則所產生的資料分割 (資料分割 2) 中的資料是正確的，且 Cube 資料是精確的。 不過，在處理資料分割 2 時，其內容可能是由產品層級之成員的父成員來決定。 這個父成員 [SoftDrinks] 也包含資料分割 1 的產品 [ColaFull]。 處理資料分割 2 時會將所有飲料的資料載入資料分割，包括 [ColaFull] 在內。 於是 Cube 會包含 [ColaFull] 的重複資料，並傳回不正確資料給使用者。  
  
 **方案**  
  
 解決方法是更新 **Source** 屬性，您可以調整 WHERE 子句或具名查詢，或者手動合併基礎事實資料表中的資料，以在資料分割範圍擴充的情況下，確保後續處理正確。  
  
 在這個範例中，將資料分割 3 合併到資料分割 2 之後，您可以在所產生的資料分割 2 中提供篩選，例如 ("Product" = 'ColaDecaf' OR "Product" = 'ColaDiet')，來指定只從事實資料表擷取關於 [ColaDecaf] 和 [ColaDiet] 的資料，而屬於 [ColaFull] 的資料將被排除在外。 或者，您可以在建立資料分割 2 和資料分割 3 時指定篩選，這些篩選便會在合併過程中進行結合。 不論是哪一種情況，在處理分割區之後，Cube 都不會包含重複的資料。  
  
 **結論**  
  
 合併資料分割之後，請務必檢查 **Source** 以確認篩選對於合併的資料是正確的。 如果您的分割區一開始包含 Q1、Q2 和 Q3 的歷程記錄資料，且您現在想合併 Q4，則必須調整篩選以加入 Q4。 否則，分割區的後續處理將產生錯誤的結果。 此結果對於 Q4 而言將不正確。  
  
##  <a name="bkmk_fact"></a> 依事實資料表或具名查詢分割分割區的特殊考量  
 除了查詢之外，也可依資料表或具名查詢分割分割區。 如果來源資料分割和目標資料分割使用資料來源或資料來源檢視中的相同事實資料表，**Source** 屬性會在合併資料分割之後生效。 它會指定適合結果分割區的事實資料表資料。 由於事實資料表中已存在產生資料分割所需的事實，因此不需要修改 **Source** 屬性。  
  
 使用多個事實資料表或具名查詢中資料的分割區需要執行額外的工作。 您必須手動將來源分割區的事實資料表中的事實，合併到目標分割區的事實資料表。  
  
 或者，您可以將合併分割區的來源變更為具名查詢，傳回兩個不同事實資料表的內容。 如果未執行此手動步驟，則事實資料表不會包含完整資訊。  
  
 基於相同理由，從具名查詢取得分割資料的分割區也需要更新。 合併的分割區現在必須具有具名查詢，以傳回先前從個別具名查詢取得的合併結果集。  
  
## 分割區儲存考量：MOLAP  
 合併 MOLAP 分割區時，也會合併分割區的多維度結構中儲存的事實。 這會產生內部完整和一致的分割區。 不過，MOLAP 分割區中儲存的事實，只是事實資料表中之事實的副本。 後續處理分割區時，將會刪除多維度結構中的事實 (僅限完整和重新整理的情況)，並從分割區的資料來源和篩選所指定的事實資料表複製資料。 如果來源分割區使用的事實資料表不同於目標分割區，則必須手動合併來源和目標分割區的事實資料表，確保處理結果分割區時有完整的資料集可用。 如果兩個分割區以不同的具名查詢為基礎，情況亦同。  
  
> [!IMPORTANT]  
>  具有不完整事實資料表的合併 MOLAP 分割區包含一份內部合併的事實資料表資料副本，並且在處理之前會正確地運作。  
  
## 分割區儲存考量：HOLAP 和 ROLAP 分割區  
 合併具有不同的事實資料表的 HOLAP 或 ROLAP 分割區時，不會自動合併事實資料表。 除非手動合併事實資料表，否則結果分割區只能使用與目標分割區相關聯的事實資料表。 結果分割區中的向下鑽研無法使用與來源分割區相關聯的事實，而且在處理分割區時，彙總也不會從無法使用的資料表中摘要資料。  
  
> [!IMPORTANT]  
>  具有不完整事實資料表的合併 HOLAP 或 ROLAP 分割區，包含正確的彙總及不完整的事實。 參考遺漏事實的查詢會傳回錯誤資料。 處理分割區時，彙總只計算可用的事實。  
  
 無法使用的事實不存在很可能無法被發現，直到使用者嘗試向下鑽研到無法使用之事實資料表中的事實，或從無法使用的資料表中執行查詢而需要事實時才會被發現。 由於合併過程中會結合彙總，只根據彙總的查詢會傳回正確資料，但其他查詢則可能會傳回不正確的資料。 即使在處理結果分割區後，來自無法使用之事實資料表的遺漏資料可能仍未被發現，特別是如果它只代表結合之資料的一小部份時。  
  
 事實資料表可以在合併分割區之前或之後合併。 然而，只有在兩個作業都完成後，彙總才能正確地代表基礎事實。 當使用者未連接到包含這些分割區的 Cube 時，建議您合併存取不同事實資料表的 HOLAP 或 ROLAP 分割區。  
  
##  <a name="bkmk_partitionSSMS"></a> 如何使用 SSMS 合併分割區  
  
> [!IMPORTANT]  
>  合併分割區之前，請先複製資料篩選資訊 (通常是根據 SQL 查詢篩選的 WHERE 子句)。 在完成合併之後，您應該更新包含累積事實資料之分割區的 Partition Source 屬性。  
  
1.  在物件總管中，展開包含您要合併的資料分割之 Cube 的 [量值群組] 節點，然後展開 [資料分割]，再以滑鼠右鍵按一下合併作業的目標或目的地資料分割。 例如，如果您要將季度事實資料移至儲存年度事實資料的分割區，請選取包含年度事實資料的分割區。  
  
2.  按一下 [合併資料分割] 以開啟 [合併資料分割 \<資料分割名稱>] 對話方塊。  
  
3.  在 [來源資料分割] 下，選取要與目標資料分割合併之每個來源資料分割旁的核取方塊，然後按一下 [確定]。  
  
    > [!NOTE]  
    >  當來源合併到目標分割區之後，會立即刪除來源分割區。 完成合併之後，請重新整理 [分割區] 資料夾以更新其內容。  
  
4.  以滑鼠右鍵按一下包含累積資料的資料分割，然後選取 [屬性]。  
  
5.  開啟 **Source** 屬性並修改 WHERE 子句，使其包含剛才合併的資料分割資料。 請注意，系統不會自動更新 **Source** 屬性。 如果重新處理而未先更新 **Source**，則可能無法取得所有預期的資料。  
  
##  <a name="bkmk_partitionsXMLA"></a> 如何使用 XMLA 合併分割區  
 如需詳細資訊，請參閱此主題：[合併資料分割 &#40;XMLA&#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/merging-partitions-xmla.md)。  
  
## 請參閱＜  
 [處理 Analysis Services 物件](../../analysis-services/multidimensional-models/processing-analysis-services-objects.md)   
 [資料分割 &#40;Analysis Services - 多維度資料&#41;](../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-analysis-services-multidimensional-data.md)   
 [建立及管理本機資料分割 &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/create-and-manage-a-local-partition-analysis-services.md)   
 [建立及管理遠端資料分割 &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/create-and-manage-a-remote-partition-analysis-services.md)   
 [設定分割區回寫](../../analysis-services/multidimensional-models/set-partition-writeback.md)   
 [可寫入的資料分割](../Topic/Write-Enabled%20Partitions.md)   
 [設定維度及分割區的字串存放區](../../analysis-services/multidimensional-models/configure-string-storage-for-dimensions-and-partitions.md)  
  
  