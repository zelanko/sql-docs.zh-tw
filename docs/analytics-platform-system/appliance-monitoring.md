---
title: 設備監視
description: 此設備監視指南說明用來監視分析平臺系統裝置的工具和工作。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: cec604ff1a93213fc6308455cadda90e6efa2d61
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "74401418"
---
# <a name="appliance-monitoring-for-analytics-platform-system"></a>分析平臺系統的設備監視
此設備監視指南說明用來監視分析平臺系統裝置的工具和工作。  
  
## <a name="monitoring-basics-and-tools"></a><a name="Basics"></a>監視基本概念和工具  
可以在 SQL Server PDW 設備上監視的值和資訊很廣泛。 例如，下列是一般的監視工作。  
  
-   檢查 SQL Server PDW 發出的任何警示。  
  
-   監視失敗的硬體。  
  
-   監視網路連線問題。  
  
-   檢查查詢處理期間傳回給使用者的錯誤。  
  
-   查看目前使用中會話和查詢的數目。  
  
-   檢查負載、備份和還原的狀態。  
  
### <a name="appliance-monitoring-tools"></a>設備監視工具  
有多種工具可用來監視設備。  
  
管理主控台  
SQL Server PDW 具有管理主控台。 這是以 web 為基礎的工具，可顯示查詢、載入、備份和還原、鎖定、會話、警示和設備狀態的相關資訊。 管理主控台會在設備上執行;使用者透過 Internet Explorer 連接到管理主控台。 如需詳細資訊，請參閱：  
  
-   [使用管理主控台 &#40;分析平臺系統來監視設備&#41;](monitor-the-appliance-by-using-the-admin-console.md)  
  
![PDW 管理主控台警示](./media/appliance-monitoring/SQL_Server_PDW_AdminConsol_Queries.png "SQL_Server_PDW_AdminConsol_Queries")  
  
系統檢視表  
SQL Server PDW 包含完整的系統檢視，可讓您取得有關設備健全狀況、狀態和效能的詳細資訊。 如需監視工作的系統檢視清單，請參閱：  
  
-   [使用系統檢視 &#40;分析平臺系統來監視設備&#41;](monitor-the-appliance-by-using-system-views.md)  
  
System Center Operations Manager （SCOM）  
SQL Server PDW 與 Systems Center Operations Manager 有廣泛的整合。 SQL Server PDW 的管理元件可免費下載。 如需使用 System Center 監視 SQL Server PDW 的詳細資訊，請參閱下列各項：  
  
-   [使用 System Center Operations Manager &#40;分析平臺系統來監視設備&#41;](monitor-the-appliance-by-using-system-center-operations-manager.md)  
  
自訂解決方案  
在您的資料中心監視工具無法使用 System Center 的情況下，您可以使用協力廠商監視解決方案來監視設備。 PDW 目前不支援安裝外部軟體代理程式，但大部分的監視解決方案都支援 Transact-sql\-整合，因此系統管理員可以對您的 PDW 應用\-裝置執行直接的 transact-SQL 查詢。  
  
如果您的監視解決方案不支援直接 Transact-sql\-查詢，或您沒有監視工具，則可以使用腳本來執行監視工作，例如在發生警示時傳送電子郵件。  TechNet wiki 包含腳本的監視解決方案範例。  
  
-   [SQL Server PDW 的 Power Shell 監視範例](https://go.microsoft.com/fwlink/?LinkId=248020)  
   
## <a name="related-monitoring-tasks"></a><a name="Tasks"></a>相關監視工作  
  
|監視工作|描述|  
|-------------------|---------------|  
|使用管理主控台來監視設備。|[使用管理主控台 &#40;分析平臺系統來監視設備&#41;](monitor-the-appliance-by-using-the-admin-console.md)|  
|使用系統檢視來監視設備。|[使用系統檢視 &#40;分析平臺系統來監視設備&#41;](monitor-the-appliance-by-using-system-views.md)|  
|使用 System Center 監視設備|[使用 System Center Operations Manager &#40;分析平臺系統來監視設備&#41;](monitor-the-appliance-by-using-system-center-operations-manager.md)|  
|監視設備的狀態。|[監視設備健全狀況狀態 &#40;分析平臺系統&#41;](monitor-appliance-health-state.md)|  
|監視的信號。|[將遙測意見反應傳送給 Microsoft &#40;SQL Server PDW&#41;](send-telemetry-feedback-to-microsoft-sql-server-pdw.md)|  
|追蹤設備警示。|[&#40;分析平臺系統&#41;追蹤設備警示](track-appliance-alerts.md)|  
|判斷使用多少容量。|[查看 &#40;分析平臺系統&#41;的容量使用率](view-capacity-utilization.md)|  
|判斷輪詢設備的頻率。|[判斷 &#40;分析平臺系統&#41;的輪詢頻率](determine-polling-frequency.md)|  
|發生叢集失敗時，判斷哪個叢集節點失敗。|[判斷哪些叢集節點 &#40;分析平臺系統失敗&#41;](determine-which-cluster-node-failed.md)|  


<!-- MISSING LINKS |Monitor loads.|[Monitor Loads &#40;SQL Server PDW&#41;](../sqlpdw/monitor-loads-sql-server-pdw.md)|  -->  
<!-- MISSING LINKS |Monitor backups and restores.|[Monitor Backups and Restores &#40;SQL Server PDW&#41;](../sqlpdw/monitor-backups-and-restores-sql-server-pdw.md)|  -->  
<!-- MISSING LINKS |Monitor the active queries.|[Monitoring Active Queries &#40;SQL Server PDW&#41;](../sqlpdw/monitoring-active-queries-sql-server-pdw.md)|  -->  
  
## <a name="see-also"></a>另請參閱  
<!-- MISSING LINKS [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
[&#40;分析平臺系統&#41;的裝置管理工作](appliance-management-tasks.md)  
  
