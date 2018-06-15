---
title: 電源應用裝置開啟或關閉-Analytics Platform System |Microsoft 文件
description: 應用裝置開啟或關閉電源的 Analytics Platform System
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 54829190d03a889ade31383662bf192516934012
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/19/2018
ms.locfileid: "31538758"
---
# <a name="power-the-appliance-on-or-off-for-analytics-platform-system"></a>應用裝置開啟或關閉電源的 Analytics Platform System
本主題描述如何開啟電源，或您正在執行的平行處理資料倉儲，選擇性地執行 HDInsight 區域的分析平台 Systemappliance 關閉電源。 使用本主題當移動 Analytics Platform System 應用裝置時，或電源應用裝置上重大停電後。  
  
開啟和關閉電源設備不是與啟動和停止應用裝置服務相同。 該主題的資訊，請參閱[PDW 服務狀態&#40;Analytics Platform System&#41;](pdw-services-status.md)。 啟動或關閉 SQL Server 2008 Parallel Data Warehouse 的相關資訊，請參閱 SQL Server 2008 Parallel Data Warehouse 說明檔。 電源開啟或關閉 SQL Server 2012 AU1 或 AU2 Parallel Data Warehouse 的相關資訊，請參閱說明檔的版本。  
  
當這些指示指定連接到 SQL Server PDW 節點時，連接可以是本機使用附加的裝置 (KVM) 或遠端使用遠端桌面。 某些動作必須是實體 （開啟電源開關），以及部分 （例如關機） 可以是實體或使用 Windows 命令。  
  
無法建立連線到 SQL Server PDW 節點使用 IP 位址指派到節點，或從**HST01**電腦使用**容錯移轉叢集管理員**(**cluadmin.msc**)或**HYPER-V 管理員**(**virtmgmt.msc**) 應用程式，以滑鼠右鍵按一下節點名稱。  
  
## <a name="PowerOff"></a>關閉裝置電源  
  
### <a name="before-you-begin"></a>開始之前  
然後再關閉應用裝置，您應該結束應用裝置上的所有活動。 若要結束所有的活動：  
  
-   使用**工作階段**頁面來識別目前使用者的系統管理員主控台。 與他們連絡並要求他們登出。  
  
-   如果需要您可以使用**KILL**強制終止用戶端連接的陳述式。 當終止時請特別小心連接。 中斷時，某些交易的處理程序，例如長時間執行的更新，必須復原活動前 SQL Server 可以完成資料庫復原。 復原部分完成的更新或刪除，可能會很費時的作業。  
  
### <a name="to-power-off-the-appliance"></a>若要關閉裝置電源  
  
> [!WARNING]  
> 必須執行所有步驟的順序列出且每個步驟必須完成下一個步驟都執行之前，除非另有說明。 執行步驟順序，或不需等到完成每個步驟可以在開啟在稍後應用裝置電源總時導致錯誤。  
  
1.  連接至 PDW 控制節點 (***PDW_region *-CTL01** ) 並使用 Analytics Platform System 應用裝置的網域系統管理員帳戶登入。  
  
2.  執行`C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100\dwconfig.exe`開啟**Configuration Manager**。  
  
3.  在 組態管理員中下,**平行資料倉儲拓樸**功能表上，按一下 **服務狀態**索引標籤，然後按一下**停止區域**停止 PDW 服務。  
  
4.  如果有 HDInsight 區域，在**HDInsight 拓撲**功能表上，按一下 **服務狀態**索引標籤，然後按一下**停止區域**停止 HDInsight 服務。  
  
5.  連接到 ***appliance_domain *-HST01**並使用應用裝置的網域系統管理員帳戶登入。  
  
6.  使用**容錯移轉叢集管理員**連接至 ***appliance_domain *-WFOHST01**叢集，如果不會自動連接，，然後在瀏覽窗格中，按一下**角色**. 在**角色**窗格：  
  
    1.  多重選取所有的虛擬機器。 按一下滑鼠右鍵，然後選取**關機**。  
  
    2.  等候所有完成關閉選取的 Vm。  
  
7.  如果沒有 HDInsight 區域：  
  
    1.  連接到 HDInsight 叢集。 若要這樣做，以滑鼠右鍵按一下**容錯移轉叢集管理員**，選取**連線到叢集**，並指定 ***appliance_domain *-WFOHST02**叢集名稱。  
  
    2.  HDInsight 叢集，按一下 **角色**。 在**角色**窗格：  
  
        1.  多重選取的所有虛擬機器中，按一下滑鼠右鍵，然後選取**關機**。  
  
        2.  等候虛擬機器關機。  
  
8.  關閉**容錯移轉叢集管理員**應用程式。  
  
9. 關閉以外的所有伺服器 ***appliance_domain *-HST01**。  
  
10. 關閉 ***appliance_domain *-HST01**伺服器。  
  
11. 關閉電源分配單元 (Pdu)。  
  
## <a name="PowerOn"></a>應用裝置上的電源  
  
### <a name="to-power-on-the-appliance"></a>應用裝置上的乘冪  
  
> [!WARNING]  
> 必須執行所有步驟的順序列出且每個步驟必須完成下一個步驟都執行之前，除非另有說明。 執行順序，或不需等到完成每個步驟的步驟，可能會導致啟動錯誤。  
  
1.  電源電源分配單元 (PDU)，並等候參數的自動啟動。  
  
2.  電源 ***appliance_domain *-HST01**伺服器。  
  
3.  登入 ***appliance_domain *-HST01**應用裝置的網域系統管理員。  
  
4.  啟動**HYPER-V 管理員**程式 (**virtmgmt.msc**)，並連接到 ***appliance_domain *-HST01**如果沒有連線的預設值。  
  
    1.  如果您無法依名稱連接因為 ***PDW_region *-AD01**是未執行，請再次嘗試連線所使用的 IP 位址。  
  
    2.  在**虛擬機器** 窗格中，找出 ***PDW_region *-AD01**並確認它正在執行。 如果沒有，請啟動此 VM，然後等候它完全啟動。  
  
5.  其餘的應用裝置中的伺服器上的電源。  
  
6.  在**HST01**應用裝置，網域系統管理員身分登入從**HYPER-V 管理員**:  
  
    1.  連接到 ***appliance_domain *-HST02**。  
  
    2.  在**虛擬機器** 窗格中，找出 ***PDW_region *-ad02 移**並確認它正在執行。  如果沒有，請啟動此 VM，然後等候它完全啟動。  
  
7.  使用**容錯移轉叢集管理員**連接至 ***appliance_domain *-WFOHST01**叢集，如果不會自動連線，然後在**瀏覽** 窗格中，按一下**角色**。 在**角色**窗格：  
  
    1.  多重選取的所有虛擬機器中，按一下滑鼠右鍵，然後**啟動**。  
  
    2.  等候所有選取的 Vm，完成後再繼續下一個步驟所啟動。  
  
    3.  如有必要的容錯移轉的 Vm，關閉它們，移動它們，然後重新啟動它們適當的主要主機上。  
  
8.  如果應用裝置有 HDInsight 區域，連接到 HDInsight 叢集。 (若要這樣做，以滑鼠右鍵按一下**容錯移轉叢集管理員**，選取**連線到叢集**，並指定 ***appliance_domain *-WFOHST01**叢集名稱。)  
  
    1.  HDInsight 叢集，按一下 **角色**。 在**角色**窗格。  
  
        1.  多重選取的所有虛擬機器中，按一下滑鼠右鍵，然後選取**啟動**，  
  
        2.  等候所有選取的 Vm，完成後再繼續下一個步驟所啟動。  
  
        3.  如有必要的容錯移轉的 Vm，關閉它們，將它們移，重新啟動它們適當的主要主機上。  
  
9. 中斷**HST01**如果您想。  
  
10. 連接到 ***PDW_region *-CTL01**應用裝置的網域系統管理員帳戶。  
  
11. 執行`C:\Program Files\Microsoft SQL Server Parallel Data Warehouse\100\dwconfig.exe`啟動**Configuration Manager**。  
  
12. 在**Configuration Manager**，請在**平行資料倉儲拓樸**功能表上，按一下 **服務狀態**索引標籤，然後按一下**開始區域**啟動 PDW 服務。  
  
13. 如果裝置具有 HDInsight 區域，在 HDInsight 拓撲功能表中，按一下**服務狀態**索引標籤，然後按一下**開始區域**啟動 HDInsight 服務。  
  
### <a name="to-verify-the-appliance-health"></a>若要驗證的應用裝置健全狀況  
應用裝置啟動後，開啟**管理主控台**並檢查警示會指出失敗狀況的健全狀況 頁面。 如需詳細資訊，請參閱[使用管理主控台來監視設備&#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-the-admin-console.md)。  
  
## <a name="see-also"></a>另請參閱  
[應用裝置管理工作&#40;Analytics Platform System&#41;](appliance-management-tasks.md)  
  
