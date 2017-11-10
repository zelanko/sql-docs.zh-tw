---
title: "Reporting Services 行動報表中加入視覺效果 |Microsoft 文件"
ms.custom: 
ms.date: 09/26/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 3b220b74-9ecd-4084-93fb-545208d5d7a2
caps.latest.revision: 15
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 7a6554de812f8f85c9adbd7a3338ab744555e9a0
ms.contentlocale: zh-tw
ms.lasthandoff: 08/09/2017

---
# <a name="add-visualizations-to-reporting-services-mobile-reports"></a>Reporting Services 行動報表中加入視覺效果
圖表是資料視覺效果中不可或缺的一部分。 了解可在 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 行動報表中用來涵蓋各種案例的圖表。 

[!INCLUDE[SS_MobileReptPub_Short](../../includes/ss-mobilereptpub-long.md)] 有三種基本圖表類型︰時間、類別和總計。 這三種圖表類型都有對應的比較圖，可用於比較兩組不同的數列。  

## <a name="shared-chart-properties"></a>共用的圖表屬性

某些屬性適用於所有圖表，而其他屬性則僅適用於特定圖表。 以下是一些共用屬性。

### <a name="number-format"></a>數字格式
您可以在 [!INCLUDE[SS_MobileReptPub_Short](../../includes/ss-mobilereptpub-short.md)] 中，針對圖表中的數字指定各種格式；例如，一般、包含或不含小數位數的貨幣、包含或不含小數位數的百分比等等。 在圖表中，數字格式會套用至軸註解，以及資料點快顯。 您會在每個圖表 (而不是整個行動報表) 上個別設定數字格式。 

* 若要設定的數字格式，請選取**配置**索引標籤上，選取圖表的設計介面上，及在**視覺屬性**窗格選取**數字格式**。 
  
### <a name="legend"></a>圖例
* 顯示圖表的圖例，請選取**配置**索引標籤上，選取圖表的設計介面上，及在**視覺屬性**窗格組**顯示圖例**至**上**
  
### <a name="series"></a>數列
每個顯示在圖表上的個別度量或值，可以視為一個數列；多個數列可以 (也應該) 共用通用 X 軸與通用 Y 軸。 數列可透過選取一或多個資料表及欄位，在資料檢視的資料屬性面板中定義。 每個欄位會在圖表視覺效果上產生個別的資料點數列，並分別有自己的色彩。  

### <a name="change-aggregation"></a>變更彙總 
在圖表中，數值欄位的預設彙總為總和。 您可以將其變更為平均值、計數、最小值、最大值、第一個值或最後一個值。

* 選取**資料** 索引標籤，然後在**資料屬性**，選取**選項**數值欄位旁 > 選取不同的彙總。

### <a name="set-or-clear-filters"></a>設定或清除篩選

如果您加入導覽器以篩選行動報表，您可以決定要篩選哪些圖表。

1. 選取**資料** 索引標籤，然後在**資料屬性**，選取**選項**。

2. 在下**經過**，您會看到導覽器，您可以選取或清除。

深入了解如何 [加入導覽器以篩選行動報表](../../reporting-services/mobile-reports/add-navigators-to-reporting-services-mobile-reports.md)。
   
## <a name="time-charts"></a>時間圖表  
  
時間圖表是 [!INCLUDE[SS_MobileReptPub_Short](../../includes/ss-mobilereptpub-short.md)]中的最基本圖表。 圖表的時間 (和日期) 軸將會自動設定到資料表中第一個有效的日期/時間欄位。  

![行動報表的時間圖表](../../reporting-services/mobile-reports/media/mobile-report-time-chart.png)

1. 拖曳**時間圖表**從**配置**索引標籤加入設計介面，並調整其大小。

2. 預設是堆疊橫條圖。 您可以變更在**數列視覺效果**。

3. 如果圖表需要已經不在報表中的資料時，選取**資料** 索引標籤 >**將資料加入**至[從 Excel 或共用資料集取得資料](../../reporting-services/mobile-reports/data-for-reporting-services-mobile-reports.md)。

3. 在**資料屬性** 窗格中，**主要數列**是**SimulatedTable**。 選取方塊中的箭號 > 選取您的資料表。

5. 如果您設定**資料結構**至**依資料行**(上**配置** 索引標籤 >**視覺屬性**窗格)，在**資料屬性**窗格，您可以選取多個資料行的數值。

   如果您設定**資料結構**至**資料列所**、 在**資料屬性**窗格，您可以選取其中**數列名稱欄位**和一個資料行的數值。
   
深入了解如何 [依資料行或資料列群組資料](../../reporting-services/mobile-reports/group-data-by-columns-or-rows-in-a-mobile-report-reporting-services.md)。
  
## <a name="category-charts"></a>類別圖表  
  
不同於時間圖表，在類別圖表中，您可以對 X 軸上的日期/時間欄位以外的欄位進行群組。 這個群組中，呼叫*類別座標*，必須為字串、 數值、 欄位未使用。

![行動報表的類別圖表](../../reporting-services/mobile-reports/media/mobile-report-category-chart.png)   

1. 拖曳**類別圖表**從**配置**索引標籤的設計介面時，調整其大小，和[取得資料](../../reporting-services/mobile-reports/data-for-reporting-services-mobile-reports.md)，必要時。

2. 選取**資料** 索引標籤，然後在**資料屬性**窗格下的**類別目錄協調**、 選取資料表和欄位來群組上。 此欄位將會在產生圖表的 X 軸上。

3. 在下**主要數列**，選取要彙總每個類別目錄的資料表和數值欄位。 
  
## <a name="totals-charts"></a>總計圖表  

![行動報表的總計圖表](../../reporting-services/mobile-reports/media/mobile-report-totals-chart.png)
  
總計圖表可完成兩個不同的動作： 
* 它不會呈現多個數列，只會呈現所定義之主要數列的總和或總計。 
* 它提供依資料行或資料列群組資料的選項。 處理扁平化資料時，依資料行群組可能會很有用。 當您依資料行群組時，只能使用主要數列屬性，因為類別資料行是由主要數列屬性選取的欄位數目自動決定。  

深入了解如何 [依資料行或資料列群組資料](../../reporting-services/mobile-reports/group-data-by-columns-or-rows-in-a-mobile-report-reporting-services.md)。 
  
## <a name="comparison-charts"></a>比較圖  
  
時間、 類別和總計圖表也會提供為*比較圖表*。 在比較圖中，您不僅可以指定主要數列，還可以指定第二個比較數列。 主要和比較數列的顯示方式有三種。

![行動報表的比較時間圖表](../../reporting-services/mobile-reports/media/mobile-report-comparison-time-chart.png)

1. 拖曳其中一個**比較圖表**（時間、 類別或總計） 從**配置**索引標籤的設計介面時，調整其大小，和[取得資料](../../reporting-services/mobile-reports/data-for-reporting-services-mobile-reports.md)，必要時。

2. 在**視覺屬性**窗格，請在**數列視覺效果**，選取下列其中之一： 
   * 橫條圖與細橫條圖比較
   * 折線圖與橫條圖比較
   * 橫條圖與階梯圖區域比較 

在比較圖中，您可以選擇讓數列中的主要和比較值具有相同的圖表色彩。

* 在**視覺屬性** 窗格中，設定**比較數列上重複使用色彩**至**上**。

   如果設定為**上**、 色彩調色盤會重新啟動之間繪製主要與比較數列，因此相關聯的值，在主要與比較數列相同。 

   如果設定為**關閉**，色彩調色盤會防止兩組數列產生誤導色彩協調比較數列後繪製主要數列時，會繼續一般輪替。  
  
## <a name="pie-and-funnel-charts"></a>圓形圖和漏斗圖  
  
圓形圖和漏斗圖是最簡單的視覺效果。 您可以將資料依資料列或資料行結構化。 
* **行動報表中的** 圓形圖 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 可以是圓形、環形或總計在中心的環形。 圓形圖適用於顯示整體不同部分的相對大小。 太多扇形會使其難以閱讀。
* **漏斗圖** 通常可用來顯示程序中的各階段，例如銷售階段。

![行動報表的漏斗圖](../../reporting-services/mobile-reports/media/mobile-report-funnel-chart.png)

### <a name="structure-pie-and-funnel-chart-data-by-rows-or-by-columns"></a>將圓形圖和漏斗圖資料依資料列或資料行結構化
1. 拖曳**圓形圖**或**漏斗圖**從**配置**索引標籤的設計介面時，調整其大小，和[取得資料](../../reporting-services/mobile-reports/data-for-reporting-services-mobile-reports.md)，必要時。
2. 在 [視覺屬性] 窗格的 [資料結構] 下，選取：
   * **循資料行**
   * **循資料列**
3. 如果您選取 [循資料行]，請選取 [資料] 索引標籤，然後在 [資料屬性] 窗格的 [主要數列] 下，選取您要在圓形圖或漏斗圖中彙總的資料表及所有欄位。 欄位名稱會用於標示結果圖表的每個區域。

   如果您選取**資料列所**，選取**資料** 索引標籤，然後在**資料屬性**窗格下的**類別資料行**，選取資料表和資料行群組和標籤在圓形圖中的使用的值。 在 [主要數列] 資料行下，針對圖表中的值選取一個數值欄位。

深入了解如何 [依資料行或資料列群組資料](../../reporting-services/mobile-reports/group-data-by-columns-or-rows-in-a-mobile-report-reporting-services.md)。 

## <a name="treemaps"></a>樹狀圖  
  
樹狀圖顯示度量的方式，是將其值套用至矩形格線中磚的大小和色彩。 

![行動報表的群組樹狀圖](../../reporting-services/mobile-reports/media/mobile-report-group-treemap.png)

1. 拖曳**矩形式樹狀結構圖**從**配置**索引標籤的設計介面時，調整其大小，和[取得資料](../../reporting-services/mobile-reports/data-for-reporting-services-mobile-reports.md)，必要時。
2.  選取**資料** 索引標籤，然後在**資料屬性**窗格： 

     * 在下**大小代表**選取的圖格大小的數值欄位。
     * 在 [色彩表示方式] 下，針對磚的色彩選取一個數值欄位。 
     * [選擇性] **自訂中間值**：當視覺效果類型為 HeatMapWithCustomCenterValue 時，您只能使用 **自訂中間值** 。
     
         中間值會決定方塊的色彩。 計量越符合中間值，顏色就越接近綠色。 反之則接近紅色。
     
     * [選擇性] 若要在檢視器選取格線中的磚時顯示快顯，請在 [快顯標籤] 下選取一個或多個欄位。 樹狀圖快顯可以同時顯示文字和數值欄位。  

根據預設，樹狀圖是階層式，會先依類別，再依大小和色彩群組磚。
* 一樣是在**資料**索引標籤，下方**分組**選取資料表和欄位。

您可以關閉群組，只依大小和色彩來排列磚。 

* 選取 [配置] 索引標籤，然後將 [雙層樹狀圖] 設定為 [關閉]。   

## <a name="waterfall-charts"></a>瀑布圖

瀑布圖會在加減值時顯示累積總計。 它很適合用來了解初始值 (例如淨收入) 如何受到一系列正負值的影響。

直條將會以綠色來顯示值的增加，並以紅色來顯示值的減少，以便您可以輕鬆辨識正負數。 初始和最終值的直條通常會從零開始，而中間值則為浮動直條。 因為這樣的「外觀」，瀑布圖也稱為橋圖表。

### <a name="when-to-use-a-waterfall-chart"></a>使用瀑布圖的時機

瀑布圖適合用於以下情況：
* 當您需要顯示跨時間序列或不同類別之度量的變更，以稽核影響總值的主要變更。
* 透過顯示收入的各種來源及最終的總收益 (或虧損)，來繪製公司的年度收益。
* 說明公司在一年期間的初始和結束員工人數。
* 以視覺化顯示您於每個月所賺取和花費的金額，以及帳戶的累積餘額。 

### <a name="create-a-waterfall-chart"></a>建立瀑布圖

1. 拖曳**瀑布圖**從**配置**索引標籤的設計介面時，調整其大小，和[取得資料](../../reporting-services/mobile-reports/data-for-reporting-services-mobile-reports.md)，必要時。

    ![mobile-report-waterfall-chart-icon](../../reporting-services/mobile-reports/media/mobile-report-waterfall-chart-icon.png)
    
2.  選取**資料** 索引標籤，然後在**資料屬性**窗格中，選取您的資料類別 欄位**類別目錄協調**，和數值欄位的**主要數列**: 

    ![mobile-report-waterfall-data](../../reporting-services/mobile-reports/media/mobile-report-waterfall-data.png)
    
3. 選取**配置**索引標籤來查看預覽中的瀑布圖。

   ![mobile-report-waterfall-chart](../../reporting-services/mobile-reports/media/mobile-report-waterfall-chart.png)
   
   虧損的月份 (例如二月、六月及七月) 是以紅色顯示。 
   盈利的月份 (例如九月、十月及十一月) 是以綠色顯示。 

## <a name="see-also"></a>另請參閱 
* [Reporting Services 行動報表中的地圖](../../reporting-services/mobile-reports/maps-in-reporting-services-mobile-reports.md)
* [Reporting Services 行動報表中的導覽器](../../reporting-services/mobile-reports/add-navigators-to-reporting-services-mobile-reports.md)
* [Reporting Services 行動報表中的資料格](../../reporting-services/mobile-reports/add-data-grids-to-mobile-reports-reporting-services.md)
* [Reporting Services 行動報表中的量測計](../../reporting-services/mobile-reports/add-gauges-to-mobile-reports-reporting-services.md)
  


