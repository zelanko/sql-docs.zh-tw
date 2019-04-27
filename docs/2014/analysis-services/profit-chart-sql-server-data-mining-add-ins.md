---
title: 收益圖 （SQL Server 資料採礦增益集） |Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- accuracy chart
- profit chart
- mining models, charting
- mining models, testing
ms.assetid: 5c902543-4da9-4db3-99d5-4ce04c43d7ef
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ddeafaafd816e226edff764c8e273cde6df4eaad
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62748452"
---
# <a name="profit-chart-sql-server-data-mining-add-ins"></a>收益圖 (SQL Server 資料採礦增益集)
  ![資料採礦功能區中的收益圖按鈕](media/dmc-profitchart.gif "資料採礦功能區中的 [收益圖] 按鈕")  
  
 在商務案例中，收益圖會顯示當公司使用某採礦模型來決定應連絡的客戶對象時，相關的估計收益增加量。 圖表的 Y 軸代表收益，而 X 軸則代表母體中公司所連絡的百分比。 一般收益圖會顯示收益增加直到某個點為止，過了這個點之後，收益就會隨著連絡的母體百分比增加而減少。  
  
## <a name="configuring-the-profit-chart"></a>設定收益圖  
 精確度圖表只評估正確或錯誤預測的機率，收益圖則會納入對預測採取行動在現實世界中的結果。 這是透過考量您在執行精靈時所指定之下列因數達成的：  
  
-   **母體**  
  
     資料集裡用來建立增益圖的案例數目。 例如，潛在客戶的數目。  
  
-   **固定成本**  
  
     與商業問題相關聯的固定成本。 如果是鎖定目標的郵寄方案，則成本不會隨變數而定，例如電話拜訪次數或郵寄的廣告信件數量。  
  
-   **單位成本**  
  
     除了固定成本外，與每一個客戶連絡的相關聯成本。 例如，廣告信件或電話費用。  
  
-   **每個別營收**  
  
     與每一次成功銷售相關聯的營收金額。  
  
## <a name="using-the-profit-chart-wizard"></a>使用收益圖精靈  
 若要建立收益圖，您必須參考現有的資料採礦模型。 您可以瀏覽模型來尋找符合您的資料，依序按一下模型**管理模型**或是**瀏覽**若要查看有關所使用之演算法的詳細資料和採礦模型中的資料行。  
  
 如需詳細資訊，請參閱 < [Excel 中的 瀏覽模型&#40;SQL Server 資料採礦增益集&#41;](browsing-models-in-excel-sql-server-data-mining-add-ins.md)並[管理模型&#40;SQL Server 資料採礦增益集&#41;](manage-models-sql-server-data-mining-add-ins.md)。  
  
#### <a name="to-create-a-profit-chart"></a>建立收益圖  
  
1.  選取現有的模型。  
  
2.  指定要預測的資料行和目標值 (如果適用)。  
  
3.  選取來源資料，這是您將會傳遞通過模型以便建立預測的資料。 來源資料不應與用來建立模型的資料相同。  
  
4.  將新 (來源) 日期中的資料行對應到在資料採礦模型中使用的資料行。 如果資料行名稱相似，精靈便會自動加以對應。  
  
5.  輸入精靈需要的成本資訊：固定成本、單位成本、母體及預期營收。  
  
6.  您可以選擇性地輸入分等級的成本序列 (按一下瀏覽 **（...）** 按鈕)。 例如，郵寄成本可能會在寄送的項目數目增加時變得更便宜，所以您可以根據項目數目輸入不同成本，然後精靈會自動調整每個取樣大小的成本。  
  
7.  精靈隨即建立包含模型之成本-效益分析的圖表。  
  
### <a name="requirements"></a>需求  
 如果您要預測離散數值，必須選取要預測的精確目標值。  
  
## <a name="understanding-the-profit-chart"></a>了解收益圖  
 收益圖包含一條灰色垂直線，您可以按一下圖表中的位置來移動此線條。 **採礦圖例**顯示分數、 母體擴展正確及預測機率的灰線在圖表上的位置與相關聯。 如果您在圖表中使用灰線選取最大收益點，則可以使用預測機率值來判斷連絡客戶的機率臨界值。  
  
 例如，假設收益曲線的峰值是母體的 55%，而相關聯的預測機率是 20%，這表示您應該只連絡預測回應機率在 20% 以上的客戶，才能達到最大收益。  
  
## <a name="see-also"></a>另請參閱  
 [驗證模型及使用模型進行預測&#40;資料採礦適用於 Excel 的增益集&#41;](validating-models-and-using-models-for-prediction-data-mining-add-ins-for-excel.md)  
  
  
