---
title: 使用鑽研建立索引標籤式的行動報表 | Reporting Services 行動報表 | Microsoft Docs
ms.date: 03/30/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: mobile-reports
ms.topic: conceptual
ms.assetid: c4d5d80d-370a-4a6d-8b76-698bd5ba5ba6
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: d01f9f1bef4d13cbce3f3e736cbef2f838c680ef
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "63061778"
---
# <a name="create-a-tabbed-mobile-report-by-using-drillthrough"></a>使用鑽研建立索引標籤式的行動報表
了解如何使用鑽研報表和參數建立 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 行動報表，使其外觀和行為類似索引標籤式報表。

例如，在此報表中，頂端的量測計會充當索引標籤。 當您按一下 Transportation 量測計時，圖表中的其餘資料會以傳輸資料進行篩選。

![06-Mobile-Report-Web-Viewer-Transportation](../../reporting-services/mobile-reports/media/tabbed-mobile-report-web-viewer-transportation-complete.png)

在幕後，這實際上是一組五份不同的報表，各有不同的參數可篩選報表，以符合報表頂端所選取的量測計。 您先建立共五份報表，然後針對這五份報表，您將其他四個量測計鑽研至其他四份報表。

此範例的步驟如下。

## <a name="create-the-basic-report"></a>建立基本報表

1. 建立稱為 Sales 且具有五個量測計的報表︰

    * Sales
    * Transportation
    * Fuel
    * 儲存體
    * Misc Expenses

   ![01-Sales-Mobile-Report-Publisher](../../reporting-services/mobile-reports/media/01-sales-mobile-report-publisher.png)
    
2. 將 Sales 量測計的 [輔色]  設為 [開啟]  ，以和報表其餘部分形成對比--本例中為黑色上的白色。

    ![01a-Sales-Accent-Mobile-Report-Publisher](../../reporting-services/mobile-reports/media/01a-sales-accent-mobile-report-publisher.png)
    
3. 儲存到 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 報表伺服器。

## <a name="make-copies-of-the-report"></a>建立報表的複本

1. 建立四份 Sales 報表的複本，並加以命名： 

    * Transportation
    * Fuel
    * 儲存體
    * Misc Expenses

3. 將它們儲存到 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 報表伺服器。

## <a name="set-the-gauge-as-a-drillthrough"></a>將量測計設定為鑽研

在此區段中，將 (Sales 量測計以外的) 每個量測計設定為鑽研至其個別報表。

1. 在 Sales 報表中，選取 Transportation 量測計。

    ![02-Sales-Create-DrillThrough-Mobile-Report-Publisher](../../reporting-services/mobile-reports/media/02-sales-create-drillthrough-mobile-report-publisher.png)

2. 選取 [版面配置]  索引標籤，然後在 [視覺屬性]  窗格中，選取 [鑽研目標]  。

3. 選取 [行動報表]  。

4. 巡覽並選取鑽研目的地的報表，本例中為 "Financials - Transportation"。

    ![03-Sales-Select-Dashboard-Mobile-Report-Publisher](../../reporting-services/mobile-reports/media/03-sales-select-dashboard-mobile-report-publisher.png)

5. 在 [設定目標報表]  ，選取篩選報表的參數，然後選取 [套用]  。

   ![04-Sales-Apply-Parameters-Mobile-Report-Publisher](../../reporting-services/mobile-reports/media/04-sales-apply-parameters-mobile-report-publisher.png)
   
6. 針對 Sales 報表中的其他量測計一一重複這些步驟。 

## <a name="set-the-gauges-for-the-other-reports"></a>設定其他報表的量測計

1.  開啟 Transportation 報表，設定 Sales 量測計鑽研至銷售報表，並設定其他三個量測計鑽研至其個別報表。

2. 仍然在 Transportation 報表中，將 Transportation 量測計的 [輔色]  設為 [開啟]  ，與報表的其餘部分對比。

3. 針對 Fuel、Storage 和 Misc Expenses 報表，重複上述步驟。 

## <a name="view-the-report-in-the-web-portal"></a>在入口網站中檢視報表

1. 移至 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 報表伺服器，並開啟其中一份報表。 

2. 請注意，每個量測計的右上角都有鑽研圖示。

    ![Web-Viewer-drillthrough-icon-mobile-report-builder](../../reporting-services/mobile-reports/media/web-viewer-drillthrough-icon-mobile-report-builder.png)

3. 選取其中一個量測計，移至報表篩選後的量測計資料。

   ![06-Mobile-Report-Web-Viewer-Transportation](../../reporting-services/mobile-reports/media/06-mobile-report-web-viewer-transportation.png)

### <a name="see-also"></a>另請參閱
    
* [將參數加入行動報表中](../../reporting-services/mobile-reports/add-parameters-to-a-mobile-report-reporting-services.md)
* [從行動報表將鑽研加入其他行動報表或 URL](../../reporting-services/mobile-reports/add-drillthrough-from-a-mobile-report-to-other-mobile-reports-or-urls.md)




  

