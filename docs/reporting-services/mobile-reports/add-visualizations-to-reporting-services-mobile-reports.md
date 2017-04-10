---
title: "Add visualizations to Reporting Services mobile reports | Microsoft Docs"
ms.custom: ""
ms.date: "09/26/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 3b220b74-9ecd-4084-93fb-545208d5d7a2
caps.latest.revision: 15
author: "maggiesMSFT"
ms.author: "maggies"
manager: "erikre"
caps.handback.revision: 15
---
# Add visualizations to Reporting Services mobile reports
圖表是資料視覺效果中不可或缺的一部分。 了解可在 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 行動報表中用來涵蓋各種案例的圖表。 

[!INCLUDE[SS_MobileReptPub_Short](../../includes/ss-mobilereptpub-long.md)] 有三種基本圖表類型︰時間、類別和總計。 這三種圖表類型都有對應的比較圖，可用於比較兩組不同的數列。  

## 共用的圖表屬性

某些屬性適用於所有圖表，而其他屬性則僅適用於特定圖表。 以下是一些共用屬性。

### 數字格式
您可以在 [!INCLUDE[SS_MobileReptPub_Short](../../includes/ss-mobilereptpub-short.md)] 中，針對圖表中的數字指定各種格式；例如，一般、包含或不含小數位數的貨幣、包含或不含小數位數的百分比等等。 在圖表中，數字格式會套用至軸註解，以及資料點快顯。 您會在每個圖表 (而不是整個行動報表) 上個別設定數字格式。 

* 若要設定數字格式，請依序選取 [配置] 索引標籤和設計介面上的圖表，然後在 [視覺屬性] 窗格中，選取 [數字格式]。 
  
### 圖例
* 若要顯示圖表的圖例，請依序選取 [配置] 索引標籤和設計介面上的圖表，然後在 [視覺屬性] 窗格中，將 [顯示圖例] 設定為 [開啟]
  
### 數列
每個顯示在圖表上的個別度量或值，可以視為一個數列；多個數列可以 (也應該) 共用通用 X 軸與通用 Y 軸。 數列可透過選取一或多個資料表及欄位，在資料檢視的資料屬性面板中定義。 每個欄位會在圖表視覺效果上產生個別的資料點數列，並分別有自己的色彩。  

### 變更彙總 
在圖表中，數值欄位的預設彙總為總和。 您可以將其變更為平均值、計數、最小值、最大值、第一個值或最後一個值。

* 選取 [資料] 索引標籤，然後在 [資料屬性] 中，選取數值欄位旁的 [選項] > 再選取其他彙總。

### 設定或清除篩選

如果您加入導覽器以篩選行動報表，您可以決定要篩選哪些圖表。

1. 選取 [資料] 索引標籤，然後在 [資料屬性] 中，選取 [選項]。

2. 在 [篩選依據] 下，您會看到可選取或清除的導覽器。

深入了解如何[加入導覽器以篩選行動報表](../../reporting-services/mobile-reports/add-navigators-to-reporting-services-mobile-reports.md)。
   
## 時間圖表  
  
時間圖表是 [!INCLUDE[SS_MobileReptPub_Short](../../includes/ss-mobilereptpub-short.md)] 中的最基本圖表。 圖表的時間 (和日期) 軸將會自動設定到資料表中第一個有效的日期/時間欄位。  

![行動報表的時間圖表](../../reporting-services/mobile-reports/media/mobile-report-time-chart.png)

1. 將 [時間圖表] 從 [配置] 索引標籤拖曳至設計介面，然後調整其大小。

2. 預設是堆疊橫條圖。 您可以在 [數列視覺效果] 中進行變更。

3. 如果圖表需要的資料已不在報表中，請選取 [資料] 索引標籤 > [加入資料]，[從 Excel 或共用資料集取得資料](../../reporting-services/mobile-reports/data-for-reporting-services-mobile-reports.md)。

3. 在 [資料屬性] 窗格中，[主要數列] 是 [SimulatedTable]。 選取方塊中的箭號 > 選取您的資料表。

5. 如果您將 [資料結構] 設定為 [循資料行] (在 [配置] 索引標籤 > [視覺屬性] 窗格上)，則可以在這裡的 [資料屬性] 窗格中，選取多個數值資料行。

   如果您將 [資料結構] 設定為 [循資料列]，則可以在這裡的 [資料屬性] 窗格中，選取一個 [數列名稱欄位] 及一個數值資料行。
   
深入了解如何[依資料行或資料列群組資料](../../reporting-services/mobile-reports/group-data-by-columns-or-rows-in-a-mobile-report-reporting-services.md)。
  
## 類別圖表  
  
不同於時間圖表，在類別圖表中，您可以對 X 軸上的日期/時間欄位以外的欄位進行群組。 此群組 (稱為「類別座標」) 必須針對字串欄位，而不是數值欄位。

![行動報表的類別圖表](../../reporting-services/mobile-reports/media/mobile-report-category-chart.png)   

1. 將 [類別圖表] 從 [配置] 索引標籤拖曳至設計介面，調整其大小，然後視需要[取得其資料](../../reporting-services/mobile-reports/data-for-reporting-services-mobile-reports.md)。

2. 選取 [資料] 索引標籤，然後在 [資料屬性] 窗格的 [類別座標] 下，選取要群組的資料表和欄位。 此欄位將會在產生圖表的 X 軸上。

3. 在 [主要數列] 下，選取要針對每個類別彙總的資料表和數值欄位。 
  
## 總計圖表  

![行動報表的總計圖表](../../reporting-services/mobile-reports/media/mobile-report-totals-chart.png)
  
總計圖表可完成兩個不同的動作： 
* 它不會呈現多個數列，只會呈現所定義之主要數列的總和或總計。 
* 它提供依資料行或資料列群組資料的選項。 處理扁平化資料時，依資料行群組可能會很有用。 當您依資料行群組時，只能使用主要數列屬性，因為類別資料行是由主要數列屬性選取的欄位數目自動決定。  

深入了解如何[依資料行或資料列群組資料](../../reporting-services/mobile-reports/group-data-by-columns-or-rows-in-a-mobile-report-reporting-services.md)。 
  
## 比較圖  
  
時間、類別和總計圖表也可當做「比較圖」使用。 在比較圖中，您不僅可以指定主要數列，還可以指定第二個比較數列。 主要和比較數列的顯示方式有三種。

![行動報表的比較時間圖表](../../reporting-services/mobile-reports/media/mobile-report-comparison-time-chart.png)

1. 將其中一個 [比較圖] (時間、類別或總計) 從 [配置] 索引標籤拖曳至設計介面，調整其大小，然後視需要[取得其資料](../../reporting-services/mobile-reports/data-for-reporting-services-mobile-reports.md)。

2. 在 [視覺屬性] 窗格的 [數列視覺效果] 中，選取下列其中之一： 
   * 橫條圖與細橫條圖比較
   * 折線圖與橫條圖比較
   * 橫條圖與階梯圖區域比較 

在比較圖中，您可以選擇讓數列中的主要和比較值具有相同的圖表色彩。

* 在 [視覺屬性] 窗格中，將 [在比較數列上重複使用色彩] 設定為 [開啟]。

   如果設定為 [開啟]，調色盤在繪製主要和比較數列之間會重新啟動，以確保主要和比較數列的相關值相同。 

   如果設定為 [關閉]，調色盤在比較數列後繪製主要數列時，會繼續一般輪替，以防止這兩組數列產生誤導色彩協調。  
  
## 圓形圖和漏斗圖  
  
圓形圖和漏斗圖是最簡單的視覺效果。 您可以將資料依資料列或資料行結構化。 
* [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 行動報表中的**圓形圖**可以是圓形、環形或總計在中心的環形。 圓形圖適用於顯示整體不同部分的相對大小。 太多扇形會使其難以閱讀。
* **漏斗圖**通常可用來顯示程序中的各階段，例如銷售階段。

![行動報表的漏斗圖](../../reporting-services/mobile-reports/media/mobile-report-funnel-chart.png)

### 將圓形圖和漏斗圖資料依資料列或資料行結構化
1. 將 [圓形圖] 或 [漏斗圖] 從 [配置] 索引標籤拖曳至設計介面，調整其大小，然後視需要[取得其資料](../../reporting-services/mobile-reports/data-for-reporting-services-mobile-reports.md)。
2. 在 [視覺屬性] 窗格的 [資料結構] 下，選取：
   * **循資料行**
   * **循資料列**
3. 如果您選取 [循資料行]，請選取 [資料] 索引標籤，然後在 [資料屬性] 窗格的 [主要數列] 下，選取您要在圓形圖或漏斗圖中彙總的資料表及所有欄位。 欄位名稱會用於標示結果圖表的每個區域。

   如果您選取 [循資料列]，請選取 [資料] 索引標籤，然後在 [資料屬性] 窗格的 [類別資料行] 下，選取其值要用於群組及作為圓形圖中標籤的資料表和資料行。 在 [主要數列] 資料行下，針對圖表中的值選取一個數值欄位。

深入了解如何[依資料行或資料列群組資料](../../reporting-services/mobile-reports/group-data-by-columns-or-rows-in-a-mobile-report-reporting-services.md)。 

## 樹狀圖  
  
樹狀圖顯示度量的方式，是將其值套用至矩形格線中磚的大小和色彩。 

![行動報表的群組樹狀圖](../../reporting-services/mobile-reports/media/mobile-report-group-treemap.png)

1. 將 [樹狀圖] 從 [配置] 索引標籤拖曳至設計介面，調整其大小，然後視需要[取得其資料](../../reporting-services/mobile-reports/data-for-reporting-services-mobile-reports.md)。
2.  選取 [資料] 索引標籤，然後在 [資料屬性] 窗格中： 

     * 在 [數值表示方式] 下，針對磚的大小選取一個數值欄位。
     * 在 [色彩表示方式] 下，針對磚的色彩選取一個數值欄位。 
     * [選擇性] **自訂中間值**：當視覺效果類型為 HeatMapWithCustomCenterValue 時，您只能使用**自訂中間值**。
     
         中間值會決定方塊的色彩。 計量越符合中間值，顏色就越接近綠色。 反之則接近紅色。
     
     * [選擇性] 若要在檢視器選取格線中的磚時顯示快顯，請在 [快顯標籤] 下選取一個或多個欄位。 樹狀圖快顯可以同時顯示文字和數值欄位。  

根據預設，樹狀圖是階層式，會先依類別，再依大小和色彩群組磚。
* 同樣在 [資料] 索引標籤的 [群組依據] 下，選取一個資料表和欄位。

您可以關閉群組，只依大小和色彩來排列磚。 

* 選取 [配置] 索引標籤，然後將 [雙層樹狀圖] 設定為 [關閉]。   

## 瀑布圖

瀑布圖會在加減值時顯示累積總計。 它很適合用來了解初始值 (例如淨收入) 如何受到一系列正負值的影響。

直條將會以綠色來顯示值的增加，並以紅色來顯示值的減少，以便您可以輕鬆辨識正負數。 初始和最終值的直條通常會從零開始，而中間值則為浮動直條。 因為這樣的「外觀」，瀑布圖也稱為橋圖表。

### 使用瀑布圖的時機

瀑布圖適合用於以下情況：
* 當您需要顯示跨時間序列或不同類別之度量的變更，以稽核影響總值的主要變更。
* 透過顯示收入的各種來源及最終的總收益 (或虧損)，來繪製公司的年度收益。
* 說明公司在一年期間的初始和結束員工人數。
* 以視覺化顯示您於每個月所賺取和花費的金額，以及帳戶的累積餘額。 

### 建立瀑布圖

1. 將 [瀑布圖] 從 [配置] 索引標籤拖曳至設計介面，調整其大小，然後視需要[取得其資料](../../reporting-services/mobile-reports/data-for-reporting-services-mobile-reports.md)。

    ![mobile-report-waterfall-chart-icon](../../reporting-services/mobile-reports/media/mobile-report-waterfall-chart-icon.png)
    
2.  選取 [資料] 索引標籤，然後在 [資料屬性] 窗格中，針對 [類別座標] 選取您資料中的類別欄位，並針對 [主要數列] 選取數值欄位： 

    ![mobile-report-waterfall-data](../../reporting-services/mobile-reports/media/mobile-report-waterfall-data.png)
    
3. 選取 [配置] 索引標籤以查看瀑布圖的預覽。

   ![mobile-report-waterfall-chart](../../reporting-services/mobile-reports/media/mobile-report-waterfall-chart.png)
   
   虧損的月份 (例如二月、六月及七月) 是以紅色顯示。 
   盈利的月份 (例如九月、十月及十一月) 是以綠色顯示。 

## 另請參閱 
* [Reporting Services 行動報表中的地圖](../../reporting-services/mobile-reports/maps-in-reporting-services-mobile-reports.md)
* [Reporting Services 行動報表中的導覽器](../../reporting-services/mobile-reports/add-navigators-to-reporting-services-mobile-reports.md)
* [Reporting Services 行動報表中的資料格](../../reporting-services/mobile-reports/add-data-grids-to-mobile-reports-reporting-services.md)
* [Reporting Services 行動報表中的量測計](../../reporting-services/mobile-reports/add-gauges-to-mobile-reports-reporting-services.md)
  
