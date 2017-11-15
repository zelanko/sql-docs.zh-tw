---
title: "DQS 管理 | Microsoft Docs"
ms.custom: 
ms.date: 10/01/2012
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: data-quality-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- dqs administration
- administration
- dqs,adminstration
ms.assetid: 9940ef5d-f6f6-4dec-9414-1077a4d7f12b
caps.latest.revision: "21"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 79d0d011909f4e368480efaabaa70322f2ceeb64
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="dqs-administration"></a>dqs 管理
  [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) 可讓您管理在 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)]上執行的各種 DQS 活動、設定與 DQS 活動相關的伺服器層級屬性、設定 Reference Data Service 設定，以及設定 DQS 記錄設定。 這些操作是透過 **中的** [管理] [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]功能完成。 根據您在 DQS 中的安全性存取權 (角色) 而定，您會被授與/拒絕對此區域中某些功能的存取。  
  
 除了這些管理活動之外，本主題也提供不使用 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]執行管理活動、備份與還原 DQS 資料庫的相關資訊。  
  
 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 中的管理功能具有下列優點：  
  
-   讓資料管理人從 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] 監控 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]上的各種 DQS 活動。  
  
-   讓 DQS 系統管理員從 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] 監控 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]上的 DQS 活動，並 *終止* 正在執行的活動或 *停止* 活動中正在執行的程序 (如有需要)。  
  
-   設定 Reference Data Service 設定 (例如設定與 Windows Azure Marketplace 的連線，以及管理協力廠商的直接參考資料服務提供者。  
  
-   設定清理與比對活動的臨界值。  
  
-   啟用/停用 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]中的通知。  
  
-   根據事件的嚴重性層級設定記錄。  
  
##  <a name="AdminUsingClent"></a> 使用 Data Quality Client 的管理活動  
 這些活動是使用 **中的** [管理] [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]功能所執行。  
  
### <a name="activity-monitoring"></a>活動監控  
 **中的** [活動監控] [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 畫面會顯示關於在 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)]上執行之每個活動的詳細資訊。 資料管理人主要使用這個畫面，對 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] 應用程式連接的 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 上執行的所有活動執行高階監視。 這個畫面不提供任何系統層級的監視。 此外，這個畫面也可以讓 DQS 系統管理員透過終止正在執行的活動或停止活動中正在執行的程序 (如有需要)，控制某個活動或某個活動中的程序。 系統會顯示知識探索、定義域管理、比對原則、清理、比對，以及 SQL Server Integration Services (SSIS) 式清理的資料。  
  
### <a name="configuration"></a>組態  
 **中的** [組態] [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 畫面可讓 DQS 系統管理員進行下列操作：  
  
-   **參考資料**：設定參考資料服務提供者：Windows Azure Marketplace 或直接參考資料提供者。 設定參考資料服務提供者之後，您可以在知識庫中的定義域管理活動期間，對應具有參考資料的定義域/複合定義域，然後使用相同的知識庫，在資料品質專案中進行清理活動。 它也可讓您指定連接網際網路所使用的 Proxy 設定，以使用 Windows Azure Marketplace。  
  
-   **一般設定**：指定資料清理和資料比對的臨界值，以及是否在 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]中啟用分析所使用的通知。 這些臨界值是由 DQS 在資料品質專案中，於電腦輔助的清理和比對活動期間所使用。  
  
-   **記錄設定**：DQS 中的記錄檔會記錄在 DQS 中執行的活動，因此在維護和疑難排解期間追蹤運作問題相當實用。 您可以篩選您要針對各種 DQS 功能 (定義域管理、知識探索、清理、比對以及 Reference Data Services) 記錄的訊息，也可以根據事件的嚴重性層級篩選 DQS 模組。  
  
> [!NOTE]  
>  **[組態]** 畫面僅適用於擁有 DQS_MAIN 資料庫之 dqs_administrator 角色的使用者。  
  
##  <a name="AdminOutsideClient"></a> Data Quality Client 外部的管理活動  
 在 Data Quality Client 外部執行的活動包括：  
  
-   **備份和還原 DQS 資料庫**：DQS 資料庫的備份和還原與任何 SQL Server 資料庫的備份和還原相同，但有專屬於 DQS 的一些考量。  
  
-   **卸離和附加 DQS 資料庫**：卸離和附加 DQS 資料庫的步驟與卸離和附加任何 SQL Server 資料庫相同，但有專屬於 DQS 的一些考量。  
  
 如需詳細資訊，請參閱＜ [Manage DQS Databases](../data-quality-services/manage-dqs-databases.md)＞。  
  
## <a name="related-tasks"></a>相關工作  
  
|工作描述|主題|  
|----------------------|-----------|  
|描述如何監控 DQS 中的活動。|[監控 DQS 活動](../data-quality-services/monitor-dqs-activities.md)|  
|描述如何在 DQS 中設定參考資料設定。|[設定 DQS 使用參考資料](../data-quality-services/configure-dqs-to-use-reference-data.md)|  
|描述如何設定清理與比對活動的臨界值。|[設定清理和比對的閾值](../data-quality-services/configure-threshold-values-for-cleansing-and-matching.md)|  
|描述如何啟用或停用 DQS 中的通知。|[啟用或停用 DQS 中的分析通知](../data-quality-services/enable-or-disable-profiling-notifications-in-dqs.md)|  
|描述如何根據事件的嚴重性層級設定 DQS 記錄。|[設定 DQS 記錄檔的嚴重性層級](../data-quality-services/configure-severity-levels-for-dqs-log-files.md)|  
|描述如何設定 DQS 記錄的進階設定。|[設定 DQS 記錄檔的進階設定](../data-quality-services/configure-advanced-settings-for-dqs-log-files.md)|  
|描述如何備份與還原 DQS 資料庫。|[備份與還原 DQS 資料庫](../data-quality-services/backing-up-and-restoring-dqs-databases.md)|  
|描述如何卸離及附加 DQS 資料庫。|[中斷連線和附加 DQS 資料庫](../data-quality-services/detaching-and-attaching-dqs-databases.md)|  
  
## <a name="see-also"></a>另請參閱  
 [DQS 中的 Reference Data Services](../data-quality-services/reference-data-services-in-dqs.md)   
 [管理 DQS 記錄檔](../data-quality-services/manage-dqs-log-files.md)   
 [管理 DQS 資料庫](../data-quality-services/manage-dqs-databases.md)  
  
  
