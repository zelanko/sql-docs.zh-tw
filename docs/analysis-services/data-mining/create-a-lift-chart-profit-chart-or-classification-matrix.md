---
title: "建立增益圖、收益圖或分類矩陣 | Microsoft Docs"
ms.custom: ""
ms.date: "03/20/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "採礦精確度圖表 [Analysis Services], 採礦結構"
ms.assetid: aa3d052f-58a9-4417-8e7a-5e6feb562af0
caps.latest.revision: 20
author: "Minewiskan"
ms.author: "owend"
manager: "jhubbard"
caps.handback.revision: 20
---
# 建立增益圖、收益圖或分類矩陣
  您可以使用五個基本步驟，為 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料採礦模型建立精確度圖表：  
  
-   選取包含您要比較之採礦模型的採礦結構。  
  
-   選取要加入至圖表的採礦模型。  
  
-   指定要用來產生圖表的測試資料來源。  
  
-   選擇圖表類型。  
  
-   設定圖表選項。  
  
 這些基本步驟對於增益圖、收益圖表和分類矩陣而言都相同。 下列程序將概略說明為這些圖表類型設定基本圖表選項的步驟。 如需如何建立交叉驗證報表的資訊，請參閱[交叉驗證報表中的量值](../../analysis-services/data-mining/measures-in-the-cross-validation-report.md)。  
  
### 在精確度圖表設計師中開啟採礦結構  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中開啟資料採礦設計師。  
  
2.  在 [方案總管] 中，按兩下包含採礦模型的採礦結構。  
  
3.  按一下 **[採礦精確度圖表]** 索引標籤。  
  
### 選取要包含在圖表中的採礦模型  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中，於資料採礦設計師的 [採礦精確度圖表] 索引標籤上，按一下 [輸入選擇] 索引標籤。  
  
     清單會顯示目前結構中所有具有相同可預測屬性的模型。  
  
2.  針對您要包含在圖表中的每個模型選取 [顯示方塊]。  
  
3.  按一下 [可預測資料行名稱] 文字方塊，然後從清單選取可預測資料行的名稱。 您放入單一圖表中的所有模型都必須具有相同的可預測資料行。  
  
4.  如果您要比較兩個模型，而可預測資料行具有不同的值或不同的資料類型，請清除 [同步處理預測資料行和值] 方塊以強制進行比較。  
  
    > [!NOTE]  
    >  如果選取 [同步處理預測資料行和值] 方塊，Analysis Services 就會分析模型和測試資料的可預測資料行中的資料，並嘗試尋找最佳的相符項目。 因此，請不要清除此方塊，除非絕對有必要要強制比較資料行。  
  
5.  按一下 [預測值] 文字方塊，然後從清單選取值。 如果可預測資料行是連續的資料類型，您必須在文字方塊中輸入值。  
  
     如需詳細資訊，請參閱[選擇用於測試採礦模型的資料行](../../analysis-services/data-mining/choose-the-column-to-use-for-testing-a-mining-model.md)。  
  
### 選取測試資料  
  
1.  在 [採礦精確度圖表] 索引標籤的 [輸入選擇] 索引標籤上，指定要用來產生圖表的資料來源，方法是在 [選取要用於精確度圖表的資料集] 群組中選取其中一個選項。  
  
    -   如果您想要使用採礦結構測試案例和在模型建立期間可能套用的任何篩選的交集所定義的案例子集，請選取 [使用採礦模型測試案例] 選項。  
  
    -   選取 [使用採礦結構測試案例] 選項可以使用採礦結構鑑效組資料集中所定義的測試案例完整集合。  
  
    -   如果您想要使用外部資料的話，請選取 [指定不同的資料集] 選項。  資料集必須可以作為資料來源檢視。   按一下瀏覽 (**…**) 按鈕可選擇要用於精確度圖表的資料表。 如需詳細資訊，請參閱[選擇和對應模型測試資料](../../analysis-services/data-mining/choose-and-map-model-testing-data.md)。  
  
         如果您要使用外部資料集，可以選擇性地篩選輸入資料集。 如需詳細資訊，請參閱[將篩選套用至模型測試資料](../../analysis-services/data-mining/apply-filters-to-model-testing-data.md)。  
  
> [!NOTE]  
>  您無法在 [輸入選擇] 索引標籤上的模型測試案例或採礦結構測試案例上建立篩選。 若要在採礦模型上建立篩選，請修改模型的篩選屬性。 如需詳細資訊，請參閱[將篩選套用至採礦模型](../../analysis-services/data-mining/apply-a-filter-to-a-mining-model.md)。  
  
### 設定圖表設定並產生圖表  
  
1.  在 [採礦精確度圖表] 索引標籤中，針對要建立的圖表按一下索引標籤。  
  
2.  如果要建立**增益圖**，請按一下 [增益圖] 索引標籤。 圖表會根據您剛選取的模型、可預測屬性以及輸入資料自動產生。  
  
3.  如果要建立**分類矩陣**，請按一下 [分類矩陣] 索引標籤。 不需要進一步的設定；圖表會根據您選取的輸入資料和模型自動產生。  
  
4.  如果要建立**收益圖**，請先按一下 [增益圖] 索引標籤。 接著從 [圖表類型] 下拉式清單中，選取 [收益圖]。  
  
     在 [收益圖設定] 對話方塊中輸入下列設定。  
  
     **母體**  
     當您建立增益圖時，想要使用之資料集內的案例數。  
  
     此模型一定會依據遞減機率的順序來選擇案例；也就是說，如果您要評估潛在的客戶，並選擇只代表客戶資料庫中一半記錄的數目，此模型將會針對最適合模型的案例子集來測量精確度。  
  
     這是因為當您使用此模型來產生郵寄或建立促銷活動時，您將會使用與每一個案例有關聯的預測機率，只針對做出正面回應的機率最高的客戶。  
  
     **固定成本**  
     與商業問題相關聯的固定成本。  
  
     如果這是針對郵寄方案，則固定成本可能代表印表機安裝費用，其中涵蓋了準備促銷郵件的初始成本。  
  
     這項成本會套用到整個目標母體一次。  
  
     **單位成本**  
     除了固定成本外，與每一個客戶連絡的相關聯成本。 例如，您可能會輸入促銷郵件的郵資成本或是打電話的成本。  
  
     這個成本對於整個目標母體都必須是相同的。 每個值都會乘以目標的案例數。  
  
     **每個別營收**  
     與每一次成功銷售相關聯的營收金額。  
  
## 請參閱＜  
 [增益圖 &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/lift-chart-analysis-services-data-mining.md)   
 [分類矩陣 &#40;Analysis Services - 資料採礦&#41;](../../analysis-services/data-mining/classification-matrix-analysis-services-data-mining.md)  
  
  