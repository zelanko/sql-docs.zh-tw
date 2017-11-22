---
title: "監視 (Analytics Platform System) 的應用裝置"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: sql-non-specified
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: analytics-platform-system
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/05/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 253864fb-9178-41d2-a0ae-5dd9fd0a4fda
caps.latest.revision: "25"
ms.openlocfilehash: dbbae960d5e4d88b6cb725c9e22fc36a428b9264
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="appliance-monitoring"></a>應用裝置監視
此應用裝置監視指南描述的工具和監視 SQL Server PDW 應用裝置的工作。  
  
## <a name="Basics"></a>監視的基本概念與工具  
和 SQL Server PDW 應用裝置上的，您可以監視資訊的值是廣泛。 例如，以下是典型監視工作。  
  
-   檢查有任何 SQL Server PDW 所發出的警示。  
  
-   監視發生錯誤的硬體。  
  
-   監視網路連線問題。  
  
-   請檢查查詢處理期間傳回給使用者的錯誤。  
  
-   檢視目前作用中工作階段和查詢的數目。  
  
-   檢查載入、 備份及還原狀態。  
  
### <a name="appliance-monitoring-tools"></a>監視工具的應用裝置  
有多個工具可以用來監視應用裝置。  
  
管理主控台  
SQL Server PDW 具有系統管理員主控台。 這是 web 型工具，顯示查詢、 載入、 備份和還原、 鎖定、 工作階段、 警示和應用裝置狀態相關資訊。 應用裝置; 上執行的系統管理員主控台使用者連線到系統管理員主控台，透過 Internet Explorer。 如需詳細資訊，請參閱：  
  
-   [使用系統管理員主控台 &#40; 監視的應用裝置Analytics Platform System &#41;](monitor-the-appliance-by-using-the-admin-console.md)  
  
![PDW 管理主控台警示](./media/appliance-monitoring/SQL_Server_PDW_AdminConsol_Queries.png "SQL_Server_PDW_AdminConsol_Queries")  
  
系統檢視表  
SQL Server PDW 包含完善的系統檢視，可讓您取得有關應用裝置的健全狀況、 狀態和效能的詳細的資訊。 如需監視工作的系統檢視表的清單，請參閱：  
  
-   [使用系統檢視 &#40; 監視的應用裝置Analytics Platform System &#41;](monitor-the-appliance-by-using-system-views.md)  
  
System Center Operations Manager (SCOM)  
SQL Server PDW 有大量與 Systems Center Operations Manager 的整合。 SQL Server PDW 的管理組件可免費下載。 如需有關如何使用 System Center 監視 SQL Server PDW 的詳細資訊，請參閱下列各項：  
  
-   [使用 System Center Operations Manager &#40; 監視的應用裝置Analytics Platform System &#41;](monitor-the-appliance-by-using-system-center-operations-manager.md)  
  
自訂解決方案  
情況下 System Center 無法使用時與您的資料中心監視工具，您可以監視應用裝置使用協力廠商的監視解決方案。 Pdw，目前不支援外部軟體代理程式安裝，但大部分監視解決方案支援 Transact-sql\-SQL 整合，讓系統管理員可以實作直接 Transact\-SQL 查詢，針對您 PDW應用裝置。  
  
如果您的監視解決方案不支援直接 Transact\-SQL 查詢，或您不需要是監視工具，則您可以使用指令碼來執行監視工作，例如發生警示時傳送電子郵件。  TechNet wiki 包含已編寫指令碼的監視解決方案範例。  
  
-   [監視 SQL Server PDW 範例 power Shell](http://go.microsoft.com/fwlink/?LinkId=248020)  
   
## <a name="Tasks"></a>相關監視工作  
  
|監視工作|Description|  
|-------------------|---------------|  
|使用系統管理員主控台監視應用裝置。|[使用系統管理員主控台 &#40; 監視的應用裝置Analytics Platform System &#41;](monitor-the-appliance-by-using-the-admin-console.md)|  
|使用系統檢視表，以監視應用裝置。|[使用系統檢視 &#40; 監視的應用裝置Analytics Platform System &#41;](monitor-the-appliance-by-using-system-views.md)|  
|使用 System Center 監視的應用裝置|[使用 System Center Operations Manager &#40; 監視的應用裝置Analytics Platform System &#41;](monitor-the-appliance-by-using-system-center-operations-manager.md)|  
|監視應用裝置的狀態。|[監視應用裝置健全狀況狀態 &#40;Analytics Platform System &#41;](monitor-appliance-health-state.md)|  
|活動訊號監視。|[將遙測意見傳送到 Microsoft &#40;SQL Server PDW &#41;](send-telemetry-feedback-to-microsoft-sql-server-pdw.md)|  
|追蹤應用裝置的警示。|[追蹤應用裝置警示 &#40;Analytics Platform System &#41;](track-appliance-alerts.md)|  
|判斷正在使用多少容量。|[檢視容量使用率 &#40;Analytics Platform System &#41;](view-capacity-utilization.md)|  
|決定頻率輪詢應用裝置。|[判斷輪詢頻率 &#40;Analytics Platform System &#41;](determine-polling-frequency.md)|  
|當叢集失敗發生時，判斷哪一個叢集節點失敗。|[判斷哪些叢集節點失敗 &#40;Analytics Platform System &#41;](determine-which-cluster-node-failed.md)|  


<!-- MISSING LINKS |Monitor loads.|[Monitor Loads &#40;SQL Server PDW&#41;](../sqlpdw/monitor-loads-sql-server-pdw.md)|  -->  
<!-- MISSING LINKS |Monitor backups and restores.|[Monitor Backups and Restores &#40;SQL Server PDW&#41;](../sqlpdw/monitor-backups-and-restores-sql-server-pdw.md)|  -->  
<!-- MISSING LINKS |Monitor the active queries.|[Monitoring Active Queries &#40;SQL Server PDW&#41;](../sqlpdw/monitoring-active-queries-sql-server-pdw.md)|  -->  
  
## <a name="see-also"></a>請參閱＜  
<!-- MISSING LINKS [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
[應用裝置管理工作 &#40;Analytics Platform System &#41;](appliance-management-tasks.md)  
  
