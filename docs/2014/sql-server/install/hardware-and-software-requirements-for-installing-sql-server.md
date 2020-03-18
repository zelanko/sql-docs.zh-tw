---
title: SQL Server 2014：硬體 & 軟體需求
ms.custom: ''
ms.date: 07/10/2018
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- Setup [SQL Server], software
- software [SQL Server]
- installing SQL Server, software
- operating systems [SQL Server], SQL Server requirements
- Setup [SQL Server], cross-language support
- operating systems [SQL Server], cross-language support
- network connections [SQL Server], requirements
- disk space [SQL Server], SQL Server installations
- WOW [SQL Server]
- Setup [SQL Server], hardware
- dependencies [SQL Server], SQL Server installations
- cluster hardware requirements [SQL Server]
- endpoints [SQL Server], SQL Server installations
- Internet [SQL Server], SQL Server installations
- hardware [SQL Server]
- Windows on Windows [SQL Server]
- installing SQL Server, hardware
- Setup Configuration Checker
- SCC [SQL Server]
- operating systems [SQL Server]
- space [SQL Server], SQL Server installations
- system configuration checker
- installing SQL Server, cross-language support
- Internet [SQL Server]
- space [SQL Server]
- extended system support [SQL Server]
- 64-bit edition [SQL Server]
- failover clustering [SQL Server]
- failover clustering [SQL Server], hardware requirements
- 32-bit edition [SQL Server]
- locales [SQL Server], SQL Server installations
- cross-language support
- disk space [SQL Server]
- localized SQL Server versions
ms.assetid: 09bcf20b-0a40-4131-907f-b61479d5e4d8
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 664422d0875ade408e48166920852ee66162a885
ms.sourcegitcommit: 976a246a92bd6d1665882484a3f49a6d3edd2b8b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/17/2020
ms.locfileid: "79433815"
---
# <a name="sql-server-2014-hardware-and-software-requirements"></a>SQL Server 2014：硬體和軟體需求

 > - 藉由安裝**[免費的開發人員版本](https://my.visualstudio.com/Downloads?q=SQL%20Server%20Developer)來試用 SQL Server 2016！**  
  
## <a name="considerations"></a>考量 
  
-   建議您[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]在 NTFS 檔案格式的電腦上執行。 支援 FAT32 檔案系統，但不建議這麼做，因為它比 NTFS 檔案系統較不安全。  
  
-   您不能將安裝在唯讀、對應或壓縮的磁片磁碟機上。  
  
-   若要讓 Visual Studio 元件能夠正確安裝， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]您需要安裝更新。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]安裝程式會檢查此更新是否存在，然後需要您下載並安裝該更新，才能繼續進行[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]安裝。 為避免在安裝期間[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中斷，請在執行** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]安裝程式之前**下載並安裝更新，如下所述（或安裝 Windows Update 上提供的所有 .net 3.5 SP1 更新）：  
  
    -   針對[!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)] SP2，請在[這裡](https://go.microsoft.com/fwlink/?LinkId=198093)取得必要的更新。  
  
    -   若為任何其他支援的作業系統，則會包含此更新。  
  
-   不支援透過終端機服務用戶端啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式。 如果您透過終端機服務用戶端啟動安裝程式，安裝將會失敗。   
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式會安裝該產品所需的下列軟體元件：  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式支援檔案  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]如需在或[!INCLUDE[win8srv](../../includes/win8srv-md.md)] [!INCLUDE[win8](../../includes/win8-md.md)]上安裝的最低版本需求，請參閱[在 Windows Server 2012 或 windows 8 上安裝 SQL Server](https://support.microsoft.com/kb/2681562) （。https://support.microsoft.com/kb/2681562)  
  
 本主題包含下列幾節：  
  
-   [硬體和軟體需求](hardware-and-software-requirements-for-installing-sql-server.md#hwswr)  
  
-   [處理器、記憶體和作業系統需求](hardware-and-software-requirements-for-installing-sql-server.md#pmosr)  
  
-   [跨語言支援](hardware-and-software-requirements-for-installing-sql-server.md#CrossLanguageSupport)  
  
-   [擴充系統支援](hardware-and-software-requirements-for-installing-sql-server.md#ess)  
  
-   [磁碟空間需求 (32 位元和 64 位元)](hardware-and-software-requirements-for-installing-sql-server.md#HardDiskSpace)  
  
-   [資料檔案的儲存類型](hardware-and-software-requirements-for-installing-sql-server.md#StorageTypes)  
  
-   [在網域控制站上安裝 SQL Server](hardware-and-software-requirements-for-installing-sql-server.md#DC_support)  
  
##  <a name="hwswr"></a> 硬體及軟體需求  


本節中的表格列出執行 SQL Server 的最低需求。 此外，也有建議的設定選項以獲得[最佳效能](https://support.microsoft.com/help/2964518)。 

下列軟體需求適用于所有安裝：  

  
|元件|需求|  
|---------------|-----------------|  
|.NET Framework|.NET 3.5 SP1 是您選取 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]、 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]、Replication 或 [!INCLUDE[ssDQSnoversion](../../includes/ssdqsnoversion-md.md)]時 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]的需求，並且不再隨 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式安裝。 <br />-如果您執行安裝程式，但沒有 .NET 3.5 SP1， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]安裝程式會要求您先下載並安裝 .NET 3.5 sp1，才能繼續進行[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]安裝。 （從[Microsoft .NET Framework 3.5 Service Pack 1](https://www.microsoft.com/download/details.aspx?id=22)安裝 .NET 3.5 SP1）。錯誤訊息包含下載中心的連結，或者您可以從 Windows Update 下載 .NET 3.5 SP1。 若要避免 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝期間發生中斷，您可以先下載及安裝 .NET 3.5 SP1，再執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式。<br />-如果您在[!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 或[!INCLUDE[win8](../../includes/win8-md.md)]的電腦上執行安裝程式，則必須先啟用 .NET Framework 3.5 SP1， [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]然後再安裝。<br />-如果沒有網際網路存取，您必須先下載並安裝 .NET Framework 3.5 SP1，才能執行安裝程式以安裝上述任何元件。 如需有關如何[!INCLUDE[win8](../../includes/win8-md.md)]在和[!INCLUDE[win8srv](../../includes/win8srv-md.md)]上取得和啟用 .NET Framework 3.5 的建議和指導的詳細資訊，請參閱[Microsoft .NET Framework 3.5 部署考慮](https://msdn.microsoft.com/library/windows/hardware/hh975396)（https://msdn.microsoft.com/library/windows/hardware/hh975396)）。<br /><br /> 
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]需要 .NET 4.0。 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會在功能安裝步驟期間安裝 .NET 4.0。<br />-如果您要安裝[!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]版本，請確定電腦上有可用的網際網路連線。 由於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 媒體不包含 .NET Framework 4，因此 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 安裝程式會下載和安裝 .NET Framework 4。<br />-[!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]不會在[!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 或[!INCLUDE[win8srv](../../includes/win8srv-md.md)]的 Server Core 模式上安裝 .net 4.0。 您必須先安裝 .NET 4.0，才能在 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] SP1 或 [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] 的 Server Core 安裝上安裝 [!INCLUDE[win8srv](../../includes/win8srv-md.md)]。|  
|Windows PowerShell|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]不會安裝或啟用 Windows PowerShell 2.0;不過，Windows PowerShell 2.0 是元件和[!INCLUDE[ssDE](../../includes/ssde-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]的安裝必要條件。 如果安裝程式回報 Windows PowerShell 2.0 不存在，您可以遵循 [Windows Management Framework](https://go.microsoft.com/fwlink/?LinkId=186214) (機器翻譯) 頁面上的指示進行安裝或啟用。|  
|網路軟體|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 支援的作業系統有內建的網路軟體。 獨安裝立的具名執行個體和預設執行個體支援下列網路通訊協定：共用記憶體、具名管道、TCP/IP 和 VIA。<br /><br /> 注意：協定容錯移轉叢集不支援 VIA 通訊。 和 SQL Server 在相同容錯移轉叢集節點上執行的用戶端或應用程式，可以使用其本機管道位址以共用記憶體通訊協定連線到 SQL Server。 不過，此類型的連線不是叢集感知，且會在執行個體容錯移轉之後中斷。 因此不建議使用此連線，且只應該在非常特定的案例中使用。 VIA 通訊協定已被取代。 [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]<br /><br /> 如需有關網路通訊協定和網路程式庫的詳細資訊，請參閱＜ [Network Protocols and Network Libraries](network-protocols-and-network-libraries.md)＞。|  
|虛擬化|下列版本的 Hyper-V 角色上執行的虛擬機器環境支援 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]：<br />-<br />                    
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Standard、Enterprise 和 Datacenter 版本<br />-[!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)]SP1 Standard、Enterprise 和 Datacenter edition。<br />-<br />                    [!INCLUDE[win8srv](../../includes/win8srv-md.md)]Datacenter 和 Standard edition。<br /><br /> 除了父分割區所需的資源外，您也必須為其 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 執行個體的每部虛擬機器 (子分割) 提供足夠的處理器資源、記憶體和磁碟資源。 需求會於本主題稍後列出。\*<br /><br /> 在 [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 或 [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 上的 Hyper-V 角色內，最多可以將 4 (四) 個虛擬處理器配置給執行 [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 32 位元/64 位元或 [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 64 位元或 [!INCLUDE[win8srv](../../includes/win8srv-md.md)] 64 位元版本的虛擬機器。<br /><br /> 在上[!INCLUDE[win8srv](../../includes/win8srv-md.md)]的 hyper-v 角色內：<br />最多可以將 8 (八) 個虛擬處理器配置給執行 [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 32 位元/64 位元的虛擬機器。<br />最多可以將 64 (六十四) 個虛擬處理器配置給執行 [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 64 位元或 [!INCLUDE[win8srv](../../includes/win8srv-md.md)] 64 位元版本的虛擬機器。<br /><br /> 如需不同版本的[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]計算容量限制以及它們在具有超執行緒處理器的實體和虛擬化環境中有何差異的詳細資訊，請參閱[依版本 SQL Server 的計算容量限制](../compute-capacity-limits-by-edition-of-sql-server.md)。 如需有關 Hyper-V 角色的詳細資訊，請參閱＜ [Windows Server 2008 網站](https://go.microsoft.com/fwlink/?LinkId=182820)＞。<br /><br /> ** \* \*重要\*事項**支援來賓容錯移轉叢集[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。 如需有關支援 Guest 容錯移轉叢集的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和作業系統版本，以及虛擬化支援的詳細資訊，請參閱＜ [在硬體虛擬環境中執行之 Microsoft SQL Server 產品的支援原則](https://go.microsoft.com/fwlink/?LinkId=151676)＞。|  
|硬碟|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 需要至少 6 GB 的可用硬碟空間。<br /><br /> 磁碟空間需求會因為您安裝的 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 元件而有所不同。 如需詳細資訊，請參閱本主題稍後的＜ [Hard Disk Space Requirements (32-Bit and 64 Bit)](hardware-and-software-requirements-for-installing-sql-server.md#HardDiskSpace) ＞。 如需支援之資料檔案儲存類型的資訊，請參閱 [資料檔案的儲存類型](hardware-and-software-requirements-for-installing-sql-server.md#StorageTypes)。|  
|光碟機|若要從光碟片安裝，則需要 DVD 光碟機。|  
|監視|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 需要 Super-VGA (800x600) 或更高解析度的監視器。|  
|Internet|網際網路功能需要網際網路存取 (可能會另行收費)。|  
  
 * [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]在虛擬機器上執行的速度會比原生執行慢，因為虛擬化的額外負荷。  
  
##  <a name="pmosr"></a> 處理器、記憶體和作業系統需求  
 下列記憶體和處理器需求適用於所有版本的 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]：  
  
|元件|需求|  
|---------------|-----------------|  
|記憶體<sup>[1]</sup>|**最低規格：**<br /><br /> Express 版本：512 MB<br /><br /> 所有其他版本：1 GB<br /><br /> **建議配備：**<br /><br /> Express 版本：1 GB<br /><br /> 所有其他版本：至少 4 GB，並應隨著資料庫大小增加以確保最佳效能。|  
|處理器速度|**最低規格：**<br /><br /> x86 處理器：1.0 GHz<br /><br /> x64 處理器：1.4 GHz<br /><br /> **建議配備：** 2.0 GHz 或更快|  
|處理器類型|x64 處理器：AMD Opteron、AMD Athlon 64、具有 Intel EM64T 支援的 Intel Xeon、具有 EM64T 支援的 Intel Pentium IV<br /><br /> x86 處理器：Pentium III 相容處理器或更快的處理器|  
  
 <sup>[1]</sup>在（DQS）中[!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] [!INCLUDE[ssDQSnoversion](../../includes/ssdqsnoversion-md.md)]安裝元件所需的最小記憶體為 2 GB RAM，這與[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]最小記憶體需求不同。 如需有關安裝 DQS 的詳細資訊，請參閱＜ [Install Data Quality Services](../../data-quality-services/install-windows/install-data-quality-services.md)＞。  
  
 **WOW64 支援：**  
  
 WOW64 (Windows 64 位元上的 Windows 32 位元) 是 Windows 64 位元版本的一項功能，可讓 32 位元應用程式在 32 位元模式中以原生方式執行。 即使基礎作業系統是 64 位元的作業系統，應用程式仍可在 32 位元模式下運作。  
  
-   在支援的 64 位元作業系統上，可以將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 32 位元版安裝到 64 位元伺服器的 WOW64 32 位元子系統上。 只有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的獨立執行個體才支援 WOW64， 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 容錯移轉叢集安裝則不支援 WOW64。  
  
-   對於安裝在支援之 64 位元作業系統上的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 64 位元版本，WOW64 支援管理工具。 如需有關支援之作業系統的詳細資訊，請從下列區段選取 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 的版本。  
  
 **Server Core 支援：**  

 Windows Server 2008 R2、Windows Server 2012、Windows Server 2012 R2、Windows Server 2016 及 Windows Server 2019 的 Server Core 安裝現在支援 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。 

下列 Windows Server 版本支援在 Server Core 模式安裝 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]：

|                              |                                |
| :------------------------    | :------------------------------|
| Windows Server 2019 Standard | Windows Server 2019 Datacenter |
| Windows Server 2016 Standard | Windows Server 2016 Datacenter |
| Windows Server 2012 R2 Standard | Windows Server 2012 R2  Datacenter|
| Windows Server 2012 Standard | Windows Server 2012 Datacenter |
| Windows Server 2008 R2 SP1 Standard | Windows Server 2008 R2 SP1 Datacenter |
| Windows Server 2008 R2 SP1 Enterprise | Windows Server 2008 R2 SP1 Web|
   | &nbsp; | &nbsp; |
  
 如需有關在 Server [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] core 上安裝的詳細資訊，請參閱[在 Server core 上安裝 SQL Server 2014](../../database-engine/install-windows/install-sql-server-on-server-core.md)。  
  
   >[!NOTE]
   > [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]64位 x64 也支援[!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] 64 位 x64 Standard edition 所支援的版本。 [!INCLUDE[sbs_2](../../includes/sbs-2-md.md)]  
  
 **作業系統支援：**  
  
 
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 版本分類如下：  
  
-   [SQL Server 2014 的主要版本](hardware-and-software-requirements-for-installing-sql-server.md#TOP_Principal)  
  
-   [SQL Server 2014 的特殊版本](hardware-and-software-requirements-for-installing-sql-server.md#TOP_SP)  
  
-   [SQL Server 2014 的廣泛版本](hardware-and-software-requirements-for-installing-sql-server.md#TOP_Breadth)  
  
###  <a name="TOP_Principal"></a>主要版本作業系統需求  
 下表顯示 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]主要版本的作業系統需求：  
  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]公告|32 位元|64 位元|  
|---------------------------------------|-------------|-------------|  
|[!INCLUDE[ssEnterprise](../../includes/ssenterprise-md.md)]|[!INCLUDE[winserver2019_datacenter_md](../../includes/winserver2019-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2019_standard_md](../../includes/winserver2019-standard-md.md)]<br/><br/>[!INCLUDE[winserver2016_datacenter_md](../../includes/winserver2016-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2016_standard_md](../../includes/winserver2016-standard-md.md)]<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)]R2 Datacenter 64 位<br /><br /> [!INCLUDE[win8srv](../../includes/win8srv-md.md)]R2 Standard 64 位<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Essentials 64 位元<br /><br /> [!INCLUDE[win8srv](../../includes/win8srv-md.md)]R2 Foundation 64 位<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Datacenter 64 位元<br /><br /> [!INCLUDE[win8srv](../../includes/win8srv-md.md)]標準64位<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Essentials 64 位元<br /><br /> [!INCLUDE[win8srv](../../includes/win8srv-md.md)]Foundation 64 位<br /><br /> [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)]SP1 Datacenter 64 位<br /><br /> [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)]SP1 Enterprise 64 位<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Standard 64 位元<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Web 64 位元<br /><br /> [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)]SP2 Datacenter 64 位<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Enterprise 64 位元<br /><br /> [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)]SP2 Standard 64 位<br /><br /> [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)]SP2 Web 64 位<br /><br /> [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)]SP2 Datacenter 64 位<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Enterprise 32 位元<br /><br /> [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)]SP2 Standard 32 位<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Web 32 位元|[!INCLUDE[winserver2019_datacenter_md](../../includes/winserver2019-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2019_standard_md](../../includes/winserver2019-standard-md.md)]<br/><br/>[!INCLUDE[winserver2016_datacenter_md](../../includes/winserver2016-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2016_standard_md](../../includes/winserver2016-standard-md.md)]<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)]R2 Datacenter 64 位<br /><br /> [!INCLUDE[win8srv](../../includes/win8srv-md.md)]R2 Standard 64 位<br /><br /> [!INCLUDE[win8srv](../../includes/win8srv-md.md)]R2 Essentials 64 位<br /><br /> [!INCLUDE[win8srv](../../includes/win8srv-md.md)]R2 Foundation 64 位<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Datacenter 64 位元<br /><br /> [!INCLUDE[win8srv](../../includes/win8srv-md.md)]標準64位<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Essentials 64 位元<br /><br /> [!INCLUDE[win8srv](../../includes/win8srv-md.md)]Foundation 64 位<br /><br /> [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)]SP1 Datacenter 64 位<br /><br /> [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)]SP1 Enterprise 64 位<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Standard 64 位元<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Web 64 位元<br /><br /> [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)]SP2 Datacenter 64 位<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Enterprise 64 位元<br /><br /> [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)]SP2 Standard 64 位<br /><br /> [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)]SP2 Web 64 位|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Business Intelligence{2}|[!INCLUDE[winserver2019_datacenter_md](../../includes/winserver2019-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2019_standard_md](../../includes/winserver2019-standard-md.md)]<br/><br/>[!INCLUDE[winserver2016_datacenter_md](../../includes/winserver2016-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2016_standard_md](../../includes/winserver2016-standard-md.md)]<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)]R2 Datacenter 64 位<br /><br /> [!INCLUDE[win8srv](../../includes/win8srv-md.md)]R2 Standard 64 位<br /><br /> [!INCLUDE[win8srv](../../includes/win8srv-md.md)]R2 Essentials 64 位<br /><br /> [!INCLUDE[win8srv](../../includes/win8srv-md.md)]R2 Foundation 64 位<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Datacenter 64 位元<br /><br /> [!INCLUDE[win8srv](../../includes/win8srv-md.md)]標準64位<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Essentials 64 位元<br /><br /> [!INCLUDE[win8srv](../../includes/win8srv-md.md)]Foundation 64 位<br /><br /> [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)]SP1 Datacenter 64 位<br /><br /> [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)]SP1 Enterprise 64 位<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Standard 64 位元<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Web 64 位元<br /><br /> [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)]SP2 Datacenter 64 位<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Enterprise 64 位元<br /><br /> [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)]SP2 Standard 64 位<br /><br /> [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)]SP2 Web 64 位<br /><br /> [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)]SP2 Datacenter 64 位<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Enterprise 32 位元<br /><br /> [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)]SP2 Standard 32 位<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Web 32 位元|[!INCLUDE[winserver2019_datacenter_md](../../includes/winserver2019-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2019_standard_md](../../includes/winserver2019-standard-md.md)]<br/><br/>[!INCLUDE[winserver2016_datacenter_md](../../includes/winserver2016-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2016_standard_md](../../includes/winserver2016-standard-md.md)]<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)]R2 Datacenter 64 位<br /><br /> [!INCLUDE[win8srv](../../includes/win8srv-md.md)]R2 Standard 64 位<br /><br /> [!INCLUDE[win8srv](../../includes/win8srv-md.md)]R2 Essentials 64 位<br /><br /> [!INCLUDE[win8srv](../../includes/win8srv-md.md)]R2 Foundation 64 位<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Datacenter 64 位元<br /><br /> [!INCLUDE[win8srv](../../includes/win8srv-md.md)]標準64位<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Essentials 64 位元<br /><br /> [!INCLUDE[win8srv](../../includes/win8srv-md.md)]Foundation 64 位<br /><br /> [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)]SP1 Datacenter 64 位<br /><br /> [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)]SP1 Enterprise 64 位<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Standard 64 位元<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Web 64 位元<br /><br /> [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)]SP2 Datacenter 64 位<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Enterprise 64 位元<br /><br /> [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)]SP2 Standard 64 位<br /><br /> [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)]SP2 Web 64 位|  
|[!INCLUDE[ssStandard](../../includes/ssstandard-md.md)]|Windows 10 家用版 64 位元<br /><br /> Windows 10 專業版 64 位元<br /><br /> Windows 10 企業版 64 位元<br /><br /> Windows 10 家用版 32 位元<br /><br /> Windows 10 專業版 32 位元<br /><br /> Windows 10 企業版 32 位元<br /><br />[!INCLUDE[winserver2019_datacenter_md](../../includes/winserver2019-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2019_standard_md](../../includes/winserver2019-standard-md.md)]<br/><br/>[!INCLUDE[winserver2016_datacenter_md](../../includes/winserver2016-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2016_standard_md](../../includes/winserver2016-standard-md.md)]<br/><br/> [!INCLUDE[win8srv](../../includes/win8srv-md.md)]R2 Datacenter 64 位<br /><br /> [!INCLUDE[win8srv](../../includes/win8srv-md.md)]R2 Standard 64 位<br /><br /> [!INCLUDE[win8srv](../../includes/win8srv-md.md)]R2 Essentials 64 位<br /><br /> [!INCLUDE[win8srv](../../includes/win8srv-md.md)]R2 Foundation 64 位<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Datacenter 64 位元<br /><br /> [!INCLUDE[win8srv](../../includes/win8srv-md.md)]標準64位<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Essentials 64 位元<br /><br /> [!INCLUDE[win8srv](../../includes/win8srv-md.md)]Foundation 64 位<br /><br /> [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)]SP1 Datacenter 64 位<br /><br /> [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)]SP1 Enterprise 64 位<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Standard 64 位元<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Foundation 64 位元<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Web 64 位元<br /><br /> [!INCLUDE[winblue_client_2](../../includes/winblue-client-2-md.md)]32位<br /><br /> [!INCLUDE[winblue_client_pro_2](../../includes/winblue-client-pro-2-md.md)]32位<br /><br /> [!INCLUDE[winblue_client_ent_2](../../includes/winblue-client-ent-2-md.md)]32位<br /><br /> [!INCLUDE[winblue_client_2](../../includes/winblue-client-2-md.md)]64位<br /><br /> [!INCLUDE[winblue_client_pro_2](../../includes/winblue-client-pro-2-md.md)]64位<br /><br /> [!INCLUDE[winblue_client_ent_2](../../includes/winblue-client-ent-2-md.md)]64位<br /><br /> [!INCLUDE[win8](../../includes/win8-md.md)]32位<br /><br /> [!INCLUDE[win8_client_pro_2](../../includes/win8-client-pro-2-md.md)]32位<br /><br /> [!INCLUDE[win8_client_ent_2](../../includes/win8-client-ent-2-md.md)]32位<br /><br /> [!INCLUDE[win8](../../includes/win8-md.md)]64位<br /><br /> [!INCLUDE[win8_client_pro_2](../../includes/win8-client-pro-2-md.md)]64位<br /><br /> [!INCLUDE[win8_client_ent_2](../../includes/win8-client-ent-2-md.md)]64位<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 旗艦版 64 位元<br /><br /> [!INCLUDE[win7](../../includes/win7-md.md)]SP1 Enterprise 64 位<br /><br /> [!INCLUDE[win7](../../includes/win7-md.md)]SP1 Professional 64 位<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 旗艦版 32 位元<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 企業版 32 位元<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 專業版 32 位元<br /><br /> [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)]SP2 Datacenter 64 位<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Enterprise 64 位元<br /><br /> [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)]SP2 Standard 64 位<br /><br /> [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)]SP2 Foundation 64 位<br /><br /> [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)]SP2 Web 64 位<br /><br /> [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)]SP2 Datacenter 64 位<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Enterprise 32 位元<br /><br /> [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)]SP2 Standard 32 位<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Web 32 位元|Windows 10 家用版 64 位元<br /><br /> Windows 10 專業版 64 位元<br /><br /> Windows 10 企業版 64 位元<br /><br />[!INCLUDE[winserver2019_datacenter_md](../../includes/winserver2019-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2019_standard_md](../../includes/winserver2019-standard-md.md)]<br/><br/>[!INCLUDE[winserver2016_datacenter_md](../../includes/winserver2016-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2016_standard_md](../../includes/winserver2016-standard-md.md)]<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)]R2 Datacenter 64 位<br /><br /> [!INCLUDE[win8srv](../../includes/win8srv-md.md)]R2 Standard 64 位<br /><br /> [!INCLUDE[win8srv](../../includes/win8srv-md.md)]R2 Essentials 64 位<br /><br /> [!INCLUDE[win8srv](../../includes/win8srv-md.md)]R2 Foundation 64 位<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Datacenter 64 位元<br /><br /> [!INCLUDE[win8srv](../../includes/win8srv-md.md)]標準64位<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Essentials 64 位元<br /><br /> [!INCLUDE[win8srv](../../includes/win8srv-md.md)]Foundation 64 位<br /><br /> [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)]SP1 Datacenter 64 位<br /><br /> [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)]SP1 Enterprise 64 位<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Standard 64 位元<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Foundation 64 位元<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Web 64 位元<br /><br /> [!INCLUDE[winblue_client_2](../../includes/winblue-client-2-md.md)]64位<br /><br /> [!INCLUDE[winblue_client_pro_2](../../includes/winblue-client-pro-2-md.md)]64位<br /><br /> [!INCLUDE[winblue_client_ent_2](../../includes/winblue-client-ent-2-md.md)]64位<br /><br /> [!INCLUDE[win8](../../includes/win8-md.md)]64位<br /><br /> [!INCLUDE[win8_client_pro_2](../../includes/win8-client-pro-2-md.md)]64位<br /><br /> [!INCLUDE[win8_client_ent_2](../../includes/win8-client-ent-2-md.md)]64位<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 旗艦版 64 位元<br /><br /> [!INCLUDE[win7](../../includes/win7-md.md)]SP1 Enterprise 64 位<br /><br /> [!INCLUDE[win7](../../includes/win7-md.md)]SP1 Professional 64 位<br /><br /> [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)]SP2 Datacenter 64 位<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Enterprise 64 位元<br /><br /> [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)]SP2 Standard 64 位<br /><br /> [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)]SP2 Foundation 64 位<br /><br /> [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)]SP2 Web 64 位| 
  
###  <a name="TOP_SP"></a>特殊版本的作業系統需求  
 下表顯示 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]特殊版本的作業系統需求：  
  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]公告|32 位元|64 位元|  
|---------------------------------------|-------------|-------------|  
|[!INCLUDE[ssWeb](../../includes/ssweb-md.md)]|Windows 10 家用版 64 位元<br /><br /> Windows 10 專業版 64 位元<br /><br /> Windows 10 企業版 64 位元<br /><br /> Windows 10 家用版 32 位元<br /><br /> Windows 10 專業版 32 位元<br /><br /> Windows 10 企業版 32 位元<br /><br />[!INCLUDE[winserver2019_datacenter_md](../../includes/winserver2019-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2019_standard_md](../../includes/winserver2019-standard-md.md)]<br/><br/>[!INCLUDE[winserver2016_datacenter_md](../../includes/winserver2016-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2016_standard_md](../../includes/winserver2016-standard-md.md)]<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)]R2 Datacenter 64 位<br /><br /> [!INCLUDE[win8srv](../../includes/win8srv-md.md)]R2 Standard 64 位<br /><br /> [!INCLUDE[win8srv](../../includes/win8srv-md.md)]R2 Essentials 64 位<br /><br /> [!INCLUDE[win8srv](../../includes/win8srv-md.md)]R2 Foundation 64 位<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Datacenter 64 位元<br /><br /> [!INCLUDE[win8srv](../../includes/win8srv-md.md)]標準64位<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Essentials 64 位元<br /><br /> [!INCLUDE[win8srv](../../includes/win8srv-md.md)]Foundation 64 位<br /><br /> [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)]SP1 Datacenter 64 位<br /><br /> [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)]SP1 Enterprise 64 位<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Standard 64 位元<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Web 64 位元<br /><br /> [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)]SP2 Datacenter 64 位<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Enterprise 64 位元<br /><br /> [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)]SP2 Standard 64 位<br /><br /> [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)]SP2 Web 64 位<br /><br /> [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)]SP2 Datacenter 64 位<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Enterprise 32 位元<br /><br /> [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)]SP2 Standard 32 位<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Web 32 位元|Windows 10 家用版 64 位元<br /><br /> Windows 10 專業版 64 位元<br /><br /> Windows 10 企業版 64 位元<br /><br />[!INCLUDE[winserver2019_datacenter_md](../../includes/winserver2019-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2019_standard_md](../../includes/winserver2019-standard-md.md)]<br/><br/>[!INCLUDE[winserver2016_datacenter_md](../../includes/winserver2016-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2016_standard_md](../../includes/winserver2016-standard-md.md)]<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)]R2 Datacenter 64 位<br /><br />[!INCLUDE[win8srv](../../includes/win8srv-md.md)]R2 Standard 64 位<br /><br /> [!INCLUDE[win8srv](../../includes/win8srv-md.md)]R2 Essentials 64 位<br /><br /> [!INCLUDE[win8srv](../../includes/win8srv-md.md)]R2 Foundation 64 位<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Datacenter 64 位元<br /><br /> [!INCLUDE[win8srv](../../includes/win8srv-md.md)]標準64位<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Essentials 64 位元<br /><br /> [!INCLUDE[win8srv](../../includes/win8srv-md.md)]Foundation 64 位<br /><br /> [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)]SP1 Datacenter 64 位<br /><br /> [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)]SP1 Enterprise 64 位<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Standard 64 位元<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Web 64 位元<br /><br /> [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)]SP2 Datacenter 64 位<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Enterprise 64 位元<br /><br /> [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)]SP2 Standard 64 位<br /><br /> [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)]SP2 Web 64 位| 
  
###  <a name="TOP_Breadth"></a>廣度版本的作業系統需求
 下表顯示 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]廣泛版本的作業系統需求：  
  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]公告|32 位元|64 位元|  
|---------------------------------------|-------------|-------------|  
|[!INCLUDE[ssDeveloper](../../includes/ssdeveloper-md.md)]|Windows 10 家用版 64 位元<br /><br /> Windows 10 專業版 64 位元<br /><br /> Windows 10 企業版 64 位元<br /><br /> Windows 10 家用版 32 位元<br /><br /> Windows 10 專業版 32 位元<br /><br /> Windows 10 企業版 32 位元<br /><br />[!INCLUDE[winserver2019_datacenter_md](../../includes/winserver2019-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2019_standard_md](../../includes/winserver2019-standard-md.md)]<br/><br/>[!INCLUDE[winserver2016_datacenter_md](../../includes/winserver2016-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2016_standard_md](../../includes/winserver2016-standard-md.md)]<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)]R2 Datacenter 64 位<br /><br />[!INCLUDE[win8srv](../../includes/win8srv-md.md)]R2 Standard 64 位<br /><br /> [!INCLUDE[win8srv](../../includes/win8srv-md.md)]R2 Essentials 64 位<br /><br /> [!INCLUDE[win8srv](../../includes/win8srv-md.md)]R2 Foundation 64 位<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Datacenter 64 位元<br /><br /> [!INCLUDE[win8srv](../../includes/win8srv-md.md)]標準64位<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Essentials 64 位元<br /><br /> [!INCLUDE[win8srv](../../includes/win8srv-md.md)]Foundation 64 位<br /><br /> [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)]SP1 Datacenter 64 位<br /><br /> [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)]SP1 Enterprise 64 位<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Standard 64 位元<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Web 64 位元<br /><br /> [!INCLUDE[winblue_client_2](../../includes/winblue-client-2-md.md)]32位<br /><br /> [!INCLUDE[winblue_client_pro_2](../../includes/winblue-client-pro-2-md.md)]32位<br /><br /> [!INCLUDE[winblue_client_ent_2](../../includes/winblue-client-ent-2-md.md)]32位<br /><br /> [!INCLUDE[winblue_client_2](../../includes/winblue-client-2-md.md)]64位<br /><br /> [!INCLUDE[winblue_client_pro_2](../../includes/winblue-client-pro-2-md.md)]64位<br /><br /> [!INCLUDE[winblue_client_ent_2](../../includes/winblue-client-ent-2-md.md)]64位<br /><br /> [!INCLUDE[win8](../../includes/win8-md.md)]32位<br /><br /> [!INCLUDE[win8_client_pro_2](../../includes/win8-client-pro-2-md.md)]32位<br /><br /> [!INCLUDE[win8_client_ent_2](../../includes/win8-client-ent-2-md.md)]32位<br /><br /> [!INCLUDE[win8](../../includes/win8-md.md)]64位<br /><br /> [!INCLUDE[win8_client_pro_2](../../includes/win8-client-pro-2-md.md)]64位<br /><br /> [!INCLUDE[win8_client_ent_2](../../includes/win8-client-ent-2-md.md)]64位<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 旗艦版 64 位元<br /><br /> [!INCLUDE[win7](../../includes/win7-md.md)]SP1 Enterprise 64 位<br /><br /> [!INCLUDE[win7](../../includes/win7-md.md)]SP1 Professional 64 位<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 家用進階版 64 位元<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 家用入門版 64 位元<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 旗艦版 32 位元<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 企業版 32 位元<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 專業版 32 位元<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 家用進階版 32 位元<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 家用入門版 32 位元<br /><br /> [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)]SP2 Datacenter 64 位<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Enterprise 64 位元<br /><br /> [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)]SP2 Standard 64 位<br /><br /> [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)]SP2 Web 64 位<br /><br /> [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)]SP2 Datacenter 64 位<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Enterprise 32 位元<br /><br /> [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)]SP2 Standard 32 位<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Web 32 位元|Windows 10 家用版 64 位元<br /><br /> Windows 10 專業版 64 位元<br /><br /> Windows 10 企業版 64 位元<br /><br />[!INCLUDE[winserver2019_datacenter_md](../../includes/winserver2019-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2019_standard_md](../../includes/winserver2019-standard-md.md)]<br/><br/>[!INCLUDE[winserver2016_datacenter_md](../../includes/winserver2016-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2016_standard_md](../../includes/winserver2016-standard-md.md)]<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)]R2 Datacenter 64 位<br /><br />[!INCLUDE[win8srv](../../includes/win8srv-md.md)]R2 Standard 64 位<br /><br /> [!INCLUDE[win8srv](../../includes/win8srv-md.md)]R2 Essentials 64 位<br /><br /> [!INCLUDE[win8srv](../../includes/win8srv-md.md)]R2 Foundation 64 位<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Datacenter 64 位元<br /><br /> [!INCLUDE[win8srv](../../includes/win8srv-md.md)]標準64位<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Essentials 64 位元<br /><br /> [!INCLUDE[win8srv](../../includes/win8srv-md.md)]Foundation 64 位<br /><br /> [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)]SP1 Datacenter 64 位<br /><br /> [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)]SP1 Enterprise 64 位<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Standard 64 位元<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Web 64 位元<br /><br /> [!INCLUDE[winblue_client_2](../../includes/winblue-client-2-md.md)]64位<br /><br /> [!INCLUDE[winblue_client_pro_2](../../includes/winblue-client-pro-2-md.md)]64位<br /><br /> [!INCLUDE[winblue_client_ent_2](../../includes/winblue-client-ent-2-md.md)]64位<br /><br /> [!INCLUDE[win8](../../includes/win8-md.md)]64位<br /><br /> [!INCLUDE[win8_client_pro_2](../../includes/win8-client-pro-2-md.md)]64位<br /><br /> [!INCLUDE[win8_client_ent_2](../../includes/win8-client-ent-2-md.md)]64位<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 旗艦版 64 位元<br /><br /> [!INCLUDE[win7](../../includes/win7-md.md)]SP1 Enterprise 64 位<br /><br /> [!INCLUDE[win7](../../includes/win7-md.md)]SP1 Professional 64 位<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 家用進階版 64 位元<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 家用入門版 64 位元<br /><br /> [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)]SP2 Datacenter 64 位<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Enterprise 64 位元<br /><br /> [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)]SP2 Standard 64 位<br /><br /> [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)]SP2 Web 64 位|  
|[!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]|Windows 10 家用版 64 位元<br /><br /> Windows 10 專業版 64 位元<br /><br /> Windows 10 企業版 64 位元<br /><br /> Windows 10 家用版 32 位元<br /><br /> Windows 10 專業版 32 位元<br /><br /> Windows 10 企業版 32 位元<br /><br />[!INCLUDE[winserver2019_datacenter_md](../../includes/winserver2019-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2019_standard_md](../../includes/winserver2019-standard-md.md)]<br/><br/>[!INCLUDE[winserver2016_datacenter_md](../../includes/winserver2016-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2016_standard_md](../../includes/winserver2016-standard-md.md)]<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)]R2 Datacenter 64 位<br /><br /> [!INCLUDE[win8srv](../../includes/win8srv-md.md)]R2 Standard 64 位<br /><br /> [!INCLUDE[win8srv](../../includes/win8srv-md.md)]R2 Essentials 64 位<br /><br /> [!INCLUDE[win8srv](../../includes/win8srv-md.md)]R2 Foundation 64 位<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Datacenter 64 位元<br /><br /> [!INCLUDE[win8srv](../../includes/win8srv-md.md)]標準64位<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Essentials 64 位元<br /><br /> [!INCLUDE[win8srv](../../includes/win8srv-md.md)]Foundation 64 位<br /><br /> [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)]SP1 Datacenter 64 位<br /><br /> [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)]SP1 Enterprise 64 位<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Standard 64 位元<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Foundation 64 位元<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Web 64 位元<br /><br /> [!INCLUDE[winblue_client_2](../../includes/winblue-client-2-md.md)]32位<br /><br /> [!INCLUDE[winblue_client_pro_2](../../includes/winblue-client-pro-2-md.md)]32位<br /><br /> [!INCLUDE[winblue_client_ent_2](../../includes/winblue-client-ent-2-md.md)]32位<br /><br /> [!INCLUDE[winblue_client_2](../../includes/winblue-client-2-md.md)]64位<br /><br /> [!INCLUDE[winblue_client_pro_2](../../includes/winblue-client-pro-2-md.md)]64位<br /><br /> [!INCLUDE[winblue_client_ent_2](../../includes/winblue-client-ent-2-md.md)]64位<br /><br /> [!INCLUDE[win8](../../includes/win8-md.md)]32位<br /><br /> [!INCLUDE[win8_client_pro_2](../../includes/win8-client-pro-2-md.md)]32位<br /><br /> [!INCLUDE[win8_client_ent_2](../../includes/win8-client-ent-2-md.md)]32位<br /><br /> [!INCLUDE[win8](../../includes/win8-md.md)]64位<br /><br /> [!INCLUDE[win8_client_pro_2](../../includes/win8-client-pro-2-md.md)]64位<br /><br /> [!INCLUDE[win8_client_ent_2](../../includes/win8-client-ent-2-md.md)]64位<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 旗艦版 64 位元<br /><br /> [!INCLUDE[win7](../../includes/win7-md.md)]SP1 Enterprise 64 位<br /><br /> [!INCLUDE[win7](../../includes/win7-md.md)]SP1 Professional 64 位<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 家用進階版 64 位元<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 家用入門版 64 位元<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 旗艦版 32 位元<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 企業版 32 位元<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 專業版 32 位元<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 家用進階版 32 位元<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 家用入門版 32 位元<br /><br /> [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)]SP2 Datacenter 64 位<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Enterprise 64 位元<br /><br /> [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)]SP2 Standard 64 位<br /><br /> [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)]SP2 Foundation 64 位<br /><br /> [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)]SP2 Web 64 位<br /><br /> [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)]SP2 Datacenter 64 位<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Enterprise 32 位元<br /><br /> [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)]SP2 Standard 32 位<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Web 32 位元|Windows 10 家用版 64 位元<br /><br /> Windows 10 專業版 64 位元<br /><br /> Windows 10 企業版 64 位元<br /><br />[!INCLUDE[winserver2019_datacenter_md](../../includes/winserver2019-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2019_standard_md](../../includes/winserver2019-standard-md.md)]<br/><br/>[!INCLUDE[winserver2016_datacenter_md](../../includes/winserver2016-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2016_standard_md](../../includes/winserver2016-standard-md.md)]<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)]R2 Datacenter 64 位<br /><br /> [!INCLUDE[win8srv](../../includes/win8srv-md.md)]R2 Standard 64 位<br /><br /> [!INCLUDE[win8srv](../../includes/win8srv-md.md)]R2 Essentials 64 位<br /><br /> [!INCLUDE[win8srv](../../includes/win8srv-md.md)]R2 Foundation 64 位<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Datacenter 64 位元<br /><br /> [!INCLUDE[win8srv](../../includes/win8srv-md.md)]標準64位<br /><br /> 
  [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Essentials 64 位元<br /><br /> [!INCLUDE[win8srv](../../includes/win8srv-md.md)]Foundation 64 位<br /><br /> [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)]SP1 Datacenter 64 位<br /><br /> [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)]SP1 Enterprise 64 位<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Standard 64 位元<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Foundation 64 位元<br /><br /> 
  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 Web 64 位元<br /><br /> [!INCLUDE[winblue_client_2](../../includes/winblue-client-2-md.md)]64位<br /><br /> [!INCLUDE[winblue_client_pro_2](../../includes/winblue-client-pro-2-md.md)]64位<br /><br /> [!INCLUDE[winblue_client_ent_2](../../includes/winblue-client-ent-2-md.md)]64位<br /><br /> [!INCLUDE[win8](../../includes/win8-md.md)]64位<br /><br /> [!INCLUDE[win8_client_pro_2](../../includes/win8-client-pro-2-md.md)]64位<br /><br /> [!INCLUDE[win8_client_ent_2](../../includes/win8-client-ent-2-md.md)]64位<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 旗艦版 64 位元<br /><br /> [!INCLUDE[win7](../../includes/win7-md.md)]SP1 Enterprise 64 位<br /><br /> [!INCLUDE[win7](../../includes/win7-md.md)]SP1 Professional 64 位<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 家用進階版 64 位元<br /><br /> 
  [!INCLUDE[win7](../../includes/win7-md.md)] SP1 家用入門版 64 位元<br /><br /> [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)]SP2 Datacenter 64 位<br /><br /> 
  [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] SP2 Enterprise 64 位元<br /><br /> [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)]SP2 Standard 64 位<br /><br /> [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)]SP2 Foundation 64 位<br /><br /> [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)]SP2 Web 64 位|  
  
## <a name="minimum-sql-server-version-requirements-for-windows-10"></a>Windows 10 的 SQL Server 基本版本需求  
 在執行 Windows 10 的電腦上安裝 SQL Server 之前，必須先確定您符合下列基本需求：  
  
-   SQL Server 2014 必須套用 SQL Server 2014 Service Pack 1 或更新版的更新。 如需詳細資訊，請參閱 [如何取得 SQL Server 2014 的最新版 Service Pack](https://support.microsoft.com/kb/2958069)。  
  
-   SQL Server 2012 必須套用 SQL Server 2012 Service Pack 2 或更新版的更新。 如需詳細資訊，請參閱 [如何取得 SQL Server 2012 的最新版 Service Pack](https://support.microsoft.com/kb/2755533)。  
  
-   SQL Server 2008 R2  
    與 SQL Server 2008 在 Windows 10 不受支援。  
  
##  <a name="CrossLanguageSupport"></a> 跨語言支援  
 如需跨語言支援及使用當地語系化語言安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之考量的詳細資訊，請參閱 [SQL Server 中的地區語言版本](local-language-versions-in-sql-server.md)。  
  
##  <a name="ess"></a>擴充系統支援  
 
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 64 位元版本包含擴充系統的支援，亦稱為 Windows 64 位元上的 Windows 32 位元 (WOW64)。 WOW64 是 Windows 64 位元版本的一項功能，可讓 32 位元應用程式在 32 位元模式中以原生方式執行。 即使基礎作業系統是 64 位元，應用程式仍可在 32 位元模式下運作。  
  
##  <a name="HardDiskSpace"></a>硬碟空間需求（32位和64位）  
 在安裝期間 Windows Installer 會在系統磁片磁碟機上建立暫存檔案。 執行安裝程式以安裝或升級[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]之前，請確認系統磁片磁碟機上至少有**6.0 GB**的可用磁碟空間可供這些檔案使用。 即使您將元件安裝到非預設磁片磁碟機，這項需求也適用。  
  
 實際硬碟空間需求需視系統組態和您決定要安裝的功能而定。 如需版本支援的功能清單[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，請參閱[SQL Server 2014 版本所支援的功能](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)。 下表提供 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 元件的磁碟空間需求。  
  
|**功能**|**磁碟空間需求**|  
|-----------------|--------------------------------|  
|[!INCLUDE[ssDE](../../includes/ssde-md.md)] 和資料檔案、複寫、全文檢索搜尋和 Data Quality Services|811 MB|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 和資料檔案|345 MB|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]和報表管理員|304 MB|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|591 MB|  
|[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]|243 MB|  
|用戶端元件 ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 線上叢書元件和 Integration Services 工具除外)|1823 MB|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]《線上叢書》元件，用以查看和管理說明內容<sup>1</sup>|375 KB|  
  
 <sup>1</sup>下載線上叢書內容的磁碟空間需求為 200 MB。  
  
##  <a name="StorageTypes"></a> 資料檔案的儲存類型  
 支援的資料檔案儲存類型包括：  
  
-   本機磁碟  
  
-   共用儲存  
  
-   SMB 檔案共用  
  
    > **注意：** 獨立或叢集安裝的[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]資料檔案不支援 SMB 儲存體。 請改用直接附加儲存體或存放區域網路。  
  
    > **重要！！** SMB 儲存體可由 Windows File Server 或協力廠商 SMB 儲存體裝置所裝載。 如果使用了 Windows File Server，則 Windows File Server 版本應為 2008 或更新版本。 如需有關使用 SMB 檔案共用安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 做為儲存體選項的詳細資訊，請參閱[＜安裝 SQL Server 與 SMB 檔案共用儲存體＞](../../database-engine/install-windows/install-sql-server-with-smb-fileshare-as-a-storage-option.md)。  
  
    > **警告！！！！**  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 容錯移轉叢集安裝只有在安裝 tempdb 檔時支援本機磁碟。 請確定針對 tempdb 資料和記錄檔所指定的路徑在**所有**叢集節點上都是有效的。 在容錯移轉期間，如果容錯移轉目標節點上的 tempdb 目錄無法使用，則 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資源將無法上線。  
  
##  <a name="DC_support"></a>在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]網域控制站上安裝-限制  
 基於安全性理由，不建議您在網域控制站上安裝 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式將不會封鎖當做網域控制站之電腦上的安裝，但適用以下限制：  
  
-   您無法以本機服務帳戶在網域控制站上執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務。  
  
-   當 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝到電腦上以後，您無法將電腦從網域成員變成網域控制站。 在您將主機電腦變更為網域控制站之前，必須先解除安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
-   當 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝到電腦上以後，您無法將電腦從網域控制站變成網域成員。 在您將主機電腦變更為網域成員之前，必須先解除安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 容錯移轉叢集執行個體。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式無法在唯讀的網域控制站上建立安全性群組或提供 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務帳戶。 在此狀況中，安裝程式將會失敗。  
  
## <a name="see-also"></a>另請參閱  
 [規劃 SQL Server 安裝](planning-a-sql-server-installation.md)   
 [SQL Server 安裝的安全性考量](security-considerations-for-a-sql-server-installation.md)   
 [SQL Server 2014 的產品規格](../../getting-started/sql-server-2014-product-specifications.md)  
