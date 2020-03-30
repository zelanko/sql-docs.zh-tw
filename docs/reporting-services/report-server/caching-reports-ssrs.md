---
title: 快取報表 | Microsoft Docs
ms.date: 05/14/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server
ms.topic: conceptual
helpviewer_keywords:
- report execution properties [Reporting Services]
- cache [Reporting Services]
- report processing [Reporting Services], caching
- cached instances [Reporting Services]
- refreshing cache
- cached reports [Reporting Services]
- preloading cache
- invalid cached reports [Reporting Services]
- performance [Reporting Services]
- expiration [Reporting Services]
- snapshots [Reporting Services], caching
ms.assetid: 146542c3-8efd-4b89-a8d8-77d22896630e
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 3e94ed2c05d3c23585abde1f2452f491be089e84
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "77082565"
---
# <a name="caching-reports-ssrs"></a>快取多個報表 (SSRS)
  報表伺服器可以快取已處理報表的副本，並在使用者開啟報表時還原該副本。 對使用者而言，能夠指出報表是快取副本的唯一證據是報表執行的日期和時間。 如果日期或時間不是目前的日期和時間，且報表不是快照集，則報表是從快取擷取而來。  
  
 如果報表很大或存取頻繁，快取就可以縮短擷取報表所需的時間。 如果伺服器重新開機，所有快取的執行個體都會在報表伺服器 Web 服務再次上線時恢復。  
  
 快取是一種效能增強技術。 快取的內容為動態，而且會隨報表加入、取代或移除而變更。 如果您需要更可預測的快取策略，就應該建立報表快照集。 如需詳細資訊，請參閱 [設定報表處理屬性](../../reporting-services/report-server/set-report-processing-properties.md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 會將暫存檔儲存在資料庫中，以便支援使用者工作階段和報表處理。 這些檔案會快取供內部使用，以及在單一瀏覽器工作階段期間支援一致的檢視體驗。 如需如何快取內部使用暫存檔的詳細資訊，請參閱[報表伺服器資料庫 &#40;SSRS 原生模式&#41;](../../reporting-services/report-server/report-server-database-ssrs-native-mode.md)。  
  
## <a name="cached-instances"></a>快取執行個體  
 報表的快取執行個體是以報表的中繼格式為基礎。 報表伺服器一般會以報表名稱為基礎，快取一個報表的執行個體。 不過，如果報表依據查詢參數而包含不同的資料，則在任何給定時間可能會快取多種版本的報表。 例如，假設您有一個將區域代碼當成參數值的參數化報表。 如果 4 個不同的使用者指定了 4 個唯一的區域代碼，就會建立 4 個快取副本。  
  
 第一個以唯一的區域代碼執行報表的使用者，會建立一個包含該區域資料的快取報表。 使用相同區域代碼要求報表的後續使用者會取得快取副本。  
  
 並非所有報表都可以快取。 如果報表包含使用者相依的資料、提示使用者輸入認證或使用 Windows 驗證，則無法快取。  
  
## <a name="refreshing-the-cache"></a>重新整理快取  
 如果使用者在先前的快取副本過期後選取報表，快取報表就會以較新版本取代。 設定當成快取執行個體執行的報表，會依據逾期設定，定期從快取移除。 您可以設定報表以分鐘為單位的逾期或在排程的時間逾期，這由資料的直接需求決定。 除非使用 SOAP API，否則無法直接從快取刪除報表。  
  
 若要設定快取逾期，可以使用共用排程或報表特定排程。 如果您使用共用排程而且後來暫停，則當排程無法作業時，快取不會過期。 如果共用排程後來被刪除，則排程設定的副本會儲存為報表特定排程。  
  
 如果排程過期或排程引擎在快取到期日時無法使用，則報表伺服器會執行即時報表，直到已排程的作業可以繼續為止 (方法是延長排程或啟動排程服務)。  
  
## <a name="preloading-the-cache"></a>預先載入快取  
 若要提升伺服器效能，您可以預先載入快取。 您可以使用兩種方式，預先載入包含參數化報表執行個體集合的快取：  
  
1.  建立快取重新整理計畫。 當您建立重新整理計畫時，可以指定單一報表的排程，或指定共用排程。  
  
2.  建立使用 Null 傳遞提供者的資料驅動訂閱。 您指定 Null 傳遞提供者做為訂閱中傳遞的方法時，報表伺服器會以報表伺服器資料庫做為傳遞目的地目標，並使用名為 Null 轉譯延伸模組的特定轉譯延伸模組。 相較於其他傳遞延伸模組，Null 傳遞提供者並沒有您可以透過訂閱定義來設定的傳遞設定。  
  
 如果您要快取參數化報表的多個執行個體，其中使用不同的參數值來產生不同的報表執行個體，快取報表特別有用。 請注意，您只能在報表上指定查詢式參數。  
  
 當您指定排程或建立資料驅動訂閱時，必須排程報表傳遞至快取的頻率。 舊副本必須已經過期，新副本才能傳遞至快取。 因此，必須設定報表的執行屬性，以包含快取逾期設定。 逾期設定必須與您定義的訂閱排程一致。 例如，您若是建立一個每晚執行的訂閱，則快取也必須在每天晚上訂閱的執行階段之前過期。 如果執行屬性未包含逾期時間，則會略過較新的傳遞。 如需快取重新整理計劃的詳細資訊，請參閱 [排程](../../reporting-services/subscriptions/schedules.md)。 如需設定屬性的詳細資訊，請參閱 [設定報表處理屬性](../../reporting-services/report-server/set-report-processing-properties.md)。 如需使用資料驅動訂閱的詳細資訊，請參閱 [資料驅動訂閱](../../reporting-services/subscriptions/data-driven-subscriptions.md)。  
  
## <a name="conditions-that-cause-cache-expiration"></a>造成快取逾期的條件  
 快取報表會因回應下列事件而無效：已修改報表定義、已修改報表參數、資料來源認證變更，或報表執行選項變更。 如果您刪除儲存在快取中的報表，也會刪除快取的版本。  
  
 如果因為任何原因造成報表無法從快取執行個體轉譯 (例如，若使用者指定的參數值與用於產生快取報表的參數值不同)，則報表伺服器會重新執行報表。  
  
## <a name="see-also"></a>另請參閱  
 [設定處理選項 &#40;SharePoint 整合模式的 Reporting Services&#41;](../../reporting-services/report-server-sharepoint/set-processing-options-reporting-services-in-sharepoint-integrated-mode.md)   
 [設定報表處理屬性](../../reporting-services/report-server/set-report-processing-properties.md)   
 [Reporting Services 概念 &#40;SSRS&#41;](../../reporting-services/reporting-services-concepts-ssrs.md)   
 [預先載入快取](../../reporting-services/report-server/preload-the-cache-report-manager.md)   
 [[排程]](../../reporting-services/subscriptions/schedules.md)   
 [快取共用資料集 &#40;SSRS&#41;](../../reporting-services/report-server/cache-shared-datasets-ssrs.md)   
  
  
