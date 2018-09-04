---
title: 在行動報表中新增量測計 | Reporting Services | Microsoft Docs
ms.date: 03/30/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: mobile-reports
ms.suite: pro-bi
ms.topic: conceptual
ms.assetid: 76d8fc8f-c37f-44d3-ab44-45fbeed4e064
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 6f5a9bab3624ebe4c294a29279cb1906f307d8db
ms.sourcegitcommit: d96b94c60d88340224371926f283200496a5ca64
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/30/2018
ms.locfileid: "43275875"
---
# <a name="add-gauges-to-mobile-reports--reporting-services"></a>在行動報表中加入量測計 | Reporting Services
量測計是行動報表中使用最廣泛的基本視覺效果。 它們顯示資料集中的單一值，只有值或和目標比較的值。

![PBI_SSMRP_Gauges](../../reporting-services/mobile-reports/media/pbi-ssmrp-gauges.png)  
  
*[配置] 索引標籤中的量測計視覺效果*  
  
在 SQL Server 行動報表發行工具 中，所有量測計至少都有一個共通屬性︰主要值，在行動報表其中一份資料表中設為數值的欄位。  

除數字量測計外，所有量測計也都可以顯示比較值或稱「差異」值，即主要值和比較值之間的關聯性。 比較值通常是目標，而量測計則是此目標的進度視覺指標，或實際和目標之間的差異。

量測計只能表示其主要值的一個彙總值，以及其比較值的一個彙總值。 量測計彙總是標準：加總、平均、最小值、最大值等等。 量測計值預設為加總，顯示包含在目前篩選出可供量測計控制項使用之資料的所有值總計。 

您可以將量測計連接至行動報表上的導覽器，藉以篩選量測計值。 

## <a name="set-the-main-and-comparison-values-for-a-gauge"></a>設定量測計的主要值和比較值

1. 將量測計從 [配置] 索引標籤拖曳至設計方格，調整為您想要的大小。

2. 取得 [Excel 或共用資料集的資料](../../reporting-services/mobile-reports/data-for-reporting-services-mobile-reports.md)。

3. 選取 [資料] 索引標籤，然後在 [資料屬性] 窗格的 [主要值] 下，選取資料表和數值欄位。

3. 在數字量測計以外的任一量測計中，在 [資料屬性] 窗格的 [比較值] 下，選取資料表和數值欄位。

4. [選用] 若要變更彙總，請選取 [選項]，然後選取不同的彙總。
   
   >**注意**︰當您變更主要值的彙總時，您可能也想要變更比較值的彙總，雖然在某些情況下您可能想要混用彙總方法。  

## <a name="filter-a-gauge"></a>篩選量測計
  
如果行動報表有任何導覽器，您可以將量測計繫結至一或多個導覽器以進行篩選。 您可以將量測計值和比較值繫結到一或多個不同的導覽器，創造幾乎無止境的量測計選項。  

1. 選取一個量測計，然後在 [資料屬性] 窗格的 [資料] 索引標籤中，選取 [主要值] 或 [比較值] 旁邊的 [選項]。

2. 在 [Filtered by (篩選條件)] 下選取您想要篩選量測計的導覽器。

   ![mobile-report-gauge-navigator](../../reporting-services/mobile-reports/media/mobile-report-gauge-navigator.png)
 
## <a name="set-visual-properties-for-a-gauge"></a>設定量測計的視覺屬性
  
您也可以自訂多項功能和視覺屬性，以及連接量測計元素和資料欄位的資料屬性。 

### <a name="set-value-direction-high-or-low-is-better"></a>設定值方向︰高好或低好。
* 選取量測計，然後在 [視覺屬性] 窗格的 [配置] 索引標籤中，將 [值方向] 設為 [數值愈高愈好] 或 [數值愈低愈好]。 

[數值愈高愈好] 以綠色顯示正值 (表示希望較佳的變更) 或紅色的較低值 (表示不希望較差的變更)。 

[數值愈低愈好] 的色彩則相反。

值方向屬性只和支援比較值的 Gauge 元素有關聯。 差異整數正負號和值方向屬性設定決定量測計色彩。  
  
### <a name="set-range-stops-for-a-gauge"></a>設定量測計停止的範圍
第二個量測計專屬的非資料屬性是範圍停駐點。 

* 選取量測計，然後在 [視覺屬性] 窗格的 [配置] 索引標籤中，選取 [範圍停止]。

使用 [範圍停止]，您設定比較值視覺效果應該呈現為正中目標值 (綠色)、中性 (琥珀色) 或偏離目標值 (紅色) 的百分比，以量測計的比較值作為目標。 再次提醒您，只有比較值量測計支援範圍停止。  

### <a name="format-the-numbers-in-the-gauge"></a>格式化量測計中的數字  
另一項由許多其他元素共用的量測計非資料屬性是數字格式。 

* 選取量測計，然後在 [視覺屬性] 窗格的 [配置] 索引標籤中，選取 [範圍停止]。

它會決定量測計顯示數字的格式化方式，例如，貨幣、百分比、時間或一般。 您可以設定行動報表每個元素的數字格式。
  
### <a name="see-also"></a>另請參閱 

* [使用 SQL Server 行動報表發行工具建立行動報表](../../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md)
* [Reporting Services 行動報表中的地圖](../../reporting-services/mobile-reports/maps-in-reporting-services-mobile-reports.md)
* [Reporting Services 行動報表中的導覽器](../../reporting-services/mobile-reports/add-navigators-to-reporting-services-mobile-reports.md)
* [Reporting Services 行動報表中的視覺效果](../../reporting-services/mobile-reports/add-visualizations-to-reporting-services-mobile-reports.md)
* [Reporting Services 行動報表中的資料格](../../reporting-services/mobile-reports/add-data-grids-to-mobile-reports-reporting-services.md) 
