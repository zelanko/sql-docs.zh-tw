---
title: 準備 Reporting Services 行動報表的資料 | Microsoft Docs
ms.custom: ''
ms.date: 02/08/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.component: mobile-reports
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 8adce9ad-6a08-4d20-b1cf-d3c45544d8de
caps.latest.revision: 15
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 731b28c5f2f269d9527a7ba846beec747680ffe5
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "33020135"
---
# <a name="prepare-data-for-reporting-services-mobile-reports"></a>準備 Reporting Services 行動報表的資料
  
[!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-long.md)] 支援多個複雜資料作業 (包括篩選、彙總和時間切割)。 本文提供準備資料時需要注意的一些重點。 預先彙總資料可以最佳化行動報表建立和使用，而且某些行動報表設計需要它。   
  
## <a name="date-and-time-formats"></a>日期和時間格式 
如果處理要用於行動報表中的日期和時間間隔 (特別是使用 TimeNavigator 時)，一定要適當地格式化日期/時間資料行，讓 [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)] 將它識別為這類日期/時間。 以下是有效的日期/時間格式範例︰  
  
    05/01/2009    
    2009-05-01    
    05/01/2009 14:57:32.8    
    2009-05-01 14:57:32.8    
    2009-05-01T14:57:32.8375298-04:00    
    5/01/2008 14:57:32.80 -07:00    
    1 May 2008 2:57:32.8 PM    
    Fri, 15 May 2009 20:10:57 GMT    
  
在大部分情況下，可以根據一個以上的日期/時間間隔 (例如每小時、每日、每月、每季和每年) 來描述日期和時間資料集。 [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)] 可以合併多個不同資料粒度的資料表，並在單一行動報表上予以顯示。 不過，請記住原始資料集的相關間隔，因為它們有助於決定最終行動報表中向使用者顯示的日期/時間篩選選項。  

[!INCLUDE[ssASnoversion_md](../../includes/ssasnoversion-md.md)] 多維度和表格式模型中的日期欄位可能會遺失它們在共用資料集中的日期格式。 請參閱 [保留行動報表中 Analysis Services 資料的日期格式](../../reporting-services/mobile-reports/retain-date-formatting-for-analysis-services-in-mobile-reports.md) 以取得保留其格式的方案。
  
## <a name="preparing-filter-data"></a>準備篩選資料 ##  
[!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)] 可以根據日期/時間欄位和索引鍵欄位來篩選資料。 雖然索引鍵欄位可以是數值，但是在大部分情況下會是識別碼或字串值。 若要準備與導覽器元素 (例如選擇清單) 搭配使用的篩選欄位，篩選索引鍵應該是資料表中的單一資料行。 因此，您可以根據篩選資料行中的值對資料表資料列進行分組。 擁有多個資料行會包含不同的篩選索引鍵或篩選準則，讓行動報表具有以階層方式或個別方式使用的多個篩選導覽器。  
  
| Industry  | Country   | Region    |  
| ------------- | ------------- | ------------- |  
| Banks     | AFGHANISTAN   | ASIA      |  
| Commercial & Professional Services | AFGHANISTAN | ASIA |  
| Food, Beverage & Tobacco | AFGHANISTAN | ASIA |  
| 媒體 | AFGHANISTAN | ASIA |  
| Pharmaceuticals | AFGHANISTAN | ASIA |  
| Food & Staples Retailing | ALBANIA | EUROPE |  
  
  
索引鍵篩選也可能是階層結構，以與樹狀結構中的選擇清單搭配使用。 若要準備資料以在這類情況下使用，請建立可描述階層結構的查閱資料表。 使用包含索引鍵資料行和父索引鍵資料行的資料表結構，指出節點在整體階層中所屬的位置。  
  
在此資料表中，ParentKey 項目會先列於 ItemKey 資料行中，再列於其子項目旁邊的 ParentItemKey 資料行中。   
  
|ItemKey    | ParentItemKey |  
| ------------- | ------------- |  
| Financials    |   |  
| Industrials   |   |  
| Consumer Staples |    |  
| Consumer Discretionary |  |     
| 健康照護   |   |  
| Information Technology |  |  
| Banks | Financials |  
| Real Estate | Financials |  
| Diversified Financials |  Financials |   
| Insurance |   Financials |  
| Commercial & Professional Services |  Industrials |  
| Capital Goods |   Industrials |  
| Transportation |  Industrials |  
| Food, Beverage & Tobacco |    Consumer Staples |  
| Food & Staples Retailing |    Consumer Staples |  
| Household & Personal Products | Consumer Staples |  
| 媒體 | Consumer Discretionary |  
| Automobiles and Components |  Consumer Discretionary |  
| Consumer Durables and Apparel |Consumer Discretionary |  
| Consumer Services |   Consumer Discretionary |  
| Retailing | Consumer Discretionary |  
| Pharmaceuticals   | 健康照護 |  
| Health Care Equipment & Services |    健康照護 |  
| Software & Services | Information Technology |  
| Technology Hardware & Equipment   | Information Technology |  
| Telecommunication Services |Information Technology |  
  
### <a name="see-also"></a>另請參閱  
- [準備 Reporting Services 行動報表的 Excel 資料](../../reporting-services/mobile-reports/prepare-excel-data-for-reporting-services-mobile-reports.md)  
- [保留行動報表中 Analysis Services 資料的日期格式](../../reporting-services/mobile-reports/retain-date-formatting-for-analysis-services-in-mobile-reports.md)
- [使用 SQL Server 行動報表發行工具建立行動報表](../../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md)
  
  
  

