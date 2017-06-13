---
title: "效能、 快照、 快取 (Reporting Services) |Microsoft 文件"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- performance [Reporting Services]
- Reporting Services, performance
ms.assetid: 85afd00f-e8d7-4ef7-9174-2ff84d82f960
caps.latest.revision: 20
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: c752ea8a5f05a1dc861b0297b7a1c0eaca5cfc88
ms.contentlocale: zh-tw
ms.lasthandoff: 06/13/2017

---
# <a name="performance-snapshots-caching-reporting-services"></a>效能、快照、快取 (Reporting Services)
  報表伺服器的效能會受到一些因素組合的影響，包括硬體、存取報表的並行使用者數目、報表中的資料量，以及輸出格式。 若要了解安裝特有的效能因素以及哪些補救措施可產生所需的結果，您必須取得基準資料並執行測試。 如需有關工具和指導方針的詳細資訊，請參閱下列 MSDN 出版品：＜ [Reporting Services 效能最佳化](http://blogs.msdn.com/b/sqlcat/archive/2013/10/30/reporting-services-performance-and-optimization.aspx) ＞和＜ [在 SQL Server 2005 Reporting Services 報表伺服器上使用 Visual Studio 2005 執行負載測試](http://go.microsoft.com/fwlink/?LinkID=77519)＞。  
  
 要考慮的一般原則包括下列各項：  
  
-   報表處理和轉譯是需要大量記憶體的作業。 可能的話，請選擇具有大量記憶的電腦。  
  
-   在個別的電腦上主控報表伺服器與報表伺服器資料庫會比在單一高階電腦上主控這兩個項目提供較佳的效能。  
  
-   如果所有報表的處理速度都很慢，請考慮採用向外延展部署，以便讓多個報表伺服器執行個體支援單一報表伺服器資料庫。 為了獲得最佳結果，請使用負載平衡軟體，將要求平均分散到部署中。  
  
-   如果單一報表的處理速度很慢，而且該報表必須視需要執行，請調整報表資料集查詢。 您也可以考慮使用您可以快取的共用資料集、快取報表，或將報表當做快照集執行。  
  
-   如果採用特定格式之所有報表的處理速度很慢 (例如，轉譯成 PDF 時)，請考慮採用檔案共用傳遞、加入更多記憶體，或選擇不同的格式。  
  
-   若要了解處理某份報表和其他使用標準需要多久，請檢閱報表伺服器執行記錄。 如需詳細資訊，請參閱 [報表伺服器 ExecutionLog 和 ExecutionLog3 檢視](../../reporting-services/report-server/report-server-executionlog-and-the-executionlog3-view.md)。  
  
-   如需有關如何透過微調記憶體管理組態設定來減少效能問題的詳細資訊，請參閱 [設定報表伺服器應用程式的可用記憶體](../../reporting-services/report-server/configure-available-memory-for-report-server-applications.md)。  
  
## <a name="in-this-section"></a>本節內容  
 [監視報表伺服器效能](../../reporting-services/report-server/monitoring-report-server-performance.md)  
 描述您可以用來追蹤伺服器之處理負載的效能物件。  
  
 [設定報表處理屬性](../../reporting-services/report-server/set-report-processing-properties.md)  
 描述將報表設定為視需要執行、從快取執行或依據排程當成報表快照集執行的方式。  
  
 [設定報表伺服器應用程式的可用記憶體](../../reporting-services/report-server/configure-available-memory-for-report-server-applications.md)  
 描述如何覆寫預設記憶體管理行為。  
  
 [快取多個報表 &#40;SSRS&#41;](../../reporting-services/report-server/caching-reports-ssrs.md)  
 描述報表伺服器上的報表快取行為。  
  
 [快取共用資料集 &#40;SSRS&#41;](../../reporting-services/report-server/cache-shared-datasets-ssrs.md)  
 描述報表伺服器上的共用資料集快取行為。  
  
 [處理大型報表](../../reporting-services/report-server/process-large-reports.md)  
 提供如何設定和散發大型報表的建議。  
  
 [設定報表和共用資料集處理的逾時值 &#40;SSRS&#41;](../../reporting-services/report-server/setting-time-out-values-for-report-and-shared-dataset-processing-ssrs.md)  
 說明如何設定查詢和報表處理的逾時。  
  
## <a name="see-also"></a>請參閱＜  
 [管理執行中的處理序](../../reporting-services/subscriptions/manage-a-running-process.md)   
 [驗證報表執行](../../reporting-services/report-server/verifying-a-report-run.md)  
  
  
