---
title: "使用外部資料來源以取得訂閱者資料 (資料驅動訂閱) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: subscriptions
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- subscriber data sources [Reporting Services]
- subscriptions [Reporting Services], external data sources
- query-based subscriptions [Reporting Services]
- external data sources [Reporting Services]
- data-driven subscriptions
- data sources [Reporting Services], subscriptions
ms.assetid: 1cade8ec-729c-4df8-a428-e75c9ad86369
caps.latest.revision: "43"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: e8fce3d396a163c77b3b98bd7defd583f94d72b0
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/05/2017
---
# <a name="use-an-external-data-source-for-subscriber-data-data-driven-subscription"></a>使用外部資料來源以取得訂閱者資料 (資料驅動訂閱)
  在資料驅動訂閱中，動態訂閱資料是由從外部資料來源擷取資料的查詢或命令所提供。 訂閱資料可以從任何支援的資料來源 (符合資料驅動訂閱處理的需求) 中擷取。 查詢或命令語法必須對安裝在您報表伺服器上的資料處理延伸模組有效。  
  
## <a name="data-processing-requirements"></a>資料處理需求  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 會使用資料處理延伸模組來擷取訂閱資料。 建議的資料來源類型包含下列幾種：  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 關聯式資料庫  
  
-   Oracle 資料庫  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 多維度和資料採礦資料來源  
  
-   XML 資料來源  
  
     使用訂閱者資料的 XML 資料處理延伸模組時，請務必增加訂閱中的查詢逾時設定。 XML 資料處理延伸模組所使用查詢逾時值的單位是毫秒，而不是秒。 如果沒有增加逾時值，訂閱可能會因為處理時間不足而失敗。  
  
     設定訂閱者資料來源的連接時，請避免使用 **[不需要認證]** 選項。 使用 XML 資料處理延伸模組在執行階段擷取訂閱資料時，建議您使用預存認證。  
  
 您或許可以使用其他支援的資料來源類型，但不保證它們全部都能執行。 例如，訂閱者資料就無法使用下列資料來源類型：  
  
-   SAP Netweaver BI 資料庫  
  
-   報表模型  
  
 如果您希望在資料驅動訂閱中使用自訂的資料處理延伸模組，則該延伸模組必須實作 <xref:Microsoft.ReportingServices.DataProcessing.IDbCommand> 和 <xref:Microsoft.ReportingServices.DataProcessing.IDataReader> 介面。 該資料處理延伸模組必須支援僅限結構描述的查詢執行。 此查詢是用於在設計階段擷取資料行中繼資料，因此使用者可以將資料行對應至訂閱定義中的傳遞選項以及報表參數。 僅限結構描述的查詢執行會發生在使用者定義訂閱的初期階段。  
  
## <a name="query-requirements"></a>查詢需求  
 當您建立擷取訂閱資料的查詢時，請牢記下列幾點：  
  
-   您只能針對該訂閱建立一個查詢。  
  
-   該查詢必須傳回所有您要用於傳遞選項以及指定報表參數的值。  
  
-   報表伺服器將在結果集內為每一個資料列建立報表傳遞。 如果結果集是由三百個資料列組成，則報表伺服器將會嘗試傳遞三百個報表。  
  
## <a name="setting-delivery-options-using-variable-data-from-a-subscriber-database"></a>使用訂閱者資料庫的變數資料建立傳遞選項  
 您可以使用訂閱者資料庫中的資料，自訂每一個收件者的傳遞選項。 所使用的傳遞延伸模組種類會決定可用的選項。 如果您使用報表伺服器電子郵件傳遞延伸模組，則查詢應包含每一個訂閱者的電子郵件別名。 如果您使用檔案共用傳遞，訂閱者資料應包含可用來建立訂閱者特定報表檔案或提供傳遞目的地的值。 如需詳細資訊，請參閱 [Reporting Services 中的電子郵件傳遞](../../reporting-services/subscriptions/e-mail-delivery-in-reporting-services.md)。  
  
## <a name="passing-parameter-values-from-the-subscriber-database-to-the-report"></a>將參數值從訂閱者資料庫傳遞到報表  
 如果正在建立參數化報表的資料驅動訂閱，則可以使用可變個數參數值來自訂每份報表的輸出。 例如，訂閱者資料庫可能包含可用來篩選報表資料的員工識別碼、雇用日期、職稱和辦公室位置資訊。 如果報表接受以這些或其他可用的資料行資料為基礎的參數，您就可以將參數對應到適當的資料行。  
  
 將訂閱者欄位對應至報表參數時，請確定資料類型與資料行長度相容。 如果資料類型不符合，訂閱處理期間會發生錯誤。 若要深入了解如何使用參數化報表中的訂閱者資料，請參閱[建立資料驅動訂閱 &#40;SSRS 教學課程&#41;](../../reporting-services/create-a-data-driven-subscription-ssrs-tutorial.md)。  
  
## <a name="modifying-the-subscriber-data-source"></a>修改訂閱者資料來源  
 下列對訂閱者資料來源的修改會妨礙訂閱執行：  
  
-   移除在訂閱中所參考的資料行。  
  
-   修改資料來源的資料表結構。  
  
-   變更其他資料行屬性的資料類型。  
  
 如果您做了其中的任一變更，就必須更新訂閱。  
  
## <a name="see-also"></a>另請參閱  
 [建立、修改和刪除資料驅動訂閱](../../reporting-services/subscriptions/create-modify-and-delete-data-driven-subscriptions.md)   
 [資料驅動訂閱](../../reporting-services/subscriptions/data-driven-subscriptions.md)   
 [訂閱與傳遞 &#40;Reporting Services&#41;](../../reporting-services/subscriptions/subscriptions-and-delivery-reporting-services.md)  
  
  
