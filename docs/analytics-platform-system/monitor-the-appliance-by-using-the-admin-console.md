---
title: 以系統管理員主控台-分析平台系統監視 |Microsoft Docs
description: Analytics Platform System，系統管理員主控台是呈現應用裝置狀態、 健全狀況和效能資訊的 web 應用程式。 使用者連線到系統管理員主控台，透過網際網路瀏覽器。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: d094f809052222238806e679e38c6578422fd9aa
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63027535"
---
# <a name="monitor-the-appliance-with-the-admin-console---analytics-platform-system"></a>監視與系統管理員主控台-Analytics Platform System appliance
系統管理員主控台是呈現應用裝置狀態、 健全狀況和效能資訊的 SQL Server PDW web 應用程式。 使用者連線到透過 Internet Explorer 的系統管理員主控台。  
  
## <a name="About"></a>關於系統管理員主控台  
![應用裝置主控台首頁](./media/monitor-the-appliance-by-using-the-admin-console/SQL_Server_PDW_AdminConsol_ApplHome.png "SQL_Server_PDW_AdminConsol_ApplHome")  
  
**Appliance**  
主資料夾  
提供設備狀態的快速摘要。  
  
健全狀況  
顯示應用裝置拓撲，以顯示每個節點內的每個受監視元件的健全狀況的指標。 可讓您檢視個別節點的目前狀態和節點元件的屬性。  
  
顯示的硬體和軟體的警示。  
  
效能監視  
顯示 效能監視器圖形。  
  
**平行處理資料倉儲**  
主資料夾  
提供的 PDW 狀態的快速摘要。  
  
工作階段  
顯示作用中的 PDW 使用者工作階段。 這可協助監視資源爭用。  
  
查詢  
顯示執行的查詢和最近完成的查詢清單。 如果有的話，它就會顯示相關的錯誤。 也提供檢視的查詢執行計劃和節點執行資訊的詳細資料的能力。  
  
載入  
如果有的話，會顯示載入計劃、 PDW 負載，以及相關的錯誤，目前的狀態。  
  
Backups/Restores  
顯示記錄的 PDW 備份和還原作業。  
  
健全狀況  
顯示 PDW 拓撲，以顯示每個節點內的每個受監視元件的健全狀況的指標。 可讓您檢視個別節點的目前狀態和節點元件的屬性。  
  
顯示的硬體和軟體的警示。  
  
資源  
會顯示一份 PDW 資源鎖定和其目前的狀態。  
  
儲存體  
摘要說明的 PDW 儲存體使用率。  
  
效能監視  
顯示 PDW 效能監視器圖形。  
 
> [!NOTE]  
> 系統管理員主控台有 1024 x 768 螢幕解析度。 系統管理員主控台會顯示最佳螢幕解析度 1280 of 或更高版本。  
  
## <a name="Connect"></a>連接到系統管理員主控台  
若要連線到管理主控台中，需要：  
  
-   在最少 Internet Explorer 10 版。  
  
-   若要存取系統管理員主控台的權限。 <!-- MISSING LINKS See [Grant Permissions to Use the Admin Console &#40;SQL Server PDW&#41;](../sqlpdw/grant-permissions-to-use-the-admin-console-sql-server-pdw.md).  -->  
  
-   控制節點的叢集 IP 位址。  從您的 SQL Server PDW 系統管理員取得。  
  
若要連線至管理主控台，使用 Internet Explorer 和 https 瀏覽至叢集的控制節點的 IP 位址。 例如，如果是叢集的控制節點的 IP 位址`10.192.63.102`，輸入`https://10.192.63.102`瀏覽器位址列中。 第一個畫面會要求您**登入**並**密碼**。 提供可能是 SQL Server 驗證登入和密碼，或 Windows 驗證登入和 Windows 密碼。 如果使用 Windows 驗證登入，系統管理員主控台會使用模擬。  
  
## <a name="RelatedTasks"></a>系統管理員主控台工作  
系統管理員主控台提供了監視下列功能：  
  
|||  
|-|-|  
|**資訊類型**|**如何在管理主控台的存取**|  
|應用裝置的整體狀態|按一下 **設備狀態**在上方功能表中，或是**首頁**。|  
|警示|按一下 **警示**。 如需詳細資訊，請參閱 <<c0> [ 了解系統管理員主控台的警示&#40;Analytics Platform System&#41;](understanding-admin-console-alerts.md)。</c0>|  
|應用裝置元件和其狀態|按一下 **設備狀態**在上方功能表中，或是**首頁**。|  
|（包括查詢、 載入、 備份和還原） 的監視要求|按一下 **工作階段**若要查看目前作用中或最近的工作階段。<br /><br />按一下 **查詢**若要查看目前作用中或新的查詢。 顯示查詢的資訊包括載入、 備份和還原。<br /><br />按一下 **鎖定**若要查看作用中的鎖定。|  
|監視載入、 備份和還原的其他資訊。|按一下 **載入**或是**備份/還原**。|  
|效能資訊|按一下 **效能監視器**。|  
  
## <a name="see-also"></a>另請參閱  
[設備監視&#40;Analytics Platform System&#41;](appliance-monitoring.md)  
  
