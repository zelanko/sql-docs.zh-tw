---
title: 安裝 SQL Server 2016 的硬體與軟體需求 | Microsoft Docs
ms.custom: ''
ms.date: 08/23/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: install
ms.reviewer: ''
ms.suite: sql
ms.technology:
- setup-install
ms.tgt_pltfrm: ''
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
caps.latest.revision: 333
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 63b782f8026e25ab7ad1544ae2fd4cc481e78283
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="hardware-and-software-requirements-for-installing-sql-server"></a>安裝 SQL Server 2008 R2 的硬體和軟體需求
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文章列出在 Windows 作業系統上安裝和執行 [!INCLUDE[ssNoVer](../../includes/ssnoversion-md.md)] 的最低軟硬體需求。 

[!INCLUDE[sscurrent](../../includes/sssqlv14-md.md)] 推出 Linux 的 [!INCLUDE[ssNoVer](../../includes/ssnoversion-md.md)] 支援。 如需資訊，請參閱[ Linux 上 [!INCLUDE[ssNoVersion](../../includes/ssNoVersion_md.md)] 的硬體與軟體需求](../../linux/sql-server-linux-setup.md#system)。 

> 本文章適用於 [!INCLUDE[ss2016](../../includes/sssql15-md.md)] 和更新版本。 如需舊版 SQL Server 的相關內容，請參閱[安裝 SQL Server 2014 的硬體和軟體需求](https://msdn.microsoft.com/library/ms143506(v=sql.120).aspx)。 
  
**現在就試試看：**  
  
-   從[**評估中心**](https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016)下載 SQL Server。 
  
-    啟動已安裝 [**SQL Server 2016**](https://azure.microsoft.com/en-us/services/virtual-machines/sql-server/?wt.mc_id=sqL16_vm) 的虛擬機器。  
  
 **下列考量適用於所有版本：**  
  
-   建議您在使用 NTFS 或 ReFS 檔案格式的電腦上執行 [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] 。 雖然支援在使用 FAT32 檔案系統的電腦上安裝 [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] ，但並不建議這種做法，因為其安全性低於 NTFS 或 ReFS 檔案系統。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式將會封鎖在唯讀、對應或是壓縮的磁碟機上進行的安裝。  
  
-   如果您透過遠端桌面連線使用 RDC 用戶端本機資源的媒體來啟動安裝程式，則安裝會失敗。 必須在實體或虛擬機器的網路共用或本機從遠端安裝媒體。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝媒體可能位於網路共用、對應磁碟機、本機磁碟機，或顯示為虛擬機器的 ISO。  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 安裝的必要條件是安裝 .NET 4.6.1。 安裝程式會在選取 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 時自動安裝 .NET 4.6.1。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式會安裝該產品所需的下列軟體元件：  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式支援檔案  
  
-   如需在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 [!INCLUDE[win8srv](../../includes/win8srv-md.md)] 上安裝 [!INCLUDE[win8](../../includes/win8-md.md)] 的最低版本需求，請參閱[在 Windows Server 2012 或 Windows 8 上安裝 SQL Server](http://support.microsoft.com/kb/2681562) (http://support.microsoft.com/kb/2681562)。  
  
##  <a name="hwswr"></a> 硬體及軟體需求  
下列需求適用於所有安裝：  
  
|元件|需求|  
|---------------|-----------------|  
|.NET Framework|[!INCLUDE[sql2016](../../includes/sssql15-md.md)] RC1 和更新版本需要 Database Engine、Master Data Services 或複寫的 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 4.6。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016 安裝程式會自動安裝 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]。 您也可以從 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] Microsoft .NET Framework 4.6 (Web Installer) for Windows [(適用於 Windows 的 Microsoft .NET Framework 4.6 (Web 安裝程式)) 手動安裝](http://support.microsoft.com/kb/3045560)。<br/><br/> 如需 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 4.6 的詳細資訊、建議和指引，請參閱 [.NET Framework 開發人員部署手冊](http://msdn.microsoft.com/library/ee942965\(v=vs.110\).aspx)。<br/><br/>[!INCLUDE[winblue_client_2](../../includes/winblue-client-2-md.md)]，而安裝 [!INCLUDE[winblue_server_2](../../includes/winblue-server-2-md.md)] 4.6 之前， [需要](http://support.microsoft.com/kb/2919355) KB2919355 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 。|  
|網路軟體|[!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] 支援的作業系統有內建的網路軟體。 獨安裝立的具名執行個體和預設執行個體支援下列網路通訊協定：共用記憶體、具名管道、TCP/IP 和 VIA。<br/><br/> 注意：容錯移轉叢集上不支援共用記憶體和 VIA。<br/><br/> 另請注意，VIA 通訊協定已被取代。 [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]<br/><br/> <br/><br/> 如需有關網路通訊協定和網路程式庫的詳細資訊，請參閱＜ [Network Protocols and Network Libraries](../../sql-server/install/network-protocols-and-network-libraries.md)＞。|  
|硬碟|[!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] 需要至少 6 GB 的可用硬碟空間。<br/><br/> 磁碟空間需求會因為您安裝的 [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] 元件而有所不同。 如需詳細資訊，請參閱本文章稍後的[硬碟空間需求](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md#HardDiskSpace)。 如需支援之資料檔案儲存類型的資訊，請參閱 [資料檔案的儲存類型](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md#StorageTypes)。|  
|光碟機|若要從光碟片安裝，則需要 DVD 光碟機。|  
|監視器|[!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] 需要 Super-VGA (800x600) 或更高解析度的監視器。|  
|網際網路|網際網路功能需要網際網路存取 (可能會另行收費)。|  
  
 注意：由於虛擬化的負荷所致，因此在虛擬機器上執行 [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] 的速度會比原生方式執行要慢。  
  
 PolyBase 功能有其他的硬體和軟體需求。 如需詳細資訊，請參閱 [開始使用 PolyBase](../../relational-databases/polybase/get-started-with-polybase.md)。  
  
##  <a name="pmosr"></a> 處理器、記憶體和作業系統需求  
 下列記憶體和處理器需求適用於所有版本的 [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)]：  
  
|元件|需求|  
|---------------|-----------------|  
|記憶體 *|**最小值：**<br/><br/> Express 版：512 MB<br/><br/> 所有其他版本：1 GB<br/><br/> **建議使用：**<br/><br/> Express 版：1 GB<br/><br/> 所有其他版本：至少 4 GB，並應隨著資料庫大小增加以確保最佳效能。|  
|處理器速度|**最小值：** x64 處理器：1.4 GHz<br/><br/> **建議值：** 2.0 GHz 或以上|  
|處理器類型|x64 處理器：AMD Opteron、AMD Athlon 64、具有 Intel EM64T 支援的 Intel Xeon、具有 EM64T 支援的 Intel Pentium IV|  
  
> [!NOTE]  
>  只有 x64 處理器支援安裝 [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] 。 x86 處理器不再支援其安裝。  
  
 \*在 [!INCLUDE[ssDQSnoversion](../../includes/ssdqsnoversion-md.md)] (DQS) 中安裝 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] 元件所需的最小記憶體為 2 GB RAM，這與 [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] 的最小記憶體需求不同。 如需有關安裝 DQS 的詳細資訊，請參閱＜ [Install Data Quality Services](../../data-quality-services/install-windows/install-data-quality-services.md)＞。  
  
 **WOW64 支援：**  
  
 WOW64 (Windows 64 位元上的 Windows 32 位元) 是 Windows 64 位元版本的一項功能，可讓 32 位元應用程式在 32 位元模式中以原生方式執行。 即使基礎作業系統是 64 位元的作業系統，應用程式仍可在 32 位元模式下運作。 [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] 安裝不支援 WOW64。 不過，WOW64 支援管理工具。  
  
 **作業系統支援：**  
  
 [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] 版本分類如下：  
  
-   [主要版本](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md#TOP_Principal)  
  
-   [廣泛版本](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md#TOP_Breadth)  
  
> [!NOTE]  
>  本節所述的作業系統支援的例外狀況，是下列 SQL Server 2016 和更新版本的商業智慧功能，可以安裝在 Windows Server 2008 R2 SP1 或更新版本上︰  
>  
>-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] - SharePoint  
> 
>-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 適用於 SharePoint 產品的增益集  
  
### <a name="features-supported-on-32-bit-client-operating-systems"></a>32 位元用戶端作業系統支援的功能  
 Windows 用戶端作業系統，例如 Windows 10 和 Windows 8.1 都有 32 位元或 64 位元架構。   64 位元用戶端作業系統支援所有的 SQL Server 功能。 在支援的 32 位元用戶端作業系統上，Microsoft 支援下列功能︰  
  
-   Data Quality Client  
  
-   用戶端工具連接性  
  
-   Integration Services  
  
-   用戶端工具回溯相容性  
  
-   用戶端工具 SDK  
  
-   文件集元件  
  
-   Distributed Replay 元件  
  
-   Distributed Replay Controller  
  
-   Distributed Replay Client  
  
-   SQL 用戶端連接性 SDK  
  
 [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] 和更新版本的伺服器作業系統沒有 32 位元架構。 所有支援的伺服器作業系統只有 64 位元。 64 位元伺服器作業系統支援所有的功能。  
  
###  <a name="TOP_Principal"></a>[!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] 的主要版本  
 下表顯示 [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)]主要版本的作業系統需求：  
  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本|支援的作業系統|  
|---------------------------------------|--------------------------------|  
|[!INCLUDE[ssEnterprise](../../includes/ssenterprise-md.md)]|[!INCLUDE[winserver2016_datacenter_md](../../includes/winserver2016-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2016_standard_md](../../includes/winserver2016-standard-md.md)]<br/><br/>[!INCLUDE[winserver2016_essentials_md](../../includes/winserver2016-essentials-md.md)]* <br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Datacenter<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Standard<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Essentials<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Foundation<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Datacenter<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Standard<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Essentials<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Foundation|  
|[!INCLUDE[ssStandard](../../includes/ssstandard-md.md)]|[!INCLUDE[winserver2016_datacenter_md](../../includes/winserver2016-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2016_standard_md](../../includes/winserver2016-standard-md.md)]<br/><br/>[!INCLUDE[winserver2016_essentials_md](../../includes/winserver2016-essentials-md.md)]* <br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Datacenter<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Standard<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Essentials<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Foundation<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Datacenter<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Standard<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Essentials<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Foundation<br/><br/> Windows 10 Home<br/><br/> Windows 10 Professional<br/><br/> Windows 10 Enterprise<br/><br/>Windows 10 IoT 企業版<br/><br/>[!INCLUDE[winblue_client_2](../../includes/winblue-client-2-md.md)]<br/><br/>[!INCLUDE[winblue_client_pro_2](../../includes/winblue-client-pro-2-md.md)]<br/><br/>[!INCLUDE[winblue_client_ent_2](../../includes/winblue-client-ent-2-md.md)]<br/><br/>[!INCLUDE[win8](../../includes/win8-md.md)]<br/><br/>[!INCLUDE[win8_client_pro_2](../../includes/win8-client-pro-2-md.md)]<br/><br/>[!INCLUDE[win8_client_ent_2](../../includes/win8-client-ent-2-md.md)]|  
|[!INCLUDE[ssWeb](../../includes/ssweb-md.md)]|[!INCLUDE[winserver2016_datacenter_md](../../includes/winserver2016-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2016_standard_md](../../includes/winserver2016-standard-md.md)]<br/><br/>[!INCLUDE[winserver2016_essentials_md](../../includes/winserver2016-essentials-md.md)]* <br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Datacenter<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Standard<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Essentials<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Foundation<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Datacenter<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Standard<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Essentials<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Foundation|  
  
\*不支援 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。
  
###  <a name="TOP_Breadth"></a> [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] 的廣泛版本  
 下表顯示 [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)]廣泛版本的作業系統需求：  
  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本|支援的作業系統|  
|---------------------------------------|--------------------------------|  
|[!INCLUDE[ssDeveloper](../../includes/ssdeveloper-md.md)]|[!INCLUDE[winserver2016_datacenter_md](../../includes/winserver2016-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2016_standard_md](../../includes/winserver2016-standard-md.md)]<br/><br/>[!INCLUDE[winserver2016_essentials_md](../../includes/winserver2016-essentials-md.md)]* <br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Datacenter<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Standard<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Essentials<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Foundation<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Datacenter<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Standard<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Essentials<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Foundation<br/><br/> Windows 10 Home<br/><br/> Windows 10 Professional<br/><br/> Windows 10 Enterprise<br/><br/>Windows 10 IoT 企業版<br/><br/>[!INCLUDE[winblue_client_2](../../includes/winblue-client-2-md.md)]<br/><br/>[!INCLUDE[winblue_client_pro_2](../../includes/winblue-client-pro-2-md.md)]<br/><br/>[!INCLUDE[winblue_client_ent_2](../../includes/winblue-client-ent-2-md.md)]<br/><br/>[!INCLUDE[win8](../../includes/win8-md.md)]<br/><br/>[!INCLUDE[win8_client_pro_2](../../includes/win8-client-pro-2-md.md)]<br/><br/>[!INCLUDE[win8_client_ent_2](../../includes/win8-client-ent-2-md.md)]|  
|[!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]|[!INCLUDE[winserver2016_datacenter_md](../../includes/winserver2016-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2016_standard_md](../../includes/winserver2016-standard-md.md)]<br/><br/>[!INCLUDE[winserver2016_essentials_md](../../includes/winserver2016-essentials-md.md)]* <br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Datacenter<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Standard<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Essentials<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Foundation<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Datacenter<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Standard<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Essentials<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Foundation<br/><br/> Windows 10 Home<br/><br/> Windows 10 Professional<br/><br/> Windows 10 Enterprise<br/><br/>Windows 10 IoT 企業版<br/><br/>[!INCLUDE[winblue_client_2](../../includes/winblue-client-2-md.md)]<br/><br/>[!INCLUDE[winblue_client_pro_2](../../includes/winblue-client-pro-2-md.md)]<br/><br/>[!INCLUDE[winblue_client_ent_2](../../includes/winblue-client-ent-2-md.md)]<br/><br/>[!INCLUDE[win8](../../includes/win8-md.md)]<br/><br/>[!INCLUDE[win8_client_pro_2](../../includes/win8-client-pro-2-md.md)]<br/><br/>[!INCLUDE[win8_client_ent_2](../../includes/win8-client-ent-2-md.md)]|  

\*不支援 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。
  
##  <a name="CrossLanguageSupport"></a> 跨語言支援  
 如需跨語言支援及使用當地語系化語言安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之考量的詳細資訊，請參閱 [SQL Server 中的地區語言版本](../../sql-server/install/local-language-versions-in-sql-server.md)。  
  
##  <a name="HardDiskSpace"></a> 硬碟空間需求  
 安裝 [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)]期間，Windows Installer 會在系統磁碟機上建立暫存檔。 在執行安裝程式來安裝或升級 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]之前，請確認系統磁碟機上至少有 6.0 GB 的可用磁碟空間可供這些檔案使用。 即使您將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 元件安裝到非預設磁碟機，這項需求也適用。  
  
 實際硬碟空間需求需視系統組態和您決定要安裝的功能而定。 下表提供 [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] 元件的磁碟空間需求。  
  
|**功能**|**磁碟空間需求**|  
|-----------------|--------------------------------|  
|[!INCLUDE[ssDE](../../includes/ssde-md.md)] 和資料檔案、複寫、全文檢索搜尋和 Data Quality Services|1480 MB|  
|[!INCLUDE[ssDE](../../includes/ssde-md.md)] (如上) 與 R Services (資料庫內)|2744 MB|  
|[!INCLUDE[ssDE](../../includes/ssde-md.md)] (如上) 與外部資料的 PolyBase 查詢服務|4194 MB|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 和資料檔案|698 MB|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|967 MB|  
|[!INCLUDE[rsql_platform](../../includes/rsql-platform-md.md)] (獨立式)|280 MB|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] - SharePoint|1203 MB|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 適用於 SharePoint 產品的增益集|325 MB|  
|[!INCLUDE[ssDQSClient](../../includes/ssdqsclient-md.md)]|121 MB|  
|用戶端工具連接性|328 MB|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|306 MB|  
|用戶端元件 ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 線上叢書元件和 Integration Services 工具除外)|445 MB|  
|[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]|280 MB|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 線上叢書元件，可用來檢視並管理說明內容*|27 MB|  
|所有功能|8030 MB|  
  
 *下載線上叢書內容的磁碟空間需求為 200 MB。  
  
##  <a name="StorageTypes"></a> 資料檔案的儲存類型  
 支援的資料檔案儲存類型包括：  
  
-   本機磁碟  
  
-   共用儲存  

-   [儲存空間直接存取 \(S2D\)](https://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview)
  
-   SMB 檔案共用  
  
    > [!NOTE]  
    >  獨立或叢集安裝的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料檔案不支援 SMB 儲存體。 請改用直接連結存放裝置、存放區域網路或 S2D。  
  
    > [!IMPORTANT]  
    >  SMB 儲存體可由 Windows File Server 或協力廠商 SMB 儲存體裝置所裝載。 如果使用了 Windows File Server，則 Windows File Server 版本應為 2008 或更新版本。 如需有關使用 SMB 檔案共用安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 做為儲存體選項的詳細資訊，請參閱＜ [Install SQL Server with SMB Fileshare as a Storage Option](../../database-engine/install-windows/install-sql-server-with-smb-fileshare-as-a-storage-option.md)的最低軟硬體需求。  
  
    > [!WARNING]  
    >  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 容錯移轉叢集安裝只有在安裝 tempdb 檔時支援本機磁碟。 務必確定在所有叢集節點上為 tempdb 資料和記錄檔指定的路徑都是有效的。 在容錯移轉期間，如果容錯移轉目標節點上的 tempdb 目錄無法使用，則 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資源將無法上線。  
  
##  <a name="DC_support"></a> 在網域控制站上安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 基於安全性理由，不建議您在網域控制站上安裝 [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] 。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式將不會封鎖當做網域控制站之電腦上的安裝，但適用以下限制：  
  
-   您無法以本機服務帳戶在網域控制站上執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務。  
  
-   當 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝到電腦上以後，您無法將電腦從網域成員變成網域控制站。 在您將主機電腦變更為網域控制站之前，必須先解除安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
-   當 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝到電腦上以後，您無法將電腦從網域控制站變成網域成員。 在您將主機電腦變更為網域成員之前，必須先解除安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 容錯移轉叢集執行個體。  
  
- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不受唯讀網域控制站的支援。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式無法在唯讀的網域控制站上建立安全性群組或提供 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務帳戶。 在此狀況中，安裝程式將會失敗。  

- 只能存取唯讀網域控制站的環境不支援 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 容錯移轉叢集執行個體。 
  
## <a name="see-also"></a>另請參閱  
 [規劃 SQL Server 安裝](../../sql-server/install/planning-a-sql-server-installation.md)   
 [SQL Server 安裝的安全性考量](../../sql-server/install/security-considerations-for-a-sql-server-installation.md)   
 [SQL Server 2016 的產品規格](http://msdn.microsoft.com/library/6445fd53-6844-4170-a86b-7fe76a9f64cb)  
  
  
