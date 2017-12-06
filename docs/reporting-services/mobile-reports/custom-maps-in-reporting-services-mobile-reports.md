---
title: "Reporting Services 行動報表中的自訂地圖 | Microsoft Docs"
ms.custom: 
ms.date: 03/30/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.service: 
ms.component: mobile-reports
ms.reviewer: 
ms.suite: pro-bi
ms.technology: reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 59a4ebad-587a-4770-afcd-c69216b8afd9
caps.latest.revision: "9"
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 52c855f145dc16e2c7ed796485ae88dd2b7fd7a1
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/05/2017
---
# <a name="custom-maps-in-reporting-services-mobile-reports"></a>Reporting Services 行動報表中的自訂地圖
SQL Server 行動報表發行工具的地理對應定義格式，稱為「ESRI 形狀檔」。  
  
最初由私人公司設計，這是現在大部分 GIS 應用程式廣泛使用的半開放式格式。 為配合這種格式，在定義對應時，行動報表發行工具需要有下列兩個檔案：  
  
- 用於圖形幾何的 .SHP 檔案  
- 用於中繼資料的 .DBF 檔案  
  
基底檔案名稱必須相符 (例如 *canada.shp* 和 *canada.dbf*)。 中繼資料必須包含 [名稱] 欄位和對應的圖形名稱值 (索引鍵)，以在對應中填入資料時使用。  
  
> **注意**︰SHP 和 DBF 這兩個對應檔案相加不能大於 512 KB。 如果地圖檔案太大，請使用 [http://mapshaper.org/](http://mapshaper.org/) 之類的工具減少其大小。  
  
請參閱如何 [將自訂地圖加入行動報表](../../reporting-services/mobile-reports/add-a-custom-map-to-a-reporting-services-mobile-report.md)。  
  
## <a name="technical-information"></a>技術資訊  
  
- 官方規格︰ [http://www.esri.com/library/whitepapers/pdfs/shapefile.pdf](http://www.esri.com/library/whitepapers/pdfs/shapefile.pdf)  
- Wikipedia 形狀檔： [http://en.wikipedia.org/wiki/Shapefile](http://en.wikipedia.org/wiki/Shapefile)  
  
## <a name="creating--editing-map-geometry"></a>建立及編輯對應幾何  
  
建立和編輯形狀檔是複雜的程序，已超出本文討論範圍。 以下是一些可協助您開始的資源和應用程式︰  
  
- ArcGIS： [http://www.arcgis.com/](http://www.arcgis.com/)  
- MAPublisher plug-in for Adobe Illustrator： [http://www.avenza.com/mapublisher](http://www.avenza.com/mapublisher)  
- QuantumGIS (免費)： [http://www.qgis.org/](http://www.qgis.org/)  
- Manco 形狀檔編輯器： [http://www.mancosoftware.com/ShapeFileEditor](http://www.mancosoftware.com/ShapeFileEditor)  
  
## <a name="existing-shapefiles"></a>現有的形狀檔  
  
網路上有很多現成的形狀檔可以下載，例如︰  
  
- Diva-GIS： [http://www.diva-gis.org/Data](http://www.diva-gis.org/Data)  
- OpenStreetMap： [http://openstreetmapdata.com/data](http://openstreetmapdata.com/data)  
  
### <a name="see-also"></a>另請參閱  
- [Reporting Services 行動報表中的地圖](../../reporting-services/mobile-reports/maps-in-reporting-services-mobile-reports.md)  
- [使用 SQL Server 行動報表發行工具建立與發行行動報表](../../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md)   
  
  
  
