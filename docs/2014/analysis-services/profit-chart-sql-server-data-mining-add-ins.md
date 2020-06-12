---
title: 收益圖（SQL Server 資料採礦增益集） |Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- accuracy chart
- profit chart
- mining models, charting
- mining models, testing
ms.assetid: 5c902543-4da9-4db3-99d5-4ce04c43d7ef
author: minewiskan
ms.author: owend
ms.openlocfilehash: 08da312fa1348266bbc33fafa6b1b3c6b07c64ad
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/09/2020
ms.locfileid: "84539770"
---
# <a name="profit-chart-sql-server-data-mining-add-ins"></a>收益圖 (SQL Server 資料採礦增益集)
  ![資料採礦用戶端中的收益圖按鈕](media/dmc-profitchart.gif "資料採礦用戶端中的收益圖按鈕")  
  
 在商務案例中，收益圖會顯示當公司使用某採礦模型來決定應連絡的客戶對象時，相關的估計收益增加量。 圖表的 Y 軸代表收益，而 X 軸則代表母體中公司所連絡的百分比。 一般收益圖會顯示收益增加直到某個點為止，過了這個點之後，收益就會隨著連絡的母體百分比增加而減少。  
  
## <a name="configuring-the-profit-chart"></a>設定收益圖  
 精確度圖表只評估正確或錯誤預測的機率，收益圖則會納入對預測採取行動在現實世界中的結果。 這是透過考量您在執行精靈時所指定之下列因數達成的：  
  
-   **人數**  
  
     資料集裡用來建立增益圖的案例數目。 例如，潛在客戶的數目。  
  
-   **固定成本**  
  
     與商業問題相關聯的固定成本。 如果是鎖定目標的郵寄方案，則成本不會隨變數而定，例如電話拜訪次數或郵寄的廣告信件數量。  
  
-   **個別成本**  
  
     除了固定成本外，與每一個客戶連絡的相關聯成本。 例如，廣告信件或電話費用。  
  
-   **每個人的收入**  
  
     與每一次成功銷售相關聯的營收金額。  
  
## <a name="using-the-profit-chart-wizard"></a>使用收益圖精靈  
 若要建立收益圖，您必須參考現有的資料採礦模型。 您可以按一下 [**管理模型**] 或 **[流覽]** 以查看所使用之演算法的詳細資料，以及在此模型中的資料行，以流覽模型來尋找符合您資料的模型。  
  
 如需詳細資訊，請參閱[在 Excel 中流覽模型 &#40;SQL Server 資料採礦增益集&#41;](browsing-models-in-excel-sql-server-data-mining-add-ins.md)和[管理模型 &#40;SQL Server 資料採礦增益集&#41;](manage-models-sql-server-data-mining-add-ins.md)。  
  
#### <a name="to-create-a-profit-chart"></a>建立收益圖  
  
1.  選取現有的模型。  
  
2.  指定要預測的資料行和目標值 (如果適用)。  
  
3.  選取來源資料，這是您將會傳遞通過模型以便建立預測的資料。 來源資料不應與用來建立模型的資料相同。  
  
4.  將新 (來源) 日期中的資料行對應到在資料採礦模型中使用的資料行。 如果資料行名稱相似，精靈便會自動加以對應。  
  
5.  輸入精靈需要的成本資訊：固定成本、單位成本、母體及預期營收。  
  
6.  （選擇性）您可以輸入一連串的成本（按一下 [流覽] **（...）** 按鈕）。 例如，郵寄成本可能會在寄送的項目數目增加時變得更便宜，所以您可以根據項目數目輸入不同成本，然後精靈會自動調整每個取樣大小的成本。  
  
7.  精靈隨即建立包含模型之成本-效益分析的圖表。  
  
### <a name="requirements"></a>規格需求  
 如果您要預測離散數值，必須選取要預測的精確目標值。  
  
## <a name="understanding-the-profit-chart"></a>了解收益圖  
 收益圖包含一條灰色垂直線，您可以按一下圖表中的位置來移動此線條。 [**挖掘圖例**] 會顯示分數、人口校正，以及與圖表上的灰階位置相關聯的預測機率。 如果您在圖表中使用灰線選取最大收益點，則可以使用預測機率值來判斷連絡客戶的機率臨界值。  
  
 例如，假設收益曲線的峰值是母體的 55%，而相關聯的預測機率是 20%，這表示您應該只連絡預測回應機率在 20% 以上的客戶，才能達到最大收益。  
  
## <a name="see-also"></a>另請參閱  
 [驗證模型及使用模型進行預測 &#40;適用于 Excel 的資料採礦增益集&#41;](validating-models-and-using-models-for-prediction-data-mining-add-ins-for-excel.md)  
  
  
