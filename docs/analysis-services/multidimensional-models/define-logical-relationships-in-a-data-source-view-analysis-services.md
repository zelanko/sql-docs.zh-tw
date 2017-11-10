---
title: "定義邏輯關聯性中的資料來源檢視 (Analysis Services) |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- adding relationships
- relationships [Analysis Services], data source views
- data source views [Analysis Services], relationships
ms.assetid: a20d6dae-e769-4131-8a59-7ef56f174220
caps.latest.revision: 37
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 08ca218747186a14224809c574a6dc524296cb1a
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="define-logical-relationships-in-a-data-source-view-analysis-services"></a>在資料來源檢視中定義邏輯關聯性 (Analysis Services)
  [資料來源檢視精靈] 和資料來源檢視設計工具會根據基礎資料庫關聯性，或是根據您所指定的名稱比對準則，自動定義加入到資料來源檢視 (DSV) 之資料表之間的關聯性。  
  
 在使用多個資料來源之資料的情況下，您可能需要在 DSV 中手動定義邏輯關聯性，以補充那些自動定義的關聯性。 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 需要關聯性來識別事實資料表和維度資料表、建構查詢以從基礎資料來源擷取資料和中繼資料，以及利用進階的商業智慧功能。  
  
 您可以在資料來源檢視設計師中定義以下類型的關聯性：  
  
-   相同資料來源中不同資料表之間的關聯性。  
  
-   資料表與本身的關聯性，如同父子關聯性一樣。  
  
-   不同資料來源的不同資料表之間的關聯性。  
  
> [!NOTE]  
>  DSV 中所定義的關聯性是邏輯關聯性，可能無法反映基礎資料來源中所定義的實際關聯性。 您可以在資料來源檢視設計師中，建立不存在於基礎資料來源的關聯性，也可以從基礎資料來源的現有外部索引鍵關聯性，移除資料來源檢視設計師所建立的關聯性。  
  
 關聯性具有方向性。 針對來源資料行中的每一個值，在目的地資料行中均有一個對應值。 在資料來源檢視圖表 (例如 [圖表] 窗格中所顯示的圖表) 中，兩個資料表間線條上的箭頭會指出關聯性的方向。  
  
 本主題包含下列各節：  
  
 [在資料表、具名查詢或檢視表之間加入關聯性](#bkmk_addRel)  
  
 [在圖表窗格中檢視或修改關聯性](#bkmk_diagrampane)  
  
 [在資料表窗格中檢視或修改關聯性](#bkmk_tablespane)  
  
##  <a name="bkmk_addRel"></a> 在資料表、具名查詢或檢視表之間加入關聯性  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，開啟含有您想在其中加入邏輯關聯性之資料來源檢視的專案，或連接到包含此資料來源檢視的資料庫。  
  
2.  在方案總管中，展開 [資料來源檢視] 資料夾，然後按兩下資料來源檢視在 [資料來源檢視設計工具] 中開啟檢視。  
  
3.  在 [資料表] 窗格中，以滑鼠右鍵按一下您要加入關聯性的資料表、具名查詢或檢視表，然後按一下 [新增關聯性]。  
  
    > [!NOTE]  
    >  若要尋找資料表、檢視表或具名查詢，您可以按一下 [資料來源檢視] 功能表，或是以滑鼠右鍵按一下 [資料表] 或 [圖表] 窗格的開放區域，即可使用 [尋找資料表] 選項。  
  
4.  在 [指定關聯性] 對話方塊中，執行下列動作：  
  
    1.  在 [來源 (外部索引鍵) 資料表] 清單中，選取適當的資料表、具名查詢或檢視表。  
  
    2.  在 [目的地 (主索引鍵) 資料表] 清單中，選取適當的資料表、具名查詢或檢視表。  
  
    3.  從 [來源資料行] 和 [目的地資料行] 清單中選取資料行，來建立兩個資料表之間的關聯性。  
  
         如果 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 藉由取樣基礎資料表、檢視表或具名查詢中的資料而偵測到您已經定義了錯誤方向的關聯性 (從主索引鍵到外部索引鍵，而不是從外部索引鍵到主索引鍵)，則會出現提示，要求您反轉此順序。 若要快速反轉此順序，請按一下 [反轉]。  
  
         如果 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 偵測到您已選取的資料行中已經有關聯性存在，將會出現提示。 您不能定義重複的關聯性。  
  
    4.  選擇性地在 [描述] 方塊中輸入關聯性的描述。  
  
##  <a name="bkmk_diagrampane"></a> 在圖表窗格中檢視或修改關聯性  
  
-   在 [資料來源檢視設計工具] 的 [圖表] 窗格中，以滑鼠右鍵按一下您要檢視的關聯性，然後按一下 [編輯關聯性] \(或直接按兩下關聯性箭頭)。  使用 [編輯關聯性] 對話方塊修改關聯性。  
  
##  <a name="bkmk_tablespane"></a> 在資料表窗格中檢視或修改關聯性  
  
1.  在 [資料來源檢視設計工具] 的 [資料表] 窗格中，尋找含有您想要檢視或修改之關聯性的資料表、檢視表或具名查詢，並加以展開。  
  
2.  展開 [關聯性] 資料夾。  會出現選定資料表、檢視表或具名查詢以及其他資料表、檢視表和具名查詢之間的關聯性，並列出關聯性資料行。  
  
3.  以滑鼠右鍵按一下您要修改的關聯性，然後按一下 [編輯關聯性]。  
  
## <a name="see-also"></a>另請參閱  
 [多維度模型中的資料來源檢視](../../analysis-services/multidimensional-models/data-source-views-in-multidimensional-models.md)  
  
  

