---
title: 開啟或關閉設備電源
description: 為分析平臺系統開啟或關閉設備電源
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: ee70338b5a46ec60d808e489d982fd80692c5d1d
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/22/2019
ms.locfileid: "74400625"
---
# <a name="power-the-appliance-on-or-off-for-analytics-platform-system"></a>為分析平臺系統開啟或關閉設備電源
本主題說明如何開啟或關閉執行平行資料倉儲的分析平臺 Systemappliance 電源。 當分析平臺系統裝置已移動，或在發生重大電源中斷後，請使用此主題來開啟設備電源。  
  
開啟和關閉設備的電源與啟動和停止設備服務不同。 如需該主題的詳細資訊，請參閱[PDW 服務狀態 &#40;分析平臺系統&#41;](pdw-services-status.md)。 如需開啟或關閉 SQL Server 2008 平行處理資料倉儲的相關資訊，請參閱 SQL Server 2008 平行處理資料倉儲說明檔。 如需開啟或關閉 SQL Server 2012 AU1 或 AU2 平行處理資料倉儲的相關資訊，請參閱這些版本的說明檔。  
  
當這些指示指定連接到 SQL Server PDW 節點時，連接可以使用 [連接的裝置（KVM）] 或 [使用遠端桌面的遠端] 進行本機連線。 某些動作必須是實體（開啟電源開關），而有些則可以是實體或使用 Windows 命令。  
  
您可以使用指派給節點的 IP 位址，或從**HST01**電腦使用**容錯移轉叢集管理員**（**cluadmin.msc**）或**hyper-v 管理員**（**virtmgmt**）應用程式，並以滑鼠右鍵按一下節點名稱，來連接 SQL Server PDW 節點。  
  
## <a name="PowerOff"></a>關閉設備電源  
  
### <a name="before-you-begin"></a>開始之前  
在關閉設備電源之前，您應該先結束設備上的所有活動。 結束所有活動：  
  
-   使用管理主控台的 [**會話**] 頁面，即可識別目前的使用者。 請洽詢他們，並要求他們登出。  
  
-   如有需要，您可以使用**KILL**語句來強制終止用戶端連接。 終止連接時請小心。 當中斷時，某些交易處理常式（例如長時間執行的更新）必須先回復活動，SQL Server 才能完成資料庫的復原。 回復部分完成的更新或刪除，可能會很耗時。  
  
### <a name="to-power-off-the-appliance"></a>關閉設備電源  
  
> [!WARNING]  
> 所有步驟都必須按照列出的確切循序執行，而且每個步驟必須在執行下一個步驟之前完成，除非另有說明。 不按循序執行步驟或不等待每個步驟完成，可能會在應用裝置於稍後開機時導致錯誤。  
  
1.  連接至 PDW 控制節點（**_PDW_region_CTL01** ），並使用 Analytics Platform System 設備網域系統管理員帳戶登入。  
  
2.  執行`C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100\dwconfig.exe`以開啟**Configuration Manager**。  
  
3.  在 [Configuration Manager 的 [**平行處理資料倉儲拓撲**] 功能表底下，按一下 [**服務狀態**] 索引標籤，然後按一下 [**停止區域**] 以停止 PDW 服務。   
  
4.  連接到** _appliance_domain_HST01** ，並使用設備網域系統管理員帳戶登入。  
  
5.  使用**容錯移轉叢集管理員**連接至** _appliance_domain_WFOHST01**叢集（如果未自動連線），然後在流覽窗格中按一下 [**角色**]。 在 [**角色**] 窗格中：  
  
    1.  多重選取所有虛擬機器。 以滑鼠右鍵按一下它們，然後選取 [**關機**]。  
  
    2.  等候所有選取的 Vm 完成關機。  
  
6.  關閉**容錯移轉叢集管理員**應用程式。  
  
7. 關閉所有伺服器， ** _appliance_domain_-HST01**除外。  
  
8. 關閉** _appliance_domain_HST01**伺服器。  
  
9. 關閉電源配置單位（Pdu）。  
  
## <a name="PowerOn"></a>設備電源  
  
### <a name="to-power-on-the-appliance"></a>若要在設備上開啟電源  
  
> [!WARNING]  
> 所有步驟都必須按照列出的確切循序執行，而且每個步驟必須在執行下一個步驟之前完成，除非另有說明。 不按循序執行步驟或不等待每個步驟完成，可能會導致啟動錯誤。  
  
1.  開啟電源配置單位（PDU）的電源，並等候交換器自動啟動。  
  
2.  在** _appliance_domain_HST01**伺服器上開啟電源。  
  
3.  以設備網域系統管理員身分登入** _appliance_domain_HST01** 。  
  
4.  啟動**Hyper-v 管理員**程式（**virtmgmt**），並連接到** _appliance_domain_-HST01** （如果預設為未連線）。  
  
    1.  如果您因為** _PDW_region_-AD01**未執行而無法依名稱進行連線，請嘗試使用 IP 位址進行連接。  
  
    2.  在 [**虛擬機器**] 窗格中，找出** _PDW_region_-AD01**並確認它正在執行。 如果沒有，請啟動此 VM，並等候它完全啟動。  
  
5.  在設備中的其餘伺服器上開啟電源。  
  
6.  當**HST01**以設備網域系統管理員身分登入時，從 [ **hyper-v**管理員]：  
  
    1.  連接到** _appliance_domain_-HST02**。  
  
    2.  在 [**虛擬機器**] 窗格中，找出** _PDW_region_-AD02**並確認它正在執行。  如果沒有，請啟動此 VM，並等候它完全啟動。  
  
7.  使用**容錯移轉叢集管理員**連接至** _appliance_domain_WFOHST01**叢集（如果未自動連線），然後在**流覽**窗格中按一下 [**角色**]。 在 [**角色**] 窗格中：  
  
    1.  多重選取所有虛擬機器，以滑鼠右鍵按一下它們，然後按一下 [**啟動**]。  
  
    2.  等待所有選取的 Vm 完成啟動後，再繼續進行下一個步驟。  
  
    3.  如果 Vm 已容錯移轉，請將其關閉並加以移動，然後在適當的主要主機上重新開機它們。  
  
8. 如有需要，請中斷與**HST01**的連線。  
  
9. 使用設備網域系統管理員帳戶連接到** _PDW_region_CTL01** 。  
  
10. 執行`C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100\dwconfig.exe`以啟動**Configuration Manager**。  
  
11. 在**Configuration Manager**的 [平行處理**資料倉儲拓撲**] 功能表中，按一下 [**服務狀態**] 索引標籤，然後按一下 [**開始區域**] 以啟動 PDW 服務。  
  
### <a name="to-verify-the-appliance-health"></a>確認設備健全狀況  
設備啟動後，請開啟**管理主控台**，並查看 [健康情況] 頁面中可能指出失敗狀況的警示。 如需詳細資訊，請參閱[使用管理主控台監視設備 &#40;分析平臺系統&#41;](monitor-the-appliance-by-using-the-admin-console.md)。  
  
## <a name="see-also"></a>另請參閱  
[&#40;分析平臺系統&#41;的裝置管理工作](appliance-management-tasks.md)  
  
