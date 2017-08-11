---
title: "加入行動報表中的資料格 |Reporting Services |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: fe98a970-90d3-44d1-9189-9141c237f141
caps.latest.revision: 4
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: c51169b12265eea7e6d57e0daa7539322e338851
ms.contentlocale: zh-tw
ms.lasthandoff: 08/09/2017

---
# <a name="add-data-grids-to-mobile-reports--reporting-services"></a>將資料格加入行動報表 | Reporting Services
有時候，資料本身就是最佳的視覺效果。 深入了解三個*資料格*，或資料表，來顯示資料在[!INCLUDE[SS_MobileReptPub_Long](../../includes/ss-mobilereptpub-long.md)]:
* 簡易資料格
* 指示器資料格
* 圖表資料格

## <a name="simple-data-grid"></a>簡易資料格
最基本的簡易資料格可顯示多個含有自訂格式和標頭的資料行。 

![mobile-report-simple-data-grid](../../reporting-services/mobile-reports/media/mobile-report-simple-data-grid.png)

將資料格加入設計介面之後，您可以將它連接到實際資料。

1. 拖曳從簡單的資料格**配置**索引標籤加入設計格線，並讓您想要的大小。

2. 取得 [Excel 或共用資料集的資料](../../reporting-services/mobile-reports/data-for-reporting-services-mobile-reports.md)。

3. 選取**資料** 索引標籤，然後在**資料屬性**窗格下**格線檢視的資料**選取資料表。

4. 在**資料行** 窗格中，選取您想要的資料行。 重新排列及重新命名這些資料行，並設定其格式和彙總方式。 

 
##  <a name="indicator-data-grid"></a>指示器資料格
您可以將含有量測計的資料行加入指示器資料格。

![mobile-report-indicator-data-grid](../../reporting-services/mobile-reports/media/mobile-report-indicator-data-grid.png)

1. 拖曳從指示器資料格**配置**索引標籤加入設計格線，並讓您想要的大小。

2. 在**資料**索引標籤中**資料行**窗格中，選取**加入量測計資料行**。 

3. 選取**選項**，然後選取**量測計類型**。 

4. 設定**值**和**比較**欄位和**值方向**，就像是[您直接加入至您的行動報表的量測計](../../reporting-services/mobile-reports/add-gauges-to-mobile-reports-reporting-services.md)。

資料格只會將該列資料格特定的資料自動饋送給量測計。  

## <a name="chart-data-grid"></a>圖表資料格
您可以將含有量測計或圖表的資料行加入圖表資料格。 

![mobile-report-chart-data-grid](../../reporting-services/mobile-reports/media/mobile-report-chart-data-grid.png)

當您將圖表資料行加入資料格時，您必須加入個別資料表，以提供資料給每個資料列中的圖表。 此第二個資料表必須與主資料表共用一個欄位，以將每個資料列連結至其關聯的圖表資料。 

1. 拖曳圖表資料格從**配置**索引標籤加入設計格線，並讓您想要的大小。

2. 在**資料**索引標籤中**資料行**窗格中，選取**新增圖表資料行**。 

3. 如果您還沒有這麼做，請取得 [Excel 或共用資料集的資料](../../reporting-services/mobile-reports/data-for-reporting-services-mobile-reports.md) ，以新增與主資料表共用一個欄位的第二個資料表。

4. 在下**資料屬性**，主要資料中選取資料表**格線檢視的資料**，然後選取第二個資料表中的**圖表視覺效果的參考資料**。

5. 選取**選項**，然後選取**圖表類型**。
 
6. 選取**圖表資料欄位**，**來源查閱**，和**目的地查閱**。 
   這三個屬性會決定資料格如何提供資料給資料行中的每個圖表。
   
   *   **來源查閱**設定為資料表中的資料中的欄位**格線檢視的資料**。 此欄位可作為每個資料列的篩選器，它會套用至圖表參考資料表，以針對每個資料列提供資料給內嵌圖表。 
   * **目的地查閱**是中的資料表中的欄位**圖表視覺效果的參考**。 每個資料列中圖表的資料，將會在那兩個欄位上聯結。   
   * **圖表資料欄位**決定中的度量**圖表視覺效果的參考**来做為每個資料列中圖表數列的 y 軸值的資料表。  

## <a name="see-also"></a>另請參閱 
* [Reporting Services 行動報表中的地圖](../../reporting-services/mobile-reports/maps-in-reporting-services-mobile-reports.md)
* [Reporting Services 行動報表中的導覽器](../../reporting-services/mobile-reports/add-navigators-to-reporting-services-mobile-reports.md)
* [Reporting Services 行動報表中的視覺效果](../../reporting-services/mobile-reports/add-visualizations-to-reporting-services-mobile-reports.md)
* [Reporting Services 行動報表中的量測計](../../reporting-services/mobile-reports/add-gauges-to-mobile-reports-reporting-services.md)  
 
  

