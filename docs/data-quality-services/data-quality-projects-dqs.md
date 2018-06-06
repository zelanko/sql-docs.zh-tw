---
title: 資料品質專案 (DQS) | Microsoft Docs
ms.custom: ''
ms.date: 10/01/2012
ms.prod: sql
ms.prod_service: data-quality-services
ms.component: data-quality-services
ms.reviewer: ''
ms.suite: sql
ms.technology:
- data-quality-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: a43fc9c0-19b6-414a-8661-4c7c55e0c03e
caps.latest.revision: 16
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 0464fb86b6ac1da08d8421026859539beecd7b91
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="data-quality-projects-dqs"></a>資料品質專案 (DQS)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) 中的資料品質專案是使用知識庫改善來源資料品質的一種工具，其方式是執行 *資料清理* 和 *資料比對* 活動，然後將產生的資料匯出到 SQL Server 資料庫或 .csv 檔案。 您可以建立資料品質專案當做清理專案或比對專案，以執行各自的活動。 清理專案和比對專案可以使用相同的知識庫執行，因為用於資料清理和比對的知識可以內建到相同的知識庫中。  
  
 資料品質專案具有以下優點：  
  
-   可讓您使用 DQS 知識庫中的知識來針對來源資料執行資料清理。  
  
-   可讓您使用知識庫中的比對原則來針對來源資料執行資料比對。  
  
-   提供精靈引導您執行清理和比對活動，並根據您的選擇將資料匯出到 SQL Server 資料庫或 .csv 檔案。 資料監管可以使用資料品質專案來執行及控制電腦輔助/互動式清理和資料比對步驟。  
  
##  <a name="Cleansing"></a> 資料品質專案：清理活動  
 清理資料品質專案可讓您根據知識庫來清理來源資料。 DQS 中的資料清理活動是兩個步驟的程序：  
  
1.  *電腦輔助* 資料清理程序，可針對知識庫中的知識分析來源資料以及建議變更。 處理過的資料會由 DQS 加以分類 (建議、新的、無效、已更正和正確)，然後顯示給使用者以供進一步處理。  
  
2.  *互動式* 清理程序，可讓資料監管核准、拒絕或修改電腦輔助的資料清理程序所提議的資料。  
  
 如需有關資料品質專案中清理活動的詳細資訊，請參閱＜ [Data Cleansing](../data-quality-services/data-cleansing.md)＞。  
  
##  <a name="Matching"></a> 資料品質專案：比對活動  
 比對資料品質專案可讓您根據知識庫中的比對原則來執行比對活動，藉由識別完全相符和大致相符來避免資料重複，藉此讓您移除重複的資料。 建議您先清理資料，然後再執行資料的比對。 若要這樣做：  
  
1.  建立資料品質專案、選取 **[清理]** 活動、針對來源資料完成資料清理活動，然後將資料匯出到 SQL Server 資料庫中的資料表。  
  
2.  使用包含比對原則的知識庫建立另一個資料品質專案、選取 **[比對]** 活動，然後在 **[對應]** 頁面上選取您在步驟 1 匯出之清理資料所在的資料庫和資料表。  
  
3.  針對清理的資料完成比對活動。  
  
 如需有關資料品質專案中比對活動的詳細資訊，請參閱＜ [Data Matching](../data-quality-services/data-matching.md)＞。  
  
##  <a name="ProfilingNotification"></a> 資料分析與通知  
 在資料品質專案中執行清理和比對活動之後，您可以看到有關 DQS 正在處理之資料的即時統計資料和資訊。 資料分析會幫助您評估清理和比對程序的效用，您也可以判斷資料清理或比對幫助提升資料品質的程度。 DQS 分析會提供兩個資料品質維度： *完整性* (資料存在的程度) 和 *精確度* (可將資料用於預定用途的程度)。 此外，根據資料分析資訊而定，為了增強資料清理與資料比對作業所採取之動作的相關通知會顯示給使用者。 如需有關資料分析和通知的詳細資訊，請參閱＜ [Data Profiling and Notifications in DQS](../data-quality-services/data-profiling-and-notifications-in-dqs.md)＞。  
  
## <a name="related-tasks"></a>相關工作  
  
|工作描述|主題|  
|----------------------|-----------|  
|描述如何建立資料品質專案。|[建立資料品質專案](../data-quality-services/create-a-data-quality-project.md)|  
|描述如何開啟、解除鎖定、重新命名和刪除資料品質專案。|[開啟、解除鎖定、重新命名和刪除資料品質專案](open-unlock-rename-and-delete-a-data-quality-project.md)|  
|描述如何在 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]中開啟 Integration Services 專案。|[在 Data Quality Client 中開啟 Integration Services 專案](../data-quality-services/open-integration-services-projects-in-data-quality-client.md)|  
  
## <a name="see-also"></a>另請參閱  
 [DQS 知識庫與網域](../data-quality-services/dqs-knowledge-bases-and-domains.md)  
  
  
