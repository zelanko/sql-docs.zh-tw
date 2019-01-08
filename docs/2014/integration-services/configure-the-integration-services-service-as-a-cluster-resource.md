---
title: 將 Integration Services 服務設定為叢集資源 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
ms.assetid: 367835aa-9855-4791-a989-b3d08402ad4c
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 0bd0382906d3ee56055cc026036816af64b55dc6
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/27/2018
ms.locfileid: "52408959"
---
# <a name="configure-the-integration-services-service-as-a-cluster-resource"></a>將 Integration Services 服務設定為叢集資源
  本節針對認為將 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服務設定為叢集資源的優點多於缺點的客戶，提供必要的設定指示。 不過， [!INCLUDE[msCoName](../includes/msconame-md.md)] 並不建議將 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服務設定為叢集資源。  
  
 如果要將 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服務設定為叢集資源，必須完成下列工作。  
  
-   在叢集上安裝 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 。  
  
     若要在叢集上安裝 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] ，您必須在叢集中的每個節點上安裝 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 。  
  
-   將 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 設定為叢集資源。  
  
     在叢集中的每個節點上安裝 Integration Services 之後，您需要將 Integration Services 設定為叢集資源。 將 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服務設定為叢集資源後，就可以將該服務加入至與 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]相同的資源群組，或加入不同的群組。 下表描述在選取資源群組時的可能優點和缺點。  
  
    |當 Integration Services 和 SQL Server 位於相同的資源群組|當 Integration Services 和 SQL Server 位於不同的資源群組|  
    |-----------------------------------------------------------------------------|-------------------------------------------------------------------------------|  
    |用戶端電腦可以使用 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 來管理儲存在 msdb 資料庫中的封裝，因為 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 和 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服務都是在相同的虛擬伺服器上執行。 這項設定可避免雙躍點狀況的委派問題。|用戶端電腦無法使用 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 來管理儲存在 msdb 資料庫中的封裝。 用戶端可以連接到 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服務執行所在的虛擬伺服器。 不過，該電腦無法將使用者的認證委派到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行所在的虛擬伺服器。 這稱為雙躍點狀況。|  
    |[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服務會與其他的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 服務競爭 CPU 和其他電腦資源。|[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服務不會與其他的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 服務競爭 CPU 和其他電腦資源，因為不同的資源群組是設定在不同的節點上。|  
    |封裝載入及儲存到 msdb 資料庫的速度會加快，產生的網路傳輸量也較少，因為兩種服務都是在相同電腦上執行。|封裝載入及儲存到 msdb 資料庫的速度可能會減慢，並產生較多的網路傳輸量。|  
    |兩種服務會同時上線或離線。|[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服務可能會在 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 離線時上線； 因此，儲存在 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] 的 msdb 資料庫中的封裝就無法使用。|  
    |必要的話，無法將 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服務快速地移至另一個節點。|必要的話，可以將 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服務快速地移至另一個節點。|  
  
     在決定將 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]加入至哪一個資源群組之後，就必須將 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 設定為該群組中的叢集資源。  
  
-   設定 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服務及封裝存放區。  
  
     將 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 設定為叢集資源之後，您必須在叢集中的每個節點上，修改 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服務組態檔的位置及內容。 在進行這些修改後，組態檔及封裝存放區就能在發生容錯移轉時供所有的節點使用。 在修改組態檔的位置及內容之後，必須將服務重新連線。  
  
-   將 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服務連線成叢集資源。  
  
 在叢集或任何伺服器上設定 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服務之後，您可能必須先設定 DCOM 權限，才能從用戶端電腦連接到該服務。 如需詳細資訊，請參閱[連接到遠端 Integration Services 伺服器 &#40;SSIS 服務&#41;](../../2014/integration-services/connect-to-a-remote-integration-services-server-ssis-service.md)。  
  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服務無法委派認證。 因此，當下列條件成立時，您無法使用 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] 來管理儲存在 msdb 資料庫中的封裝：  
  
-   [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服務和 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 正在不同的伺服器或虛擬伺服器上執行。  
  
-   正在執行 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 的用戶端是第三台電腦。  
  
 用戶端可以連接到 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服務執行所在的虛擬伺服器。 不過，該電腦無法將使用者的認證委派到 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 執行所在的虛擬伺服器。 這稱為雙躍點狀況。  
  
### <a name="to-install-integration-services-on-a-cluster"></a>在叢集上安裝 Integration Services  
  
1.  安裝和設定具有一個或多個節點的叢集。  
  
2.  (選擇性) 安裝叢集服務，例如 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]。  
  
3.  在叢集的每個節點上安裝 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 。  
  
### <a name="to-configure-integration-services-as-a-cluster-resource"></a>將 Integration Services 設定為叢集資源  
  
1.  開啟 [叢集管理員]。  
  
2.  在主控台樹狀目錄中，選取 [Groups] 資料夾。  
  
3.  在結果窗格中，選取您打算加入 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]的群組：  
  
    -   若要將 Integrations Services 當做叢集資源加入與 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]相同的資源群組，請選取 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 所屬的群組。  
  
    -   若要將 Integrations Services 當做叢集資源加入至與 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 不同的群組，請選取 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 所屬群組以外的群組。  
  
4.  在 [檔案] 功能表上，指向 [開新檔案]，然後按一下 [資源]。  
  
5.  在 [資源精靈] 的 [新資源] 頁面上鍵入名稱，然後選取 [一般服務] 作為 [服務類型]。 請不要變更 [群組] 的值。 按 [下一步] 。  
  
6.  在 [可能的擁有者] 頁面中，加入或移除作為資源之可能擁有者的叢集節點。 按 [下一步] 。  
  
7.  若要在 [相依性] 頁面上加入相依性，請選取 [可用的資源] 之下的資源，然後按一下 [加入]。 在容錯移轉時，[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 和儲存 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 封裝的共用磁碟會在 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 連線之前重新連線。 選取相依性之後，請按一下 [下一步]。  
  
     如需詳細資訊，請參閱[加入 SQL Server 資源的相依性](../sql-server/failover-clusters/windows/add-dependencies-to-a-sql-server-resource.md)。  
  
8.  在 [一般服務參數] 頁面上，輸入 **MsDtsServer** 作為服務的名稱。 按 [下一步] 。  
  
9. 在 [機碼複寫] 頁面上，按一下 [加入] 以加入用來識別 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服務組態檔位置的登錄機碼。 此檔案必須位在與 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服務相同的資源群組中的共用磁碟上。  
  
10. 在 [登錄機碼] 對話方塊中，輸入 **SOFTWARE\Microsoft\Microsoft SQL Server\100\SSIS\ServiceConfigFile**。 按一下 [確定]，然後按一下 [完成]。  
  
     [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服務現在已加入成叢集資源。  
  
### <a name="to-configure-the-integration-services-service-and-package-store"></a>設定 Integration Services 服務和封裝存放區  
  
1.  尋找位於 %ProgramFiles%\Microsoft SQL Server\100\DTS\Binn\MsDtsSrvr.ini.xml 的組態檔。 將該檔案複製到其中加入了 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服務的群組的共用磁碟。  
  
2.  在共用磁碟上，建立名為 **Packages** 的新資料夾作為封裝存放區。 請將新資料夾的「列出資料夾」和寫入權限授與適當的使用者和群組。  
  
3.  在共用磁碟上，在文字或 XML 編輯器中開啟組態檔。 將 `ServerName` 元素的值變更成位在相同資源群組中的虛擬 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 名稱。  
  
4.  值變更`StorePath`的完整路徑的項目**封裝**在上一個步驟中的共用磁碟上建立資料夾。  
  
5.  將登錄中的 **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\SSIS\ServiceConfigFile** 值，更新為共用磁碟上之服務組態檔的完整路徑和檔案名稱。  
  
### <a name="to-bring-the-integration-services-service-online"></a>將 Integration Services 服務連線  
  
-   請在 [叢集管理員] 中，選取 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服務並按一下滑鼠右鍵，然後從快顯功能表中選取 [上線]。 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 服務現在已連線成叢集資源。  
  
  
