---
title: "圖表中的空白和 Null 資料點 (報表產生器及 SSRS) | Microsoft Docs"
ms.custom: 
ms.date: 05/30/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-design
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: faddd29d-4cc1-4c2c-8e29-d3d9918fe22a
caps.latest.revision: "10"
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 627e71fcbd48a533a61abbbf29f4db20c2f5d6e3
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/09/2018
---
# <a name="empty-and-null-data-points-in-charts-report-builder-and-ssrs"></a>圖表中的空白和 Null 資料點 (報表產生器及 SSRS)

  如果您要在 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 分頁報表的圖表中顯示包含空白或 Null 值的欄位，圖表外觀可能不如您預期。 圖表會根據指定的圖表類型，以不同的方式處理空白值：  
  
-   如果圖表類型是線性圖表類型 (橫條圖、直條圖、散佈圖、折線圖、區域圖、範圍圖)，則空白值會在圖表中顯示為空格或「間距」。 如果想要指出空點，必須加入空點預留位置。 如需詳細資訊，請參閱[新增空白點至圖表 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/add-empty-points-to-a-chart-report-builder-and-ssrs.md)。  
  
-   如果圖表類型是連續的線性圖表類型 (區域圖、橫條圖、直條圖、折線圖、散佈圖)，則空白的資料點會加入到圖表以維持數列的連續性。  
  
-   如果圖表類型是非線性圖表類型 (極座標圖、圓形圖、環圈圖、漏斗圖或金字塔圖)，則圖表會省略空白值的顯示。  
  
-   形狀圖圖表類型中會省略 Null 值。  
  
 具有空資料點的圖表範例可從範例報表取得。 如需下載這個範例報表及其他項目的詳細資訊，請參閱 [報表產生器與報表設計師範例報表](http://go.microsoft.com/fwlink/?LinkId=198283)：  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="removing-empty-or-null-values"></a>移除空白或 Null 值  
 若要避免重要資料不易辨認，請考慮從資料集移除空白值。 若要篩選 Null 值，可以在查詢中使用 NOT IS NULL 子句。 或者也可以加入篩選運算式，指定您只要顯示不等於零的值。 如需詳細資訊，請參閱 [加入資料集篩選、資料區篩選和群組篩選 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/add-dataset-filters-data-region-filters-and-group-filters.md)。  
  
## <a name="fields-with-no-values-in-a-chart"></a>圖表中沒有值的欄位  
 如果在傳回的資料集中欄位未包含任何值，則圖表會顯示沒有資料點的空白圖表，但會加入數列名稱 (通常為欄位名稱) 做為圖例項目。  
  
 這項行為與傳回資料集中有零個資料列的情況不同，後者可能會發生在當報表已進行參數化，而選取的值傳回空白結果集時。 如果資料集查詢傳回零個資料列，則系統會在執行階段會顯示訊息，指出沒有可以顯示的資料。 您可以在 [屬性] 窗格中修改報表的 NoDataMessage 標題，以自訂這個訊息。 如需詳細資訊，請參閱 [報表內嵌資料集和共用資料集 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)。  

## <a name="next-steps"></a>後續步驟

[圖表](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)   
[格式化圖表](../../reporting-services/report-design/formatting-a-chart-report-builder-and-ssrs.md)   
[圖表至報表](../../reporting-services/report-design/add-a-chart-to-a-report-report-builder-and-ssrs.md)   
[針對圖表進行疑難排解](../../reporting-services/report-design/troubleshoot-charts-report-builder-and-ssrs.md)  

更多問題嗎？ [請嘗試詢問 Reporting Services 論壇](http://go.microsoft.com/fwlink/?LinkId=620231)
