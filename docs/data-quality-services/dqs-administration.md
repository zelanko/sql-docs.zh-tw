---
title: "DQS 管理 | Microsoft Docs"
ms.custom: ""
ms.date: "10/01/2012"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "data-quality-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "dqs 管理"
  - "管理"
  - "dqs, 管理"
ms.assetid: 9940ef5d-f6f6-4dec-9414-1077a4d7f12b
caps.latest.revision: 21
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 21
---
# DQS 管理
  [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) 可讓您管理和管理上所執行的各種 DQS 活動 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)], 、 設定與 DQS 活動相關的伺服器層級屬性，設定參考資料服務的設定，並設定 DQS 記錄設定。 這些項目都透過完成 **管理** 功能 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]。 根據您在 DQS 中的安全性存取權 (角色) 而定，您會被授與/拒絕對此區域中某些功能的存取。  
  
 除了這些管理活動之外，本主題也提供不使用 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 執行管理活動、備份與還原 DQS 資料庫的相關資訊。  
  
 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 中的管理功能具有下列優點：  
  
-   讓資料管理人從 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] 監控 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 上的各種 DQS 活動。  
  
-   讓 DQS 系統管理員監視上的 DQS 活動 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] 從 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)], ，和 *終止* 執行中的活動或 *停止* 在活動中，視需要執行的處理序。  
  
-   設定 Reference Data Service 設定 (例如設定與 Windows Azure Marketplace 的連線，以及管理協力廠商的直接參考資料服務提供者。  
  
-   設定清理與比對活動的臨界值。  
  
-   啟用/停用 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 中的通知。  
  
-   根據事件的嚴重性層級設定記錄。  
  
##  <a name="AdminUsingClent"></a> 使用 Data Quality Client 的管理活動  
 這些活動都是透過使用 **管理** 功能 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]。  
  
### 活動監控  
  **活動監控** 畫面 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 顯示對每個活動的詳細的資訊 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)]。 資料管理人主要使用這個畫面，對 [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] 應用程式連接的 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]上執行的所有活動執行高階監視。 這個畫面不提供任何系統層級的監視。 此外，這個畫面也可以讓 DQS 系統管理員透過終止正在執行的活動或停止活動中正在執行的程序 (如有需要)，控制某個活動或某個活動中的程序。 系統會顯示知識探索、定義域管理、比對原則、清理、比對，以及 SQL Server Integration Services (SSIS) 式清理的資料。  
  
### 組態  
  **組態** 畫面 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] DQS 系統管理員可以執行下列動作︰  
  
-   **參考資料**︰ 設定參考資料服務提供者︰ Windows Azure Marketplace 或直接參考資料服務提供者。 設定參考資料服務提供者之後，您可以在知識庫中的定義域管理活動期間，對應具有參考資料的定義域/複合定義域，然後使用相同的知識庫，在資料品質專案中進行清理活動。 它也可讓您指定連接網際網路所使用的 Proxy 設定，以使用 Windows Azure Marketplace。  
  
-   **一般設定**︰ 指定資料清理和資料比對，以及是否要啟用通知以進行分析的臨界值 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]。 這些臨界值是由 DQS 在資料品質專案中，於電腦輔助的清理和比對活動期間所使用。  
  
-   **記錄設定**: DQS 中的記錄檔記錄在 DQS 中執行的活動，而且可用於維護期間追蹤運作問題和疑難排解。 您可以篩選您要針對各種 DQS 功能 (定義域管理、知識探索、清理、比對以及 Reference Data Services) 記錄的訊息，也可以根據事件的嚴重性層級篩選 DQS 模組。  
  
> [!NOTE]  
>   **組態** 畫面是僅適用於擁有 DQS_MAIN 資料庫的 dqs_administrator 角色的使用者。  
  
##  <a name="AdminOutsideClient"></a> Data Quality Client 外部的管理活動  
 在 Data Quality Client 外部執行的活動包括：  
  
-   **備份與還原 DQS 資料庫**︰ 備份與還原 DQS 資料庫是相同的備份與還原任何 SQL Server 資料庫，有專屬於 DQS 的一些考量。  
  
-   **卸離和附加 DQS 資料庫**︰ 卸離和附加 DQS 資料庫的步驟是相同卸離和附加任何 SQL Server 資料庫，有專屬於 DQS 的一些考量。  
  
 如需詳細資訊，請參閱 [管理 DQS 資料庫](../data-quality-services/manage-dqs-databases.md)。  
  
## 相關工作  
  
|工作描述|主題|  
|----------------------|-----------|  
|描述如何監控 DQS 中的活動。|[Monitor DQS Activities](../data-quality-services/monitor-dqs-activities.md)|  
|描述如何在 DQS 中設定參考資料設定。|[Configure DQS to Use Reference Data](../data-quality-services/configure-dqs-to-use-reference-data.md)|  
|描述如何設定清理與比對活動的臨界值。|[Configure Threshold Values for Cleansing and Matching](../data-quality-services/configure-threshold-values-for-cleansing-and-matching.md)|  
|描述如何啟用或停用 DQS 中的通知。|[Enable or Disable Profiling Notifications in DQS](../data-quality-services/enable-or-disable-profiling-notifications-in-dqs.md)|  
|描述如何根據事件的嚴重性層級設定 DQS 記錄。|[Configure Severity Levels for DQS Log Files](../data-quality-services/configure-severity-levels-for-dqs-log-files.md)|  
|描述如何設定 DQS 記錄的進階設定。|[為 DQS 記錄檔設定進階設定](../data-quality-services/configure-advanced-settings-for-dqs-log-files.md)|  
|描述如何備份與還原 DQS 資料庫。|[備份及還原 DQS 資料庫](../data-quality-services/backing-up-and-restoring-dqs-databases.md)|  
|描述如何卸離及附加 DQS 資料庫。|[Detaching and Attaching DQS Databases](../data-quality-services/detaching-and-attaching-dqs-databases.md)|  
  
## 另請參閱  
 [DQS 中的 Reference Data Services](../data-quality-services/reference-data-services-in-dqs.md)   
 [管理 DQS 記錄檔](../data-quality-services/manage-dqs-log-files.md)   
 [管理 DQS 資料庫](../data-quality-services/manage-dqs-databases.md)  
  
  