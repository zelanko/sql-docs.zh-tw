---
title: 使用特定查詢字串參數開啟行動報表 | Microsoft Docs
ms.date: 10/25/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: mobile-reports
ms.topic: conceptual
ms.assetid: 4eeb3204-e207-4ac0-aff3-bfc4926e5754
author: markingmyname
ms.author: maghan
ms.openlocfilehash: ca74d2d606dfddf394b0c7a32e8fe7d50f210934
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/15/2019
ms.locfileid: "56296019"
---
# <a name="open-a-mobile-report-with-specific-query-string-parameters--reporting-services"></a>使用特定查詢字串參數開啟行動報表 | Reporting Services
如果您的 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 行動報表具有參數與 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 或 [!INCLUDE[ssASnoversion_md](../../includes/ssasnoversion-md.md)] 資料來源，則可以在報表 URL 中包括查詢字串參數，以使用您指定的值來自動開啟報表。 
1.  建立 [含參數的行動報表](../../reporting-services/mobile-reports/add-parameters-to-a-mobile-report-reporting-services.md)。

2. 在行動報表發行工具中開啟報表，然後選取 [資料] 索引標籤。 

2. 在資料表底部的索引標籤上尋找資料集的名稱，以及您要的欄位名稱。 
    
    ![mobile-report-publisher-parameter-data-view](../../reporting-services/mobile-reports/media/mobile-report-publisher-parameter-data-view.png)
    
2.  URL 的語法取決於您的資料來源。 

     **SQL Server Analysis Services 資料來源**：使用查詢字串參數建置 URL，格式如下︰

    `https://<servername>/reports/<report-folder-name>/<report-name>?<dataset-name>.<field-name>=<parameter-value>`

    例如：
    
    `https://sampleserver/reports/adventureworks-reports/adventureworks-load-on-demand?TimeChartLoD.category=Clothing` 
    
     **SQL Server 資料來源**：查詢字串參數大致相同，但是在欄位名稱前要有 \@ 符號：

    `https://<servername>/reports/<report-folder-name>/<report-name>?<dataset-name>.@<field-name>=<parameter-value>`

    例如：
    
      `https://sampleserver/reports/adventureworks-reports/adventureworks-load-on-demand?TimeChartLoD.@category=Clothing` 

    
3.  此 URL 會在伺服器上開啟報表，並自動篩選至您指定的參數值。

    ![mobile-report-publisher-parameter-web-portal-view](../../reporting-services/mobile-reports/media/mobile-report-publisher-parameter-web-portal-view.png)

### <a name="see-also"></a>另請參閱

[將參數加入行動報表中](../../reporting-services/mobile-reports/add-parameters-to-a-mobile-report-reporting-services.md)

