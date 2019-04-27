---
title: 預測精靈 （資料採礦適用於 Excel 的增益集） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- forecasting [data mining]
- time series [data mining]
ms.assetid: c5b33f75-42d4-4598-89e7-94815c142ce6
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1ba2f28e4f2e66fd642273d06409eb128d219d8b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62731035"
---
# <a name="forecast-wizard-data-mining-add-ins-for-excel"></a>預測精靈 (適用於 Excel 的資料採礦增益集)
  ![資料採礦功能區中的關聯精靈](media/dmc-forecast.gif "資料採礦功能區中的關聯精靈")  
  
 預測精靈可協助您預測時間序列中的值。 預測精靈使用 [!INCLUDE[msCoName](../includes/msconame-md.md)] 時間序列演算法，這是用於預測連續資料行 (例如產品銷售) 的迴歸演算法。  
  
 每一個預測模型必須包含一個案例序列，它是用來區分序列中各個點的資料行。 例如，如果您使用記錄資料來預測數個月內的銷售量，您會使用包含一連串日期的資料行做為案例序列。  
  
 您可以從預測模型建立預測，而不需要提供新的輸入資料。  
  
 [預測&#40;適用於 Excel 的資料表分析工具&#41;](forecast-table-analysis-tools-for-excel.md)工具**分析**功能區，也可讓您建立預測模型，但其自訂功能較少，可以只使用 Excel 資料表中的資料。  
  
## <a name="using-the-forecast-wizard"></a>使用預測精靈  
  
1.  在 **資料採礦**功能區中，按一下**預測**。  
  
2.  在 **選取來源資料**，選擇 Excel 資料表、 範圍或外部資料來源當做輸入使用。  
  
     如果使用外部資料來源，您可以定義自訂檢視或查詢，然後將其儲存為 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 資料來源。  
  
3.  在上**Forecasting**頁面上，如**時間戳記**，選取包含唯一數值 （這包括日期和時間值），可用來當做案例序列的資料行。 您必須依據此資料行，以遞增順序來排序資料來源。  
  
     如果您的資料並沒有這類資料行，您可以使用此選項\<沒有時間戳記 >。 精靈會為輸入資料新增唯一的排序資料行，因此，您必須確定資料是以您想要的方式排序，再執行精靈並選擇此選項。  
  
4.  或者，您可以按一下**參數**並自訂採礦模型的行為。  
  
     預測模型支援數種不同的演算法：  
  
    -   ARIMA  
  
    -   ARTXP (一種迴歸模型)  
  
    -   結合 ARTXP 和 ARIMA  
  
     如需差異的資訊，請參閱 < [Microsoft 時間序列演算法技術參考](data-mining/microsoft-time-series-algorithm-technical-reference.md)。  
  
     您也可以新增週期性提示、指定平滑選項，以及自訂模型的迴歸選項。  
  
5.  在 **完成**頁面上，提供您的資料集和模型的描述性名稱，然後設定下列選項可控制如何使用完成的模型：  
  
    -   **瀏覽模型**。 選取此選項時，只要精靈完成處理模型，它會開啟**瀏覽**幫助您探索結果 視窗。 檢視器的內容取決於建立的模型類型。 如需詳細資訊，請參閱 <<c0> [ 瀏覽預測模型](browsing-a-forecasting-model.md)。  
  
    -   **啟用鑽研**。 選取此選項可檢視完成模型中的基礎資料。 只有建立決策樹模型時，才能使用這個選項。  
  
    -   **使用暫時性模型**。 如果選取這個選項，此模型將無法儲存到伺服器。 當您關閉 Excel 時，即會刪除暫時性模型。  
  
### <a name="requirements"></a>需求  
 您的資料應該至少包含一個可做為時間序列的資料行。 此資料行的值應該是唯一且連續-也就是應該沒有間距。 執行精靈之前，請依據時間序列資料行，以遞增順序來排序資料。  
  
 如果您的資料不包含時間或日期欄，您可以指派任意數值序列，或讓精靈建立一個資料行。 如果您讓精靈建立序列排序資料行，請確定其他資料行是以您想要的方式排序，再啟動精靈。  
  
## <a name="see-also"></a>另請參閱  
 [建立資料採礦模型](creating-a-data-mining-model.md)   
 [預測&#40;適用於 Excel 的資料表分析工具&#41;](forecast-table-analysis-tools-for-excel.md)   
 [瀏覽預測模型](browsing-a-forecasting-model.md)  
  
  
