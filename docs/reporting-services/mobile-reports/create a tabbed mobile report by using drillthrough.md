---
title: "使用鑽研建立索引標籤式的行動報表 | Reporting Services 行動報表 | Microsoft Docs"
ms.custom: ""
ms.date: "12/09/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: c4d5d80d-370a-4a6d-8b76-698bd5ba5ba6
caps.latest.revision: 9
author: "maggiesMSFT"
ms.author: "maggies"
manager: "erikre"
---
# 使用鑽研建立索引標籤式的行動報表 | Reporting Services 行動報表
了解如何使用鑽研報表和參數建立 [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] 行動報表，使其外觀和行為類似索引標籤式報表。

例如，在此報表中，頂端的量測計會充當索引標籤。 當您按一下 Transportation 量測計時，圖表中的其餘資料會以傳輸資料進行篩選。

![06-Mobile-Report-Web-Viewer-Transportation](../../reporting-services/mobile-reports/media/06-mobile-report-web-viewer-transportation.png)

在幕後，這實際上是一組五份不同的報表，各有不同的參數可篩選報表，以符合報表頂端所選取的量測計。 

在此範例中，您先建立共五份報表，然後針對這五份報表，您將其他四個量測計鑽研至其他四份報表。 

以下是這些步驟的高階大綱。

1. 建立稱為 Sales 且具有五個量測計的報表︰
     - Sales
     - Transportation
     - Fuel
     - 儲存空間
     - Misc Expenses
2. 建立四個報表複本，稱為： 
     - Transportation
     - Fuel
     - 儲存空間
     - Misc Expenses
3.  在 Sales 報表中，設定這四個量測計 (非 Sales 量測計) 鑽研至其個別報表。

4. 仍然在 Sales 報表中，設定 Sales 量測計的 Accent 屬性，其與報表的其餘部分對比，因此更為引人注目。

5.  現在，在 Transportation 報表中，設定 Sales 量測計鑽研至 Sales 報表，並設定其他三個量測計鑽研至其個別報表。

6. 再次，仍然在 Transportation 報表中，設定 Transportation 量測計的 Accent 屬性，其與報表的其餘部分對比。

5. 針對 Fuel、Storage 和 Misc Expenses 報表，重複上述步驟。 







  
