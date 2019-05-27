---
title: 監視報表伺服器效能 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- performance counters [Reporting Services]
- report servers [Reporting Services], performance
- counters [Reporting Services]
- monitoring performance [Reporting Services]
- SQL Server Reporting Services, performance
- performance [Reporting Services]
- Reporting Services, performance
ms.assetid: c1bc13d4-8297-4daf-bb19-4c1e5ba292a6
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: f020dd812b53e531a3f4634ccba0d2cba980b89e
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/23/2019
ms.locfileid: "66103802"
---
# <a name="monitoring-report-server-performance"></a>監視報表伺服器效能
  使用效能監視工具來監視報表伺服器的效能，以評估伺服器活動、觀察趨勢、診斷系統瓶頸，以及收集可協助您判斷目前系統組態是否適當的資料。 若要微調伺服器效能，您可以指定回收報表伺服器應用程式定義域的頻率。 如需詳細資訊，請參閱 [設定報表伺服器應用程式的可用記憶體](../report-server/configure-available-memory-for-report-server-applications.md)。  
  
## <a name="sources-of-performance-data"></a>效能資料的來源  
 使用技術與工具的組合，取得有關系統如何執行的詳細資訊。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows Server 作業系統會透過下列工具提供效能資訊：  
  
-   工作管理員  
  
-   事件檢視器  
  
-   效能主控台  
  
 工作管理員提供有關在您電腦上執行之程式與處理序的資訊。 您可以使用工作管理員來監視報表伺服器效能的重要指標。 您也可以評估執行處理序的活動，以及檢視 CPU 和記憶體使用量的圖表與資料。 如需有關使用工作管理員的資訊，請參閱 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 產品文件集。  
  
 您可以使用效能主控台和事件檢視器來建立有關報表處理與資源耗用的記錄和警示。 如需 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]產生之 Windows 事件的資訊，請參閱 [Windows 應用程式記錄檔](windows-application-log.md)。 如需有關效能主控台的詳細資訊，請參閱本主題稍後的「Windows 效能計數器」。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公用程式也會提供用於快取和工作階段管理之報表伺服器資料庫與暫存資料庫的相關資訊。  
  
## <a name="windows-performance-counters"></a>Windows 效能計數器  
 監視特定的效能計數器可以讓您：  
  
-   估計支援預測之工作負載所需的系統需求。  
  
-   建立測量組態變更或應用程式升級之影響的效能基準線。  
  
-   監視在實際或人為產生之特定負載下的應用程式效能。  
  
-   確認硬體升級對效能的影響是正面的。  
  
-   驗證系統組態的變更對效能有正面的影響。  
  
## <a name="reporting-services-performance-objects"></a>Reporting Services 效能物件  
 [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] 包含下列效能物件：  
  
-   **MSRS 2011 Web Service**和`MSRS 2011 SharePoint Mode Web Service`來監視報表伺服器效能。 這些效能物件包含一組計數器集合，用來追蹤通常透過互動式報表檢視作業所起始的報表伺服器處理。 每當 [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 停止報表伺服器 Web 服務時，便會重設這些計數器。  
  
-   `MSRS 2011 Windows Service` 和 `MSRS 2011 Windows Service SharePoint Mode` 用於監視已排程的作業與報表傳遞。 這些效能物件包含一組計數器集合，用來追蹤透過已排程的作業所起始的報表處理。 已排程的作業包括訂閱與傳遞、報表執行快照集，以及報表記錄。  
  
-   `ReportServer:Service` 和 `ReportServerSharePoint:Service` 用於監視 HTTP 相關事件和記憶體管理。 這些計數器是 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]特有的，而且它們會追蹤報表伺服器的 HTTP 相關事件，例如要求、連接和登入嘗試。 這個效能物件也包含與記憶體管理相關的計數器。  
  
 如果您在單一電腦上有多個報表伺服器執行個體，則可以一起或分開監視這些執行個體。 加入計數器時，選擇要包含哪些執行個體。 如需使用效能主控台 (perfmon.msc) 與加入計數器的詳細資訊，請參閱 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 產品文件集。  
  
## <a name="other-performance-counters"></a>其他效能計數器  
 自訂 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 效能計數器只會提供給 `MSRS 2008 Web Service`、`MSRS 2008 Windows Service` 和 `ReportServer:Service` 使用。 下列效能物件會提供報表伺服器的其他效能監視資料。  
  
|效能物件|注意|  
|------------------------|-----------|  
|`.NET CLR Data` 和 `.NET CLR Memory`|報表管理員會使用 [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] 效能計數器。 如需詳細資訊，請參閱 MSDN 上的「Improving .NET Application Performance and Scalability」。|  
|`Process`|針對 ReportingServicesService 執行個體加入 `Elapsed Time` 和 `ID Process` 效能計數器，以便依據處理序識別碼追蹤處理序執行時間。|  
  
## <a name="sharepoint-events"></a>SharePoint 事件  
 除了 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 效能物件以外，如果您是以 SharePoint 整合模式執行報表伺服器，而且已經將報表環境設定成使用 SharePoint 產品，則可能也要設定 SharePoint 事件。 在本節中，如果您的報表環境已經與 SharePoint 整合，請使用「SharePoint 整合模式中報表伺服器的事件」來檢閱可能會提供有用資訊的診斷事件。  
  
## <a name="in-this-section"></a>本節內容  
 [MSRS 2014 Web 服務和 MSRS 2014 Windows 服務效能物件的效能計數器&#40;原生模式&#41;](performance-counters-msrs-2011-web-service-performance-objects.md)  
 描述報表伺服器 Web 服務所使用的效能計數器。  
  
 [MSRS 2014 Web 服務 SharePoint 模式和 MSRS 2014 Windows 服務 SharePoint 模式效能物件的效能計數器&#40;SharePoint 模式&#41;](performance-counters-msrs-2011-sharepoint-mode-performance-objects.md)  
 描述報表伺服器 Windows 服務所使用的效能計數器。  
  
 [ReportServer:Service 和 ReportServerSharePoint:Service 效能物件的效能計數器](performance-counters-reportserver-service-performance-objects.md)  
 描述 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]中的 HTTP 相關和記憶體相關效能計數器。  
  
 SharePoint 整合模式中報表伺服器的事件  
 描述當您執行含有 SharePoint 產品的報表環境時所要記錄的有用診斷事件。  
  
## <a name="see-also"></a>另請參閱  
 [設定報表伺服器應用程式的可用記憶體](../report-server/configure-available-memory-for-report-server-applications.md)   
 [Reporting Services 報表伺服器 &#40;原生模式&#41;](reporting-services-report-server-native-mode.md)   
 [Reporting Services 工具](../tools/reporting-services-tools.md)  
  
  
