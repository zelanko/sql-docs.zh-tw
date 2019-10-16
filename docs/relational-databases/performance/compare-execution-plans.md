---
title: 比較執行計畫 | Microsoft Docs
ms.custom: ''
ms.date: 11/21/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- comparing execution plans
- compare execution plans
- plan comparison
- execution plans [SQL Server], comparing
- Query Store, comparing plans
ms.assetid: 9e583a18-5f4a-4054-bfe1-4b2a76630db6
author: pmasl
ms.author: pelopes
manager: amitban
ms.openlocfilehash: fc0eb0e3e8cd6a095a6f30f44ee08c520db19e45
ms.sourcegitcommit: 43c3d8939f6f7b0ddc493d8e7a643eb7db634535
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/12/2019
ms.locfileid: "72289293"
---
# <a name="compare-execution-plans"></a>比較執行計畫
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
本主題說明如何使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 計畫比較功能，來比較實際圖形化執行計畫之間的相似處和差異。 從 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] v16 開始提供此功能。
  
> [!NOTE]
> 實際執行計畫是在執行 [!INCLUDE[tsql](../../includes/tsql-md.md)] 查詢或 Batch 後產生。 基於這個緣故，實際執行計劃包含執行階段資訊；例如，實際資料列數目、資源使用量計量和執行階段警告 (如果有的話)。 如需詳細資訊，請參閱[顯示實際執行計畫](../../relational-databases/performance/display-an-actual-execution-plan.md)。
  
比較計畫的功能是資料庫專業人員可能必須基於疑難排解因素而進行的動作：
-   尋找查詢或批次突然變慢的原因。
-   了解重新撰寫查詢的影響。
-   觀察已導入至結構描述設計的特定效能增強變更 (例如，新索引) 如何有效地變更執行計畫。  
 
[計畫比較]  功能表選項能夠對兩個不同的執行計畫進行並排比較，可更容易識別出相似之處與變更，基於上述所有因素來說明不同的行為。 此選項可在下列項目之間進行比較：
- 兩個先前儲存的執行計畫檔案 ( *.sqlplan* 延伸模組)。
- 一個使用中的執行計畫和一個先前儲存的查詢執行計畫。
- [查詢存放區](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)中兩個已選取的查詢計畫。

> [!TIP]
> 計畫比較使用任何 *.sqlplan* 檔案，甚至是來自舊版的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 此外，此選項會啟用離線比較，因此不需連線到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體。 

比較兩個執行計畫時，**基本上執行相同動作**的計畫區域都會以相同的色彩和模式來反白顯示。 按一下某個計畫中的彩色區域，將使另一個計畫位於該計畫中相符節點的中心。 您仍然可以比較執行計畫中不相符的運算子和節點，但在此情況下，您必須手動選取要比較的運算子。

> [!IMPORTANT]
> 只使用被視為要變更計畫圖形的節點來檢查相似之處。 因此，可能有一個節點不會在位於相同計畫子區段的兩個節點中間上色。 在此情況下缺乏色彩，表示在檢查區段是否相等時不會將節點納入考量。
  
## <a name="to-compare-execution-plans"></a>比較執行計畫
  
1.  使用 [檔案]  功能表並按一下 [開啟檔案]  來開啟先前儲存的查詢執行計畫檔案 (.sqlplan)，或將計畫檔案拖曳至 [!INCLUDE[ssManStudio](../../includes/ssManStudio-md.md)] 視窗。 或者，如果您只執行查詢並選擇顯示它的執行計畫，請移至結果窗格中的 [執行計畫]  索引標籤。 

2.  以滑鼠右鍵按一下執行計畫的空白區域，然後按一下 [比較執行程序表]  。 

    ![以滑鼠右鍵按一下 [比較執行程序表]](../../relational-databases/performance/media/plancomparisonmenuoption.png "以滑鼠右鍵按一下 [比較執行程序表]")   

3.  選擇您想要比較的第二個查詢計畫檔案。 第二個檔案將會開啟，讓您可以比較計畫。

4.  比較的計畫將會開啟新視窗，根據預設，一個在頂端，另一個則在底部。 預設選項將是比較計畫中第一次出現的常見運算子或節點，但會顯示計畫之間的差異。 所有反白顯示的運算子和節點均存在於這兩個比較計畫中。 在頂端或左方計畫中選取反白顯示的運算子，也會自動選取底部或右方計畫中對應的運算子。 選取任一個比較計畫中的根節點運算子 (下圖中的 SELECT 節點) 也會選取另一個比較計畫中相應的根節點運算子。

    ![兩個已儲存計畫檔案的計畫比較](../../relational-databases/performance/media/plancomparison-plans.png "兩個已儲存計畫檔案的計畫比較")  

     > [!TIP]
     > 您可以滑鼠右鍵按一下執行計畫的空白區域，然後選取 [切換分隔器方向]  ，來將執行計畫比較的顯示切換為並排顯示。

     > [!TIP]
     > 所有適用於執行計畫的縮放和導覽選項均可在計畫比較模式中運作。 如需更多詳細資料，請參閱[顯示實際執行計畫](../../relational-databases/performance/display-an-actual-execution-plan.md)。

5.  雙重屬性視窗也會在預設選項的範圍內，於右側開啟。 存在於這兩個比較運算子內但有差異的屬性，將會在前面加上「不等於」  符號 (&ne;)，以便更容易識別。

    ![雙重屬性視窗](../../relational-databases/performance/media/plancomparison-properties.png "雙重屬性視窗")  

6.  [執行程序表分析]  比較導覽視窗也會在底部開啟。 有三個索引標籤可供使用：

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

    1.  在 [陳述式選項]  索引標籤中，預設選項是 [反白顯示類似作業]  ，而比較計畫中相同的反白顯示運算子或節點會共用相同的色彩和線條圖樣。 按一下線條圖樣，在比較計畫中的類似區域之間導覽。 您也可以藉由選取 [反白顯示與類似區段不符的作業]  ，來選擇在計畫中反白顯示差異而非相似之處。 
    
       > [!NOTE]
       > 根據預設，在比較計畫以允許對具有不同名稱但共用相同結構描述的資料庫擷取的計畫進行比較時，會忽略資料庫名稱。 例如，從資料庫 *ProdDB* 和 *TestDB* 比較計畫時。 此行為可以利用 [在比較運算子時忽略資料庫名稱]  選項來變更。

       ![[執行程序表分析] 視窗](../../relational-databases/performance/media/plancomparison-analysis.png "[執行程序表分析] 視窗") 

    2.  使用多個陳述式比較計畫時，由於能夠比較成對的正確陳述式，[多重陳述式]  索引標籤非常實用。

        ![比較計畫中的多個陳述式](../../relational-databases/performance/media/plancomparison-multiple.png "比較計畫中的多個陳述式")  

    3.  在 [案例]  索引標籤中，您可以找到一些最相關層面的自動化分析，來查看比較計畫中與[基數估計](../../relational-databases/performance/cardinality-estimation-sql-server.md)差異相關的項目。 針對左窗格上每個列出的運算子，右窗格會在 [按一下這裡可取得此案例的詳細資訊]  連結中顯示有關案例的詳細資料，並列出可能原因來說明該案例。 

        ![不同的估計資料列](../../relational-databases/performance/media/plancomparison-scenarios.png "不同的估計資料列")  

    如果這個視窗已關閉，以滑鼠右鍵按一下比較計畫的空白區域，然後選取 [執行程序表比較選項]  以重新開啟。

    ![計畫比較選項](../../relational-databases/performance/media/plancomparison-options.png "計畫比較選項")  

## <a name="to-compare-execution-plans-in-query-store"></a>在查詢存放區中比較執行計畫

1.  在查詢存放區中，找出具有一個以上執行計畫的查詢。 如需查詢存放區案例的詳細資訊，請參閱[查詢存放區使用案例](../../relational-databases/performance/query-store-usage-scenarios.md#identify-and-tune-top-resource-consuming-queries)。

2.  同時使用 SHIFT 鍵和滑鼠，針對同一個查詢選取兩個計畫。 

    ![在查詢存放區中選取兩個計畫](../../relational-databases/performance/media/plancomparison-querystore.png "在查詢存放區中選取兩個計畫")   

3.  使用 [在另一個視窗中比較所選查詢的計畫]  按鈕，開始比較計畫。 接著適用「比較執行計畫」  的步驟 4 到 6。 

    ![比較查詢存放區中的執行程序表](../../relational-databases/performance/media/plancomparison-querystoreoption.png "比較查詢存放區中的執行程序表") 
