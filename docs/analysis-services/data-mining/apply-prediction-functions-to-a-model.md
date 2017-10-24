---
title: "套用至模型的預測函數 |Microsoft 文件"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Mining Model Prediction [Analysis Services], selecting mining models
ms.assetid: cf9a97e2-c249-441b-af12-c977c1a91c44
caps.latest.revision: 17
author: Minewiskan
ms.author: owend
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 0634ebe36d956f356d13384159eb1171d4fc2ea4
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="apply-prediction-functions-to-a-model"></a>將預測函數套用至模型
  若要在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料採礦中建立預測查詢，您必須先選取該查詢要作為基礎的採礦模型。 您可以選取存在於目前專案中的任何採礦模型。  
  
 在您選取模型之後，請將 [預測函數] 加入查詢中。 預測函數可用來取得預測，但您也可以加入傳回相關統計資料的預測函數，例如預測值的機率或用於產生預測的資訊。  
  
 預測函數可以傳回以下類型的值：  
  
-   可預測屬性的名稱以及預測的值。  
  
-   有關預測值之分佈和變異數的統計資料。  
  
-   指定之結果或是所有可能結果的機率。  
  
-   最高或最低分數或值。  
  
-   與指定之節點、物件或屬性相關聯的值。  
  
 可以使用的預測函數類型取決於您正在使用的模型類型。 比方說，套用至決策樹模型的預測函數可以傳回規則與節點描述；時間序列模型的預測函數可以傳回延隔和其他針對時間序列的資訊。  
  
 如需幾乎支援所有模型類型的預測函數清單，請參閱[一般預測函數 &#40;DMX)](../../dmx/general-prediction-functions-dmx.md)。  
  
 如需如何查詢特定採礦模型類型的範例，請參閱[資料採礦演算法 &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md) 中的演算法參考主題。  
  
### <a name="choose-a-mining-model-to-use-for-prediction"></a>選擇用來預測的採礦模型  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中，以滑鼠右鍵按一下模型，然後選取 [Build Prediction Query (建立預測查詢)]。  
  
     --或--  
  
     在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中，按一下 [採礦模型預測] 索引標籤，然後按一下 [採礦模型] 資料表中的 [選取模型]。  
  
2.  在 [選取採礦模型] 對話方塊中選取採礦模型，然後按一下 [確定]。  
  
     您可以在目前的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料庫中選擇任何模型。 若要使用不同資料庫中的模型建立查詢，您必須在該資料庫的內容中開啟新的查詢視窗，或是開啟包含該模型的方案檔。  
  
### <a name="add-prediction-functions-to-a-query"></a>將預測函數加入至查詢中  
  
1.  在 [Prediction Query Builder (預測查詢產生器)] 中，設定用於預測的輸入資料，其方法是在 [單一查詢輸入] 對話方塊中提供值，或是將模型對應到外部資料來源。  
  
     如需詳細資訊，請參閱[為預測查詢選擇和對應輸入資料](../../analysis-services/data-mining/choose-and-map-input-data-for-a-prediction-query.md)。  
  
    > [!WARNING]  
    >  您不需要提供輸入來產生預測。 當沒有輸入時，此演算法通常會傳回所有可能的輸入中最有可能的預測值。  
  
2.  按一下 [來源] 資料行，然後從清單中選擇值：  
  
    |||  
    |-|-|  
    |**\<模型名稱 >**|選取此選項，將採礦模型中的值包含在輸出中。 您只能加入可預測的資料行。<br /><br /> 當您加入模型中的資料行時，傳回的結果會是該資料行中的非相異值清單。<br /><br /> 您以這個選項加入的資料行會包含在產生之 DMX 陳述式的 SELECT 部分內。|  
    |**預測函數**|選取這個選項可瀏覽預測函數清單。<br /><br /> 您選取的值或函數會加入至產生之 DMX 陳述式的 SELECT 部分內。<br /><br /> 系統不會篩選預測函數清單，也不會由您選取的模型類型加以限制。 因此，如果您對於目前模型類型是否支援此函數有任何疑問，您只需要將此函數加入至清單中，並查看是否有錯誤發生。<br /><br /> 前有 $ 的清單項目 (例如 $AdjustedProbability) 代表巢狀資料表中的資料行，當您使用 **PredictHistogram**函數時，該資料表為輸出。 當您傳回單一資料行而非巢狀資料表時，可以使用這些當做捷徑。|  
    |**自訂運算式**|選取這個選項來輸入自訂運算式，然後為輸出指派別名。<br /><br /> 此自訂運算式會加入至產生之 DMX 預測查詢的 SELECT 部分中。<br /><br /> 如果您想要針對包含每一個資料列的輸出加入文字、呼叫 VB 函數或是呼叫自訂預存程序，這個選項會非常實用。<br /><br /> 如需從 DMX 使用 VBA 和 Excel 函數的資訊，請參閱 [MDX 和 DAX 中的 VBA 函數](../../mdx/vba-functions-in-mdx-and-dax.md)。|  
  
3.  在您加入每一個函數或運算式之後，切換到 DMX 檢視可查看此函數如何加入至 DMX 陳述式內。  
  
    > [!WARNING]  
    >  要等到您按一下 [結果] 之後，預測查詢產生器才會驗證 DMX。 通常您會發現，查詢產生器所產生的運算式並不是有效的 DMX。 通常原因是因為參考的資料行與可預測資料行無關，或是嘗試預測巢狀資料表中的資料行 (這需要子 SELECT 陳述式)。 此時，您可以切換到 DMX 檢視，並繼續編輯陳述式。  
  
### <a name="example-create-a-query-on-a-clustering-model"></a>範例：在群集模型上建立查詢  
  
1.  如果您沒有叢集模型可用來建立此範例查詢，請使用[資料採礦基本教學課程](http://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c)建立 [TM_Clustering] 模型。  
  
2.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中，以滑鼠右鍵按一下模型 [TM_Clustering]，然後選取 [Build Prediction Query (建立預測查詢)]。  
  
3.  從 [採礦模型] 功能表中選取 [單一查詢]。  
  
4.  在 [單一查詢輸入] 對話方塊中，將以下的值設定為輸入：  
  
    -   Gender = M  
  
    -   Commute Distance = 5-10 miles  
  
5.  在查詢方格中，針對 [來源] 選取 TM_Clustering 採礦模型，並加入 [Bike Buyer] 資料行。  
  
6.  針對 [來源] 選取 [預測函數]，並加入 **Cluster** 函數。  
  
7.  針對 [來源] 選取 [預測函數]、加入 **PredictSupport** 函數，然後將 [Bike Buyer] 模型資料行拖曳到 [準則/引數] 方塊中。 在 [別名] 資料行中輸入 **Support**。  
  
     從 [準則/引數] 方塊複製代表預測函數和資料行參考的運算式。  
  
8.  針對 [來源] 選取 [自訂運算式]、輸入別名，然後使用以下語法來參考 Excel CEILING 函數：  
  
    ```  
    Excel![CEILING](<arguments) as <return type>  
    ```  
  
     貼上資料行參考，當做函數的引數。  
  
     例如，下列運算式會傳回支援值的 CEILING：  
  
    ```  
    EXCEL!CEILING(PredictSupport([TM_Clustering].[Bike Buyer]),2)  
    ```  
  
     在 [別名] 資料行中輸入「CEILING」。  
  
9. 按一下 [切換到查詢文字檢視] 來檢閱產生的 DMX 陳述式，然後按一下 [切換到查詢結果檢視] 來查看預測查詢的資料行輸出。  
  
     下表會顯示預期的結果：  
  
    |Bike Buyer|$Cluster|SUPPORT|CEILING|  
    |----------------|--------------|-------------|-------------|  
    |0|叢集 8|954|953.948638926372|  
  
 如果您想要在陳述式中的其他地方加入其他子句，例如，如果您想要加入 WHERE 子句，您不能使用此方格來加入，而必須先切換到 DMX 檢視。  
  
## <a name="see-also"></a>請參閱＜  
 [資料採礦查詢](../../analysis-services/data-mining/data-mining-queries.md)  
  
  

