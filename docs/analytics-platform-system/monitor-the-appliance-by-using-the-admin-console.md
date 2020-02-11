---
title: 使用管理主控台進行監視
description: 對於分析平臺系統，管理主控台是一種 web 應用程式，可呈現設備狀態、健康情況和效能資訊。 使用者透過網際網路瀏覽器連接到管理主控台。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 977e38016fbb58356d22ccfc5f783539e5f852d5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "74400947"
---
# <a name="monitor-the-appliance-with-the-admin-console---analytics-platform-system"></a>使用管理主控台分析平臺系統來監視設備
管理主控台是一個 SQL Server PDW web 應用程式，可呈現設備狀態、健康情況和效能資訊。 使用者透過 Internet Explorer 連接到管理主控台。  
  
## <a name="About"></a>關於管理主控台  
![應用裝置主控台首頁](./media/monitor-the-appliance-by-using-the-admin-console/SQL_Server_PDW_AdminConsol_ApplHome.png "SQL_Server_PDW_AdminConsol_ApplHome")  
  
**台**  
首頁  
提供設備狀態的快速摘要。  
  
健康情況  
顯示裝置拓朴，其中包含指示器，顯示每個節點內每個受監視元件的健全狀況。 可讓您查看節點元件之個別節點和屬性的目前狀態。  
  
顯示硬體和軟體警示。  
  
效能監視器  
顯示效能監視器圖形。  
  
**平行處理資料倉儲**  
首頁  
提供 PDW 狀態的快速摘要。  
  
工作階段  
顯示作用中的 PDW 使用者會話。 這有助於監視資源爭用。  
  
查詢  
顯示執行中查詢和最近完成的查詢清單。 它會顯示相關的錯誤（如果有的話）。 也可讓您查看查詢執行計畫和節點執行資訊的詳細資料。  
  
載入  
顯示載入計畫、PDW 載入的目前狀態，以及相關的錯誤（如果有的話）。  
  
備份/還原  
顯示 PDW 備份和還原作業的記錄檔。  
  
健康情況  
顯示 PDW 拓撲，其中包含指示器，顯示每個節點內每個受監視元件的健全狀況。 可讓您查看節點元件之個別節點和屬性的目前狀態。  
  
顯示硬體和軟體警示。  
  
資源  
顯示 PDW 資源鎖定和其目前狀態的清單。  
  
儲存體  
摘要說明 PDW 儲存體使用率。  
  
效能監視器  
顯示 PDW 效能監視器圖形。  
 
> [!NOTE]  
> 管理主控台具有1024x768 的螢幕解析度。 系統管理主控台顯示的最佳螢幕解析度為 1280 X 1024 或更高。  
  
## <a name="Connect"></a>連接到管理主控台  
若要連接到管理主控台，需要：  
  
-   至少要有 Internet Explorer 第10版。  
  
-   存取管理主控台的許可權。 <!-- MISSING LINKS See [Grant Permissions to Use the Admin Console &#40;SQL Server PDW&#41;](../sqlpdw/grant-permissions-to-use-the-admin-console-sql-server-pdw.md).  -->  
  
-   控制節點叢集的 IP 位址。  從您的 SQL Server PDW 系統管理員取得此帳戶。  
  
若要連接到管理主控台，請使用 Internet Explorer 和 HTTPs 流覽至控制節點叢集的 IP 位址。 例如，如果控制節點叢集的 IP 位址是`10.192.63.102`，請在您的`https://10.192.63.102`瀏覽器網址列中輸入。 第一個畫面會要求您的**登**入和**密碼**。 提供 SQL Server Authentication 登入和密碼，或是 Windows 驗證登入和 Windows 密碼。 如果使用 Windows 驗證登入，管理主控台將會使用模擬。  
  
## <a name="RelatedTasks"></a>管理主控台工作  
管理主控台提供監視下列功能的能力：  
  
|||  
|-|-|  
|**資訊類型**|**如何在管理主控台中存取**|  
|設備的整體狀態|按一下頂端功能表中的 [**設備狀態**] 或 [**首頁**]。|  
|警示|按一下 [警示]****。 如需詳細資訊，請參閱[瞭解管理主控台警示 &#40;分析平臺系統&#41;](understanding-admin-console-alerts.md)。|  
|設備元件及其狀態|按一下頂端功能表中的 [**設備狀態**] 或 [**首頁**]。|  
|監視要求（包括查詢、載入、備份和還原）|按一下 [**會話**]，以查看目前作用中或最近的會話。<br /><br />按一下 [**查詢**]，以查看目前作用中或最近的查詢。 針對查詢所顯示的資訊包括載入、備份和還原。<br /><br />按一下 [**鎖定**] 以查看作用中鎖定。|  
|監視載入、備份和還原的其他資訊。|按一下 [**載入**] 或 [**備份/還原**]。|  
|效能資訊|按一下 [**效能監視器**]。|  
  
## <a name="see-also"></a>另請參閱  
[&#40;分析平臺系統&#41;的設備監視](appliance-monitoring.md)  
  
