---
title: Reporting Services 行動報表中的自訂地圖 | Microsoft Docs
description: 了解 SQL Server 行動報表發行工具中的地圖，這是以 ESRI 形狀檔格式所定義。
ms.date: 12/06/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: mobile-reports
ms.custom: seodec18
ms.topic: conceptual
ms.assetid: 59a4ebad-587a-4770-afcd-c69216b8afd9
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 5e34e018cbbd1ecc9dd6258111cccf7132a682e7
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/15/2019
ms.locfileid: "56289066"
---
# <a name="custom-maps-in-reporting-services-mobile-reports"></a>Reporting Services 行動報表中的自訂地圖
SQL Server 行動報表發行工具的地理對應定義格式，稱為「ESRI 形狀檔」。  
  
最初由私人公司設計，這是現在大部分 GIS 應用程式廣泛使用的半開放式格式。 為配合這種格式，在定義對應時，行動報表發行工具需要有下列兩個檔案：  
  
- 用於圖形幾何的 .SHP 檔案  
- 用於中繼資料的 .DBF 檔案  
  
基底檔案名稱必須相符 (例如 *canada.shp* 和 *canada.dbf*)。 中繼資料必須包含 [名稱] 欄位和對應的圖形名稱值 (索引鍵)，以在對應中填入資料時使用。  

SHP 和 DBF 這兩個地圖檔案相加不能大於 512 KB。 如果地圖檔案太大，請使用 [https://mapshaper.org/](https://mapshaper.org/) 之類的工具減少其大小。  
  
請參閱如何 [將自訂地圖加入行動報表](../../reporting-services/mobile-reports/add-a-custom-map-to-a-reporting-services-mobile-report.md)。  
  
## <a name="technical-information"></a>技術資訊  
  
- 官方規格： [https://www.esri.com/library/whitepapers/pdfs/shapefile.pdf](https://www.esri.com/library/whitepapers/pdfs/shapefile.pdf)  
- Wikipedia shapefile 文章：[https://en.wikipedia.org/wiki/Shapefile](https://en.wikipedia.org/wiki/Shapefile)  
  
## <a name="creating--editing-map-geometry"></a>建立及編輯對應幾何  
  
建立和編輯形狀檔是複雜的程序，已超出本文討論範圍。 以下是一些可協助您開始的資源和應用程式︰  
  
- ArcGIS：[https://www.arcgis.com/](https://www.arcgis.com/)  
- MAPublisher plug-in for Adobe Illustrator：[https://www.avenza.com/mapublisher](https://www.avenza.com/mapublisher)  
- QuantumGIS (免費)：[https://www.qgis.org/](https://www.qgis.org/)  

## <a name="existing-shapefiles"></a>現有的形狀檔  
  
網路上有很多現成的形狀檔可以下載，例如 Diva-GIS 之類的網站︰[https://www.diva-gis.org/Data](https://www.diva-gis.org/Data)。  

## <a name="see-also"></a>另請參閱  
- [Reporting Services 行動報表中的地圖](../../reporting-services/mobile-reports/maps-in-reporting-services-mobile-reports.md)  
- [使用 SQL Server 行動報表發行工具建立與發行行動報表](../../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md)   
  
  
  
