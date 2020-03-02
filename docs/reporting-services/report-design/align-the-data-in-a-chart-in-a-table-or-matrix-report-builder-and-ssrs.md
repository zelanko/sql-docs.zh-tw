---
title: 在資料表或矩陣的圖表上對齊資料 (報表產生器) | Microsoft Docs
ms.date: 03/03/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 75137575-d1bf-46d6-8527-5afc85eea5e1
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: c6cb82188a6ded92fadf96385f193f504c29bf56
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "77081520"
---
# <a name="align-the-data-in-a-chart-in-a-table-or-matrix-report-builder-and-ssrs"></a>在資料表或矩陣的圖表上對齊資料 (報表產生器及 SSRS)
  走勢圖和資料橫條很小，也就是以少量的外來細節傳達許多資訊的簡易圖表。 在 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 分頁報表中，當您核取這個選項時，走勢圖和資料橫條中的值將會跨資料表或矩陣中的不同資料格對齊，即使它們在其依據的資料中有遺漏值也是一樣。  
  
 ![rs_SparklineAlignData](../../reporting-services/report-design/media/rs-sparklinealigndata.gif "rs_SparklineAlignData")  
  
 在這個影像中，直條圖會顯示每一個員工的每天銷售量。 請注意，如果是員工沒有任何銷售量的日子，圖表就會留下空白，並將後續的日子水平對齊。 它也會使不同圖表的大小彼此相對，以垂直對齊圖表。 如需詳細資訊，請參閱 [走勢圖和資料橫條 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/sparklines-and-data-bars-report-builder-and-ssrs.md)。  
  
## <a name="align-the-data-in-a-sparkline-or-data-bar"></a>對齊走勢圖或資料橫條中的資料  
  
1.  [加入走勢圖或資料橫條](../../reporting-services/report-design/add-sparklines-and-data-bars-report-builder-and-ssrs.md) 至資料表或矩陣。  
  
2. 在走勢圖或資料橫條中按一下，然後按一下 **[水平軸屬性]** 或 **[垂直軸屬性]** 。  
  
2.  在 **[軸選項]** 索引標籤上，核取 **[對齊軸]** 方塊，然後在下拉方塊中，選取要對齊軸的群組。  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>另請參閱  
 [圖表 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/charts-report-builder-and-ssrs.md)   
 [加入走勢圖和資料橫條 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-design/add-sparklines-and-data-bars-report-builder-and-ssrs.md)  
  
  
