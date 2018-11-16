---
title: 設備監視-Analytics Platform System |Microsoft Docs
description: 此應用裝置的監視指南描述的工具和監視 Analytics Platform System appliance 的工作。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 100a587814e62a6455d25e78a3defca973f39bf6
ms.sourcegitcommit: 50b60ea99551b688caf0aa2d897029b95e5c01f3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/15/2018
ms.locfileid: "51696086"
---
# <a name="appliance-monitoring-for-analytics-platform-system"></a>設備監視 Analytics Platform System
此應用裝置的監視指南描述的工具和監視 Analytics Platform System appliance 的工作。  
  
## <a name="Basics"></a>監視的基本概念和工具  
和 SQL Server PDW 應用裝置上的，您可以監視資訊的值是廣泛。 例如，以下是典型的監視工作。  
  
-   檢查有任何 SQL Server PDW 所發出的警示。  
  
-   監視故障的硬體。  
  
-   監視網路連線問題。  
  
-   請檢查傳回給使用者，在查詢處理期間的錯誤。  
  
-   檢視目前使用中工作階段和查詢的數目。  
  
-   檢查載入、 備份及還原的狀態。  
  
### <a name="appliance-monitoring-tools"></a>設備監視工具  
有多個工具可用來監視設備。  
  
管理主控台  
SQL Server PDW 具有系統管理員主控台。 這是 web 型工具，顯示查詢、 載入、 備份和還原、 鎖定、 工作階段、 警示和應用裝置狀態的相關資訊。 設備; 上執行的系統管理員主控台使用者連線到透過 Internet Explorer 的系統管理員主控台。 如需詳細資訊，請參閱：  
  
-   [使用管理主控台來監視設備&#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-the-admin-console.md)  
  
![PDW 管理主控台警示](./media/appliance-monitoring/SQL_Server_PDW_AdminConsol_Queries.png "SQL_Server_PDW_AdminConsol_Queries")  
  
系統檢視表  
SQL Server PDW 包含完整的系統檢視，讓您取得設備健全狀況、 狀態和效能的詳細的資訊。 如需監視工作的系統檢視表的清單，請參閱：  
  
-   [使用系統檢視表來監視設備&#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-system-views.md)  
  
System Center Operations Manager (SCOM)  
SQL Server PDW 的 Systems Center Operations manager 的豐富整合。 SQL Server PDW 的管理組件可免費下載。 如需使用 System Center 來監視 SQL Server PDW 的詳細資訊，請參閱下列各項：  
  
-   [使用 System Center Operations Manager 監視設備&#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-system-center-operations-manager.md)  
  
自訂解決方案  
情況下當 System Center 是不與您的資料中心監視工具，您可以監視設備使用第三方監視解決方案。 在 PDW 中，目前不支援外部軟體代理程式的安裝，但大部分監視解決方案支援的 Transact\-SQL 整合，讓系統管理員可以實作直接 Transact\-PDW 的 SQL 查詢應用裝置。  
  
如果您的監視解決方案不支援直接 Transact\-SQL 查詢，或您不需要是監視工具，則您可以使用指令碼來執行監視工作，例如發生警示時傳送電子郵件。  TechNet wiki 中包含已編寫指令碼的監視解決方案範例。  
  
-   [適用於 SQL Server PDW 監控範例的 power Shell](https://go.microsoft.com/fwlink/?LinkId=248020)  
   
## <a name="Tasks"></a>相關監視工作  
  
|監視工作|描述|  
|-------------------|---------------|  
|使用管理主控台來監視設備。|[使用管理主控台來監視設備&#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-the-admin-console.md)|  
|使用系統檢視表來監視設備。|[使用系統檢視表來監視設備&#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-system-views.md)|  
|使用 System Center 來監視設備|[使用 System Center Operations Manager 監視設備&#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-system-center-operations-manager.md)|  
|監視設備的狀態。|[監視設備健全狀況狀態&#40;Analytics Platform System&#41;](monitor-appliance-health-state.md)|  
|活動訊號監視。|[將遙測意見反應傳送給 Microsoft &#40;SQL Server PDW&#41;](send-telemetry-feedback-to-microsoft-sql-server-pdw.md)|  
|追蹤設備警示。|[追蹤設備警示&#40;Analytics Platform System&#41;](track-appliance-alerts.md)|  
|判斷正在使用多少容量。|[檢視容量使用率&#40;Analytics Platform System&#41;](view-capacity-utilization.md)|  
|決定頻率輪詢應用裝置。|[判斷輪詢頻率&#40;Analytics Platform System&#41;](determine-polling-frequency.md)|  
|當叢集失敗發生時，判斷哪一個叢集節點失敗。|[判斷哪一個叢集節點失敗， &#40;Analytics Platform System&#41;](determine-which-cluster-node-failed.md)|  


<!-- MISSING LINKS |Monitor loads.|[Monitor Loads &#40;SQL Server PDW&#41;](../sqlpdw/monitor-loads-sql-server-pdw.md)|  -->  
<!-- MISSING LINKS |Monitor backups and restores.|[Monitor Backups and Restores &#40;SQL Server PDW&#41;](../sqlpdw/monitor-backups-and-restores-sql-server-pdw.md)|  -->  
<!-- MISSING LINKS |Monitor the active queries.|[Monitoring Active Queries &#40;SQL Server PDW&#41;](../sqlpdw/monitoring-active-queries-sql-server-pdw.md)|  -->  
  
## <a name="see-also"></a>另請參閱  
<!-- MISSING LINKS [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
[設備管理工作&#40;Analytics Platform System&#41;](appliance-management-tasks.md)  
  
