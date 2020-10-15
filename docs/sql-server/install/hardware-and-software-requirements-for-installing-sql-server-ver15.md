---
title: SQL Server 2019：硬體與軟體需求
description: 安裝及執行 SQL Server 2019 的硬體、軟體和作業系統需求清單。
ms.custom: sqlfreshmay19
ms.date: 09/01/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: release-landing
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
ms.author: mikeray
author: MikeRayMSFT
ms.openlocfilehash: 89088af9d3758a710db5bd1ee313835087bad832
ms.sourcegitcommit: a41e1f4199785a2b8019a419a1f3dcdc15571044
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/13/2020
ms.locfileid: "91987649"
---
# <a name="sql-server-2019-hardware-and-software-requirements"></a>SQL Server 2019：硬體和軟體需求
[!INCLUDE [SQL Server Windows Only - ASDBMI ](../../includes/applies-to-version/sql-windows-only-asdbmi.md)]

本文列出在 Windows 作業系統上安裝及執行 SQL Server 2019 的最低硬體和軟體需求。

如需其他 SQL Server 版本的硬體和軟體需求，請參閱：
- [SQL Server 2016 和 2017](hardware-and-software-requirements-for-installing-sql-server.md)
- [Linux 上的 SQL Server](../../linux/sql-server-linux-setup.md#system)
- [巨量資料叢集](../../big-data-cluster/deployment-guidance.md)

##  <a name="hardware-requirements"></a><a name="pmosr"></a> 硬體需求  
 下列記憶體和處理器需求適用於所有版本的 [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)]：  
  
|元件|需求|  
|---------------|-----------------|  
|硬碟|[!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] 需要至少 6 GB 的可用硬碟空間。<br/><br/> 磁碟空間需求會因為您安裝的 [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] 元件而有所不同。 如需詳細資訊，請參閱本文章稍後的[硬碟空間需求](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md#HardDiskSpace)。 如需支援之資料檔案儲存類型的資訊，請參閱 [資料檔案的儲存類型](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md#StorageTypes)。|  
|監視|[!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] 需要 Super-VGA (800x600) 或更高解析度的監視器。|  
|Internet|網際網路功能需要網際網路存取 (可能會另行收費)。|  
|記憶體 \*|**最低規格：**<br/><br/> Express 版本：512 MB<br/><br/> 所有其他版本：1 GB<br/><br/> **建議配備：**<br/><br/> Express 版本：1 GB<br/><br/> 所有其他版本：至少 4 GB，並應隨著資料庫大小增加以確保最佳效能。|  
|處理器速度|**最小值：** x64 處理器：1.4 GHz<br/><br/> **建議配備：** 2.0 GHz 或更快|  
|處理器類型|x64 處理器：AMD Opteron、AMD Athlon 64、具有 Intel EM64T 支援的 Intel Xeon、具有 EM64T 支援的 Intel Pentium IV|  
  
> [!NOTE]  
> 只有 x64 處理器支援安裝 [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] 。 x86 處理器不再支援其安裝。  
  
 \*在 [!INCLUDE[ssDQSnoversion](../../includes/ssdqsnoversion-md.md)] (DQS) 中安裝 [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] 元件所需的最小記憶體為 2 GB RAM，這與 [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] 的最小記憶體需求不同。 如需有關安裝 DQS 的詳細資訊，請參閱＜ [Install Data Quality Services](../../data-quality-services/install-windows/install-data-quality-services.md)＞。  


##  <a name="software-requirements"></a><a name="hwswr"></a> 軟體需求  

下列需求適用於所有安裝：  
  
|元件|需求|  
|---------------|-----------------|  
|作業系統|Windows 10 TH1 1507 或更新版本<br/><br>Windows Server 2016 或更新版本<br/><br/>
|.NET Framework|最低作業系統包括最低的 .NET Framework。|  
|網路軟體|[!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] 支援的作業系統有內建的網路軟體。 獨立安裝的具名和預設執行個體均支援下列網路通訊協定：共用記憶體、具名管道和 TCP/IP。<br/><br/> |  

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式會安裝該產品所需的下列軟體元件：  
  
   - [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client    
   - [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式支援檔案  


> [!IMPORTANT]
> PolyBase 功能有其他的硬體和軟體需求。 如需詳細資訊，請參閱 [開始使用 PolyBase](../../relational-databases/polybase/polybase-guide.md)。  
  

##  <a name="operating-system-support"></a><a name="TOP_Principal"></a> 作業系統支援 

下表顯示 SQL Server 2019 哪些版本可與 Windows 的哪些版本相容：  
  

| SQL Server 版本：               | Enterprise | 開發人員 | 標準 | Web | Express |  
| :------------------------         | :--------- | :-------- | :------- | :-- | :------ | 
| Windows Server 2019 Datacenter    |    是     |    是    |    是   | 是 |   是   |
| Windows Server 2019 Standard      |    是     |    是    |    是   | 是 |   是   |
| Windows Server 2019 Essentials    |    是     |    是    |    是   | 是 |   是   |
| Windows Server 2016 Datacenter    |    是     |    是    |    是   | 是 |   是   |
| Windows Server 2016 Standard      |    是     |    是    |    是   | 是 |   是   |
| Windows Server 2016 Essentials    |    是     |    是    |    是   | 是 |   是   |
| Windows 10 IoT 企業版         |    否      |    是    |    是   | 否  |   是   |
| Windows 10 Enterprise             |    否      |    是    |    是   | 否  |   是   |
| Windows 10 Professional           |    否      |    是    |    是   | 否  |   是   |
| Windows 10 Home                   |    否      |    是    |    是   | 否  |   是   |
| &nbsp; | &nbsp; |

### <a name="server-core-support"></a>Server Core 支援

下列 Windows Server 版本支援在 Server Core 模式中安裝 SQL Server 2019：

:::row:::
    :::column:::
        Windows Server 2019 Core
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        Windows Server 2016 Core
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
    :::column-end:::
:::row-end:::

如需在 Server Core 上安裝 SQL Server 的詳細資訊，請參閱[在 Server Core 上安裝 SQL Server](../../database-engine/install-windows/install-sql-server-on-server-core.md)。 


##  <a name="cross-language-support"></a><a name="CrossLanguageSupport"></a> 跨語言支援  
 如需跨語言支援及使用當地語系化語言安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之考量的詳細資訊，請參閱 [SQL Server 中的地區語言版本](../../sql-server/install/local-language-versions-in-sql-server.md)。  
  
##  <a name="disk-space-requirements"></a><a name="HardDiskSpace"></a>  磁碟空間需求  
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
  
##  <a name="storage-types-for-data-files"></a><a name="StorageTypes"></a> 資料檔案的儲存類型  
 支援的資料檔案儲存類型包括：  
  
- 本機磁碟 
    - [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 目前支援具有標準原生磁區大小 512 位元組及 4 KB 的磁碟機。  磁區大小大於 4 KB 的硬碟可能會在嘗試於其上儲存 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料檔案時產生錯誤。  請參閱 [SQL Server 中的硬碟磁區大小支援界限](https://support.microsoft.com/kb/926930) \(機器翻譯\)，以取得 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中硬碟磁區大小支援的詳細資訊。 
    - [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 容錯移轉叢集安裝只有在安裝 tempdb 檔時支援本機磁碟。 務必確定在所有叢集節點上為 tempdb 資料和記錄檔指定的路徑都是有效的。 在容錯移轉期間，如果容錯移轉目標節點上的 tempdb 目錄無法使用，則 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資源將無法上線。
- 共用儲存  
- [儲存空間直接存取 \(S2D\)](/windows-server/storage/storage-spaces/storage-spaces-direct-overview)  
- SMB 檔案共用  
    - 獨立或叢集安裝的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 資料檔案不支援 SMB 儲存體。 請改用直接連結存放裝置、存放區域網路或 S2D。 
    - SMB 儲存體可由 Windows 檔案伺服器或第三方 SMB 存放裝置所裝載。 如果使用了 Windows File Server，則 Windows File Server 版本應為 2008 或更新版本。 如需有關使用 SMB 檔案共用安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 做為儲存體選項的詳細資訊，請參閱[＜安裝 SQL Server 與 SMB 檔案共用儲存體＞](../../database-engine/install-windows/install-sql-server-with-smb-fileshare-as-a-storage-option.md)。  
  
  
  
##  <a name="installing-ssnoversion-on-a-domain-controller"></a><a name="DC_support"></a> 在網域控制站上安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 基於安全性理由，不建議您在網域控制站上安裝 [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] 。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式將不會封鎖當做網域控制站之電腦上的安裝，但適用以下限制：  
  
- 您無法以本機服務帳戶在網域控制站上執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務。    
- 當 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝到電腦上以後，您無法將電腦從網域成員變成網域控制站。 在您將主機電腦變更為網域控制站之前，必須先解除安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。    
- 當 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝到電腦上以後，您無法將電腦從網域控制站變成網域成員。 在您將主機電腦變更為網域成員之前，必須先解除安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。   
- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 容錯移轉叢集執行個體。   
- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不受唯讀網域控制站的支援。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式無法在唯讀的網域控制站上建立安全性群組或提供 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務帳戶。 在此狀況中，安裝程式將會失敗。 
- 只能存取唯讀網域控制站的環境不支援 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 容錯移轉叢集執行個體。 
  
## <a name="installation-media"></a>安裝媒體

您可從下列位置取得相關的安裝媒體： 
  
- [SQL Server Evaluation Center](https://www.microsoft.com/evalcenter/evaluate-sql-server-2019)
- [最新的累積更新](../../database-engine/install-windows/latest-updates-for-microsoft-sql-server.md)

或者，您可建立[已在執行 SQL Server 的 Azure 虛擬機器](/azure/virtual-machines/windows/sql/quickstart-sql-vm-create-portal)，但由於虛擬化的額外負荷，虛擬機器上的 SQL Server 速度會比原生方式執行要慢。


## <a name="next-steps"></a>後續步驟

檢閱安裝 SQL Server 的硬體和軟體需求之後，即可開始[規劃 SQL Server 安裝](../../sql-server/install/planning-a-sql-server-installation.md)或檢閱 [SQL Server 的安全性考量](../../sql-server/install/security-considerations-for-a-sql-server-installation.md)。