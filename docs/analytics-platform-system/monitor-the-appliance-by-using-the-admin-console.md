---
title: "使用管理主控台 (Analytics Platform System) 監視的應用裝置"
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
ms.assetid: 294ba6ac-b1ff-46ea-ba32-d8b32cb4cdc2
caps.latest.revision: "26"
ms.openlocfilehash: c9a2d9e7191a1f362dfc998254f69a2a71e32aac
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="monitor-the-appliance-by-using-the-admin-console"></a>使用管理主控台來監視應用裝置
系統管理員主控台是 SQL Server PDW web 應用程式，可呈現的應用裝置狀態、 運行狀況和效能資訊。 使用者連線到系統管理員主控台，透過 Internet Explorer。  
  
## <a name="About"></a>關於系統管理員主控台  
![應用裝置主控台首頁](./media/monitor-the-appliance-by-using-the-admin-console/SQL_Server_PDW_AdminConsol_ApplHome.png "SQL_Server_PDW_AdminConsol_ApplHome")  
  
**應用裝置**  
主資料夾  
提供快速應用裝置狀態的摘要。  
  
健全狀況  
顯示應用裝置拓撲，以及指標，顯示每個節點內的每個受監視元件的健全狀況。 可讓您檢視個別節點的目前狀態和節點元件的屬性。  
  
顯示的硬體和軟體的警示。  
  
效能監視  
顯示效能監視器圖形。  
  
**平行處理資料倉儲**  
主資料夾  
提供快速的 PDW 狀態摘要。  
  
工作階段  
顯示作用中的 PDW 使用者工作階段。 這可協助監視資源爭用的情況。  
  
查詢  
顯示執行查詢和最近完成的查詢清單。 如果有的話，它會顯示相關的錯誤。 也提供功能，以檢視詳細資料的查詢執行計劃和節點執行資訊。  
  
載入  
顯示載入方案、 目前狀態的 PDW 載入和相關的錯誤，如果有的話。  
  
備份/還原  
顯示記錄檔的 PDW 備份和還原作業。  
  
健全狀況  
顯示 PDW 拓撲，以及指標，顯示每個節點內的每個受監視元件的健全狀況。 可讓您檢視個別節點的目前狀態和節點元件的屬性。  
  
顯示的硬體和軟體的警示。  
  
資源  
顯示 PDW 資源鎖定及其目前狀態的清單。  
  
儲存空間  
摘要說明的 PDW 儲存體使用量。  
  
效能監視  
顯示 PDW 效能監視器圖形。  
  
**HDInsight**  
主資料夾  
提供快速 HDInsight 狀態的摘要。  
  
HDFS  
摘要說明 HDInsight 空間使用量，並列出的前 10 個的空間取用者。  
  
對應/減少  
摘要說明 MapReduce 工作的狀態。  
  
健全狀況  
顯示 HDInsight 拓撲，以及指標，顯示每個節點內的每個受監視元件的健全狀況。 可讓您檢視個別節點的目前狀態和節點元件的屬性。  
  
顯示的硬體和軟體的警示。  
  
儲存空間  
摘要說明 HDInsight 儲存使用量。  
  
效能監視  
顯示效能監視器圖形。  
  
> [!NOTE]  
> 系統管理員主控台有 1024 x 768 螢幕解析度。 系統管理員主控台顯示最佳螢幕解析度是 1280 X 1024 或更高版本。  
  
## <a name="Connect"></a>連接到系統管理員主控台  
若要連接到系統管理員主控台中，需要：  
  
-   在最少 Internet Explorer 第 10 版。  
  
-   若要存取系統管理員主控台的權限。 <!-- MISSING LINKS See [Grant Permissions to Use the Admin Console &#40;SQL Server PDW&#41;](../sqlpdw/grant-permissions-to-use-the-admin-console-sql-server-pdw.md).  -->  
  
-   控制節點的叢集 IP 位址。  從您的 SQL Server PDW 系統管理員取得。  
  
若要連接到系統管理員主控台，使用 Internet Explorer 和 https 瀏覽至控制項節點叢集的 IP 位址。 例如，如果控制項節點叢集的 IP 位址是`10.192.63.102`，輸入`https://10.192.63.102`瀏覽器位址列中。 第一個畫面會要求您**登入**和**密碼**。 提供 SQL Server 驗證登入和密碼，或 Windows 驗證登入和 Windows 密碼。 如果使用 Windows 驗證登入，系統管理員主控台會使用模擬。  
  
## <a name="RelatedTasks"></a>系統管理員主控台工作  
系統管理員主控台提供了監視下列功能：  
  
|||  
|-|-|  
|**資訊類型**|**如何在管理主控台中存取**|  
|應用裝置的整體狀態|按一下**應用裝置狀態**中最上方的功能表或**首頁**。|  
|警示|按一下**警示**。 如需詳細資訊，請參閱[了解系統管理員主控台警示 &#40;Analytics Platform System &#41;](understanding-admin-console-alerts.md).|  
|應用裝置元件以及它們的狀態|按一下**應用裝置狀態**中最上方的功能表或**首頁**。|  
|（包括查詢、 載入、 備份和還原） 的監視要求|按一下**工作階段**若要查看目前作用中或新的工作階段。<br /><br />按一下**查詢**若要查看目前作用中或新的查詢。 顯示查詢的資訊包括載入、 備份和還原。<br /><br />按一下**鎖定**若要查看作用中的鎖定。|  
|監視負載、 備份和還原的其他資訊。|按一下**載入**或**備份/還原**。|  
|效能資訊|按一下**效能監視器**。|  
  
## <a name="see-also"></a>請參閱＜  
[應用裝置監視 &#40;Analytics Platform System &#41;](appliance-monitoring.md)  
  
