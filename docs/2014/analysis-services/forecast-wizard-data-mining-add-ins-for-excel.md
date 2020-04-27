---
title: 預測 Wizard （適用于 Excel 的資料採礦增益集） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- forecasting [data mining]
- time series [data mining]
ms.assetid: c5b33f75-42d4-4598-89e7-94815c142ce6
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f0717d8a81cc89897de005144dd631d23da42137
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "66081027"
---
# <a name="forecast-wizard-data-mining-add-ins-for-excel"></a>預測精靈 (適用於 Excel 的資料採礦增益集)
  ![資料採礦功能區中的關聯精靈](media/dmc-forecast.gif "資料採礦功能區中的關聯精靈")  
  
 預測精靈可協助您預測時間序列中的值。 預測精靈使用 [!INCLUDE[msCoName](../includes/msconame-md.md)] 時間序列演算法，這是用於預測連續資料行 (例如產品銷售) 的迴歸演算法。  
  
 每一個預測模型必須包含一個案例序列，它是用來區分序列中各個點的資料行。 例如，如果您使用記錄資料來預測數個月內的銷售量，您會使用包含一連串日期的資料行做為案例序列。  
  
 您可以從預測模型建立預測，而不需要提供新的輸入資料。  
  
 [**分析**] 功能區中的 [[適用于 Excel&#41;工具的預測 &#40;資料表分析工具](forecast-table-analysis-tools-for-excel.md)] 也可讓您建立預測模型，但它的自訂性較少，而且只能使用 Excel 資料表中的資料。  
  
## <a name="using-the-forecast-wizard"></a>使用預測精靈  
  
1.  在 [**資料採礦**] 功能區中，按一下 [**預測**]。  
  
2.  在 [**選取來源資料**] 中，選擇要當做輸入使用的 Excel 資料表、範圍或外部資料源。  
  
     如果使用外部資料來源，您可以定義自訂檢視或查詢，然後將其儲存為 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 資料來源。  
  
3.  在 [**預測**] 頁面上，針對 [**時間戳記**] 選取包含唯一數值（包括日期和時間值）的資料行，這些值可當做案例序列使用。 您必須依據此資料行，以遞增順序來排序資料來源。  
  
     如果您的資料沒有這類資料行，您可以使用 [沒有\<時間戳記>] 選項。 精靈會為輸入資料新增唯一的排序資料行，因此，您必須確定資料是以您想要的方式排序，再執行精靈並選擇此選項。  
  
4.  （選擇性）您可以按一下 [**參數**]，並自訂採礦模型的行為。  
  
     預測模型支援數種不同的演算法：  
  
    -   ARIMA  
  
    -   ARTXP (一種迴歸模型)  
  
    -   結合 ARTXP 和 ARIMA  
  
     如需差異的詳細資訊，請參閱[Microsoft 時間序列演算法技術參考](data-mining/microsoft-time-series-algorithm-technical-reference.md)。  
  
     您也可以新增週期性提示、指定平滑選項，以及自訂模型的迴歸選項。  
  
5.  在 [**完成]** 頁面上，為您的資料集和模型提供描述性的名稱，並設定下列選項來控制如何使用完成的模型：  
  
    -   **流覽模型**。 選取這個選項時，一旦 wizard 完成模型的處理，就會開啟 **[流覽**] 視窗以協助您流覽結果。 檢視器的內容取決於建立的模型類型。 如需詳細資訊，請參閱[流覽預測模型](browsing-a-forecasting-model.md)。  
  
    -   **啟用 [鑽取**]。 選取此選項可檢視完成模型中的基礎資料。 只有建立決策樹模型時，才能使用這個選項。  
  
    -   **使用暫時性模型**。 如果選取這個選項，此模型將無法儲存到伺服器。 當您關閉 Excel 時，即會刪除暫時性模型。  
  
### <a name="requirements"></a>需求  
 您的資料應該至少包含一個可做為時間序列的資料行。 此資料行中的值應該是唯一且連續的，也就是不應該有間距。 執行精靈之前，請依據時間序列資料行，以遞增順序來排序資料。  
  
 如果您的資料不包含時間或日期欄，您可以指派任意數值序列，或讓精靈建立一個資料行。 如果您讓精靈建立序列排序資料行，請確定其他資料行是以您想要的方式排序，再啟動精靈。  
  
## <a name="see-also"></a>另請參閱  
 [建立資料採礦模型](creating-a-data-mining-model.md)   
 [適用于 Excel&#41;的預測 &#40;資料表分析工具](forecast-table-analysis-tools-for-excel.md)   
 [瀏覽預測模型](browsing-a-forecasting-model.md)  
  
  
