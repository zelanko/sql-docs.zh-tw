---
title: 設定報表和共用資料集處理的逾時值 (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: report-server
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- time-outs [Reporting Services]
- query time-outs [Reporting Services]
- report processing [Reporting Services], time-outs
- report execution time-outs [Reporting Services]
ms.assetid: 0f9dc61d-d03c-4bbf-8090-7a53844350f8
caps.latest.revision: 39
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 1c41a408ee565bf63bac308b5d680599ad136cc8
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="setting-time-out-values-for-report-and-shared-dataset-processing-ssrs"></a>設定報表和共用資料集處理的逾時值 (SSRS)
  您可以 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 指定逾時值，以便設定系統資源的使用限制。 報表伺服器支援兩種逾時值：  
  
-   內嵌資料集查詢逾時值是報表伺服器等候資料庫回應的秒數。 此值是在報表中定義的。  
  
-   共用資料集查詢逾時值是報表伺服器等候資料庫回應的秒數。 此值是共用資料集定義的一部分，而且可以在報表伺服器上管理共用資料集時變更。  
  
-   報表執行逾時值是報表處理在停止之前，可以繼續的秒數上限。 此值是在系統層級定義的。 您可以針對個別報表更改此設定。  
  
 大部分的逾時錯誤會在查詢處理時發生。 如果您遇到逾時錯誤，請試著增加查詢逾時值。 請務必調整報表執行逾時值，使其大於查詢逾時。這個時間週期應該要足以完成查詢與報表處理。  
  
## <a name="setting-a-query-time-out-for-an-embedded-dataset-in-a-report"></a>設定報表中內嵌資料集的查詢逾時  
 當您定義內嵌資料集時，可在報表撰寫期間指定查詢逾時值。 逾時值會與報表一起儲存在報表定義的 **Timeout** 元素中。 依預設，此值設定為 30 秒。 如需詳細資訊，請參閱 [報表內嵌資料集和共用資料集 &#40;報表產生器及 SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)。  
  
 擁有權限修改已發行報表之屬性的使用者，可以編輯報表定義檔案，重設此值。  
  
 您也可以指定資料驅動訂閱的查詢逾時值。 查詢逾時值是在 [資料驅動訂閱] 頁面中指定的。 您指定的值會決定報表伺服器從訂閱者資料來源擷取資料時，等候查詢處理完成的時間長度。  
  
## <a name="setting-a-query-time-out-for-a-shared-dataset"></a>設定共用資料集的查詢逾時  
 當您建立或管理共用資料集時，可在報表伺服器上以秒數指定查詢逾時值。 根據預設，這個值是設定為 0 秒，相當於沒有逾時值。 如需詳細資訊，請參閱 [Manage Shared Datasets](../../reporting-services/report-data/manage-shared-datasets.md)(管理共用資料集)。  
  
## <a name="setting-a-report-execution-time-out"></a>設定報表執行逾時  
 您可以設定報表執行逾時值，來限制報表伺服器用於處理報表的時間量。 報表執行逾時值可以在報表管理員中指定。 您可以設定 [站台設定] 頁面中所有報表的預設值，然後覆寫特定報表在 [執行] 屬性頁面中的值。 依預設，此值設定為 1800 秒。 如需詳細資訊，請參閱 [Set Report Processing Properties](../../reporting-services/report-server/set-report-processing-properties.md)(設定報表處理屬性)。  
  
## <a name="how-report-execution-time-out-values-are-evaluated"></a>如何評估報表執行逾時值  
 報表伺服器會以 60 秒的間隔評估執行中的作業。 每間隔 60 秒，報表伺服器會比較實際的處理時間和報表執行逾時值。 如果報表的處理時間超過報表執行逾時值，就會停止報表的處理。  
  
 請注意，如果您指定少於 60 秒的逾時值，當報表伺服器還沒有評估執行中的作業之前，處理就已經在週期內開始和完成，則報表可能會完全執行。 例如，如果您將報表的逾時值設定為 10 秒，而報表需要 20 秒執行，那麼如果報表在 60 秒週期的較早時刻就開始執行，報表就會完全處理。  
  
> [!NOTE]  
>  您可以在 RSReportServer.config 檔案中設定 **RunningRequestsDbCycle** 設定，以變更評估執行中之作業的頻率。  
  
## <a name="see-also"></a>另請參閱  
 [設定處理選項 &#40;SharePoint 整合模式的 Reporting Services&#41;](../../reporting-services/report-server-sharepoint/set-processing-options-reporting-services-in-sharepoint-integrated-mode.md)   
 [Reporting Services 報表伺服器 &#40;原生模式&#41;](../../reporting-services/report-server/reporting-services-report-server-native-mode.md)   
 [管理執行中的處理序](../../reporting-services/subscriptions/manage-a-running-process.md)   
 [報表管理員 &#40;SSRS 原生模式&#41;](http://msdn.microsoft.com/library/80949f9d-58f5-48e3-9342-9e9bf4e57896)  
  
  
