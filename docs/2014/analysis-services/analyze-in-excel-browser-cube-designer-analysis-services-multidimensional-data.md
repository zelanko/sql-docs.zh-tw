---
title: 分析的 Excel （瀏覽器索引標籤，Cube 設計工具） (Analysis Services-多維度資料) |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.asvs.cubeeditor.browsecube.datapane.f1
- sql12.asvs.ssms.analyzeinexcel.f1
ms.assetid: 890ed457-137e-44ac-9b2c-83344a1b8fc9
caps.latest.revision: 22
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: b6e20d95fc7d1a097f50eb5cca4937cc62580ef3
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36132118"
---
# <a name="analyze-in-excel-browser-tab-cube-designer-analysis-services---multidimensional-data"></a>在 Excel 中進行分析 (瀏覽器索引標籤，Cube 設計師) (Analysis Services - 多維度資料)
  **[在 Excel 中進行分析]** 提供 Cube 開發人員一種方式，可快速檢閱使用者所看到的專案外觀。 **[在 Excel 中進行分析]** 功能可開啟 Microsoft Excel、建立工作空間資料庫的資料來源連接，以及自動將樞紐分析表加入工作表。 此功能取代舊版 [瀏覽器] 索引標籤中提供內嵌樞紐分析表的 Office Web 元件。  
  
 **若要檢視 cube 資料：**  
  
1.  在 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]的方案總管中，按兩下 Cube，在 Cube 設計師中加以開啟。  
  
2.  按一下 **[瀏覽器]** 索引標籤。  
  
3.  按一下 **[重新連接]** 驗證連接。  
  
4.  按一下功能表列上的 Excel 圖示。  
  
5.  當系統要求您啟用資料連接時，按一下 **[啟用]**。 Excel 會使用目前的資料連接來開啟，並將樞紐分析表加入工作表中，讓您可以開始瀏覽資料。  
  
 您現在可透過將事實資料表中的量值拖曳至 [值] 區域，並將維度屬性拖曳至 [資料列] 和 [資料行] 區域，以互動方式建立樞紐分析表。 如果您有階層，可將它們加入至 [資料列] 或 [資料行] 區域。 您可以積存或向下鑽研階層，瀏覽不同層級的事實資料。  
  
 物件及資料是在有效使用者或角色及檢視方塊的內容中進行檢視。 使用 Excel 執行查詢時，目前使用者的認證 (而非在 **[模擬資訊]** 頁面中指定的認證) 會用來連接資料來源。  
  
> [!NOTE]  
>  若要使用 [在 Excel 中進行分析] 功能，您必須在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]所在電腦上安裝 Excel。 如果未將 Excel 安裝在相同的電腦上，您可以在其他電腦上使用 Excel，然後連接至 Cube 做為資料來源。 然後即可手動將樞紐分析表加入工作表。 模型物件 (資料表、資料行、量值及 KPI) 會包含在樞紐分析表欄位清單中當做欄位。  
  
 如需有關 **[在 Excel 中進行分析]** 功能的詳細資訊，請參閱以下資源：  
  
 [在 Excel 中分析&#40;SSAS 表格式&#41;](tabular-models/analyze-in-excel-ssas-tabular.md)  
  
 [分析表格式模型在 Excel 中的&#40;SSAS 表格式&#41;](tabular-models/analyze-a-tabular-model-in-excel-ssas-tabular.md)  
  
 [瀏覽 Cube 中的資料和中繼資料](multidimensional-models/browse-data-and-metadata-in-cube.md)  
  
## <a name="see-also"></a>另請參閱  
 [瀏覽器&#40;Cube 設計師&#41; &#40;Analysis Services-多維度資料&#41;](browser-cube-designer-analysis-services-multidimensional-data.md)   
 [工具列&#40;瀏覽器索引標籤，Cube 設計工具&#41; &#40;Analysis Services-多維度資料&#41;](toolbar-browser-tab-cube-designer-analysis-services-multidimensional-data.md)   
 [中繼資料&#40;瀏覽器索引標籤，Cube 設計工具&#41; &#40;Analysis Services-多維度資料&#41;](metadata-browser-tab-cube-designer-analysis-services-multidimensional-data.md)   
 [查詢和篩選&#40;瀏覽器索引標籤，Cube 設計工具&#41; &#40;Analysis Services-多維度資料&#41;](query-filter-browser-cube-designer-analysis-services-multidimensional-data.md)  
  
  