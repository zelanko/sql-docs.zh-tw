---
title: 電源或關閉-Analytics Platform System appliance |Microsoft Docs
description: Analytics Platform System 的電源設備開啟或關閉
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 994b0f94448b7fb7901734b2ae737e26be23900f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62678626"
---
# <a name="power-the-appliance-on-or-off-for-analytics-platform-system"></a>Analytics Platform System 的電源設備開啟或關閉
本主題描述如何開啟或關閉您的分析平台 Systemappliance 電源的電源在執行平行處理資料倉儲。 使用本主題當 Analytics Platform System appliance 移動時，或電源設備上嚴重的電源中斷後。  
  
開啟和關閉電源設備不是相同啟動及停止設備服務。 如需該主題的詳細資訊，請參閱[PDW 服務狀態&#40;Analytics Platform System&#41;](pdw-services-status.md)。 如需詳細資訊及支援開啟或關閉 SQL Server 2008 Parallel Data Warehouse，SQL Server 2008 Parallel Data Warehouse 說明檔。 如需詳細資訊及支援開啟或關閉 SQL Server 2012 AU1 或 AU2 平行處理資料倉儲，這些版本的說明檔。  
  
當這些指示指定連線到 SQL Server PDW 節點時，連接可以是本機使用連接的裝置 (KVM) 或使用遠端桌面的遠端。 某些動作必須是實體 （開啟電源開關），以及一些 （例如關機） 可以是實體，或使用 Windows 命令。  
  
SQL Server PDW 節點的連線，您可以使用指派給節點，或從 IP 位址進行**HST01**電腦使用其中一種**容錯移轉叢集管理員**(**cluadmin.msc**)或是**HYPER-V 管理員**(**virtmgmt.msc**) 應用程式，並以滑鼠右鍵按一下節點名稱。  
  
## <a name="PowerOff"></a>設備關閉電源  
  
### <a name="before-you-begin"></a>開始之前  
電源設備之外之前, 您應該結束應用裝置上的所有活動。 若要結束所有的活動：  
  
-   使用**工作階段**系統管理員主控台來識別目前的使用者 頁面。 請與他們連絡，並要求他們登出。  
  
-   如果需要您可以使用**KILL**陳述式，以強制終止用戶端連線。 刪除時請小心連接。 當中斷時，某些交易的處理程序，例如長時間執行的 update、 必須在 SQL Server 之前的復原活動可以完成復原的資料庫。 復原部分完成的更新或刪除，可能非常耗時。  
  
### <a name="to-power-off-the-appliance"></a>若要關閉應用裝置電源  
  
> [!WARNING]  
> 必須執行所有步驟中所列的正確順序，每個步驟之前必須完成下一個步驟會都執行，除非另有說明。 執行順序，或等待每個步驟，才能完成的步驟可能會導致錯誤時於稍後開啟該設備。  
  
1.  連接至 PDW 控制節點 (**_PDW_region_-CTL01** ) 並使用 Analytics Platform System appliance 網域系統管理員帳戶登入。  
  
2.  執行`C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100\dwconfig.exe`以開啟**Configuration Manager**。  
  
3.  在 組態管理員中下,**平行資料倉儲拓樸**功能表上，按一下**服務狀態**索引標籤，然後按一下**停止區域**停止 PDW 服務。   
  
4.  連接到 **_appliance_domain_-HST01**並使用設備網域系統管理員帳戶登入。  
  
5.  使用**容錯移轉叢集管理員**連接到 **_appliance_domain_-WFOHST01**叢集，如果不會自動連接，，然後在 [導覽] 窗格中，按一下**角色**。 在 **角色**窗格：  
  
    1.  多重選取所有虛擬機器。 按一下滑鼠右鍵，然後選取**關機**。  
  
    2.  等候完成關閉所有選取的 Vm。  
  
6.  關閉**容錯移轉叢集管理員**應用程式。  
  
7. 關機以外的所有伺服器 **_appliance_domain_-HST01**。  
  
8. 關閉 **_appliance_domain_-HST01**伺服器。  
  
9. 關閉電源分配單元 (Pdu)。  
  
## <a name="PowerOn"></a>在應用裝置上的電源  
  
### <a name="to-power-on-the-appliance"></a>應用裝置上的乘冪  
  
> [!WARNING]  
> 必須執行所有步驟中所列的正確順序，每個步驟之前必須完成下一個步驟會都執行，除非另有說明。 執行順序，或等待每個步驟，才能完成的步驟，可能會導致啟動錯誤。  
  
1.  開啟電源分配單元 (PDU)，並等候參數自動啟動。  
  
2.  開啟電源 **_appliance_domain_-HST01**伺服器。  
  
3.  登入 **_appliance_domain_-HST01**設備網域管理員的身分。  
  
4.  開始**HYPER-V 管理員**計劃 (**virtmgmt.msc**)，並連接到 **_appliance_domain_-HST01**如果未連接的預設值。  
  
    1.  如果您不能因為依照名稱連接 **_PDW_region_-AD01**是未執行，請嘗試使用的 IP 位址來連線。  
  
    2.  在 **虛擬機器**窗格中，找出 **_PDW_region_-AD01**並確認它正在執行。 如果沒有，啟動此 VM，並等候它完全啟動。  
  
5.  在其餘的設備中的伺服器上的電源。  
  
6.  當您於**HST01**設備網域系統管理員身分登入從**HYPER-V 管理員**:  
  
    1.  連接到 **_appliance_domain_-HST02**。  
  
    2.  在 **虛擬機器**窗格中，找出 **_PDW_region_-ad02 移**並確認它正在執行。  如果沒有，啟動此 VM，並等候它完全啟動。  
  
7.  使用**容錯移轉叢集管理員**連接到 **_appliance_domain_-WFOHST01**叢集，如果不會自動連接，然後再於**瀏覽** 窗格中，按一下**角色**。 在 **角色**窗格：  
  
    1.  多重選取的所有虛擬機器中，按一下滑鼠右鍵，然後**啟動**。  
  
    2.  等候完成再繼續進行下一個步驟中啟動所有選取的 Vm。  
  
    3.  如有必要容錯移轉的 vm，來關閉、 移動它們，然後重新啟動它們適當的主要主機上。  
  
8. 中斷**HST01**如果您想要。  
  
9. 連接到 **_PDW_region_-CTL01**使用設備網域系統管理員帳戶。  
  
10. 執行`C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100\dwconfig.exe`以啟動**Configuration Manager**。  
  
11. 在**Configuration Manager**，請在**平行資料倉儲拓樸**功能表上，按一下 **服務狀態**索引標籤，然後按一下 **啟動區域**啟動 PDW 服務。  
  
### <a name="to-verify-the-appliance-health"></a>若要確認應用裝置健全狀況  
在啟動設備之後，開啟**管理主控台**和檢查健全狀況 頁面，可能表示失敗狀況的警示。 如需詳細資訊，請參閱 <<c0> [ 使用管理主控台來監視設備&#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-the-admin-console.md)。</c0>  
  
## <a name="see-also"></a>另請參閱  
[設備管理工作&#40;Analytics Platform System&#41;](appliance-management-tasks.md)  
  
