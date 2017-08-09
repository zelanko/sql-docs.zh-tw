---
title: "建立索引標籤式的行動報表使用鑽研 |Reporting Services 行動報表 |Microsoft 文件"
ms.custom: 
ms.date: 03/30/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c4d5d80d-370a-4a6d-8b76-698bd5ba5ba6
caps.latest.revision: 9
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 6554f808c19540d2a3b7cbe3fdf4e86c5fe7a357
ms.contentlocale: zh-tw
ms.lasthandoff: 08/09/2017

---
# <a name="create-a-tabbed-mobile-report-by-using-drillthrough"></a>建立索引標籤式的行動報表使用鑽研
了解如何使用鑽研報表和參數建立 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 行動報表，使其外觀和行為類似索引標籤式報表。

例如，在此報表中，頂端的量測計會充當索引標籤。 當您按一下 Transportation 量測計時，圖表中的其餘資料會以傳輸資料進行篩選。

![06-Mobile-Report-Web-Viewer-Transportation](../../reporting-services/mobile-reports/media/tabbed-mobile-report-web-viewer-transportation-complete.png)

在幕後，這實際上是一組五份不同的報表，各有不同的參數可篩選報表，以符合報表頂端所選取的量測計。 首先，建立所有五個報表，然後針對每個的五個報表，您對其他四個量測計入 drillthroughs 其他四個報表。

以下是此範例中的步驟。

## <a name="create-the-basic-report"></a>建立基本報表

1. 建立稱為 Sales 且具有五個量測計的報表︰

    * Sales
    * Transportation
    * Fuel
    * 儲存空間
    * Misc Expenses

   ![01-sales-行動裝置版的報表-發行者](../../reporting-services/mobile-reports/media/01-sales-mobile-report-publisher.png)
    
2. 設定**腔調字**至**上**Sales 的量測計，因此它將會對照與其餘的報表--在此情況下，在黑色上的白色。

    ![01a-Sales-Accent-Mobile-Report-Publisher](../../reporting-services/mobile-reports/media/01a-sales-accent-mobile-report-publisher.png)
    
3. 將它儲存到[!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)]報表伺服器。

## <a name="make-copies-of-the-report"></a>建立報表的複本

1. 建立的銷售報表的四個複本，並將它們命名： 

    * Transportation
    * Fuel
    * 儲存空間
    * Misc Expenses

3. 儲存它們[!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)]報表伺服器。

## <a name="set-the-gauge-as-a-drillthrough"></a>設定量測計做為鑽研

本節中，在中，您可以將每個量測計 （非 Sales 的量測計） 做為鑽研至個別的報表。

1. 在銷售報表中，選取傳輸量測計。

    ![02-Sales-Create-DrillThrough-Mobile-Report-Publisher](../../reporting-services/mobile-reports/media/02-sales-create-drillthrough-mobile-report-publisher.png)

2. 與**配置** 索引標籤中選取**視覺屬性**窗格選取**鑽研目標**。

3. 選取**行動報表**。

4. 瀏覽並選取 在此情況下，將會用於鑽研-目的地報告 「 財務-運輸 」。

    ![03-Sales-Select-Dashboard-Mobile-Report-Publisher](../../reporting-services/mobile-reports/media/03-sales-select-dashboard-mobile-report-publisher.png)

5. 在**設定目標報表**，選取參數來篩選報表，然後選取**套用**。

   ![04-Sales-Apply-Parameters-Mobile-Report-Publisher](../../reporting-services/mobile-reports/media/04-sales-apply-parameters-mobile-report-publisher.png)
   
6. 針對每個銷售報表中其他量測計重複這些步驟。 

## <a name="set-the-gauges-for-the-other-reports"></a>設定量測計的其他報表

1.  開啟傳輸報表、 鑽研銷售額報表及其他三個量測計做為其個別報表的 drillthroughs 設定 Sales 的量測計。

2. 仍在運輸報表中，設定**腔調字**要傳輸量測計**上**，與報表的其餘部分。

3. 重複上述步驟燃料、 存放裝置，以及其他費用報表。 

## <a name="view-the-report-in-the-web-portal"></a>入口網站中檢視報表

1. 移至[!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)]報表伺服器，並開啟其中一個報表。 

2. 請注意每個量測計在右上角有鑽研圖示。

    ![Web-Viewer-drillthrough-icon-mobile-report-builder](../../reporting-services/mobile-reports/media/web-viewer-drillthrough-icon-mobile-report-builder.png)

3. 選取其中一個來移至報表的篩選後，該量測計的資料量測計。

   ![06-Mobile-Report-Web-Viewer-Transportation](../../reporting-services/mobile-reports/media/06-mobile-report-web-viewer-transportation.png)

### <a name="see-also"></a>另請參閱
    
* [將參數加入行動報表中](../../reporting-services/mobile-reports/add-parameters-to-a-mobile-report-reporting-services.md)
* [從行動報表將鑽研加入其他行動報表或 URL](../../reporting-services/mobile-reports/add-drillthrough-from-a-mobile-report-to-other-mobile-reports-or-urls.md)




  


