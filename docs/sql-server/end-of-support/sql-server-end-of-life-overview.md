---
title: 終止支援選項
description: 了解已達終止支援其 SQL Server 產品 (例如 SQL Server 2005、SQL Server 2008 和 SQL Server 2008 R2) 的各種可用選項。
ms.date: 08/12/2020
ms.prod: sql
ms.technology: install
ms.topic: conceptual
author: cawrites
ms.author: chadam
ms.reviewer: pmasl
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: e465f1e4e8c6cc9e5effb27c1cc97ee7633309eb
ms.sourcegitcommit: ece151df14dc2610d96cd0d40b370a4653796d74
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "96297960"
---
# <a name="sql-server-end-of-support-options"></a>SQL Server 終止支援選項 
[!INCLUDE [SQL Server Windows Only - ASDBMI ](../../includes/applies-to-version/sql-windows-only-asdbmi.md)]

本文說明可用於解決已達終止支援其 SQL Server 產品的選項。

## <a name="understanding-the-sql-server-lifecycle"></a>了解 SQL Server 生命週期

每種 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本至少有 10 年的支援，包括 5 年的主要支援，以及 5 年的延伸支援：
-  **主要支援** 包含功能、效能、延展性和安全性更新。 
-  **延伸支援** 僅包含安全性更新。 

**終止支援** (有時也稱為生命週期結束) 表示產品已達其生命週期的尾端，不再為產品提供服務和支援。 如需 Microsoft 週期的詳細資訊，請參閱 [Microsoft 週期原則](https://support.microsoft.com/hub/4095338/microsoft-lifecycle-policy)。



## <a name="options"></a>選項。

一旦您的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 已達終止支援階段，您可以選擇：
- 升級至目前的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本。
- 購買[延伸安全性更新訂閱](https://www.microsoft.com/cloud-platform/extended-security-updates)。 
- 將您的工作負載依現況移轉到 Azure 虛擬機器，以取得[免費的延伸安全性更新](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-server-2008-eos-extend-support)。
- 將您的工作負載移轉到 [Azure SQL Database 服務](/azure/sql-database/sql-database-paas-vs-sql-server-iaas)。 

如需規劃升級或移轉並將其自動化的詳細資訊、指導方針和工具，請參閱 [SQL Server 2005 終止支援](https://www.microsoft.com/sql-server/sql-server-2005)和 [SQL Server 2008 終止支援](https://www.microsoft.com/cloud-platform/windows-sql-server-2008)。  

![終止支援選項](media/sql-server-end-of-life-overview/sql-server-upgrade-paths.png)

本文描述每種方法的優點和考量，以及可協助引導決策制定程序的其他資源。

## <a name="upgrade-sql-server"></a>升級 SQL Server

一旦您的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 已達終止支援，則可選擇升級至較新且支援的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本。 這會為您提供環境一致性、讓您能夠使用最新的功能集，並採用新版本的支援週期。

### <a name="benefits"></a>優點
- **最新技術**：新的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本引進一些創新，包括效能、延展性和高可用性功能，以及增強的安全性。 
- **控制**：因為軟硬體皆由您所管理，所以您幾乎能自由操控各項功能與規模調整功能。
- **熟悉的環境**：若要從舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 升級，則這是最相似的環境。
- **廣泛的適用性**：適用於任何種類的資料庫應用程式，包括 OLTP 系統和資料倉儲。
- **對資料庫應用程式的風險很低**：藉由維護與舊版系統相同層級的資料庫相容性，現有的資料庫應用程式會受到保護，以防止可能造成不利影響的功能和效能變更。 只有在應用程式需要使用由較新資料庫相容性設定所管制的功能時，才需要完整的重新認證。 如需詳細資訊，請參閱[相容性憑證](../../database-engine/install-windows/compatibility-certification.md)。

### <a name="considerations"></a>考量

- **成本**：此方法的初期投資最高，管理時間也最長。 您必須購買、維護及管理您所擁有的硬體與軟體。
- **停機**：視您的升級策略而定，可能會出現停機。 也會有在就地升級過程中遇到問題的固有風險。
- **複雜度**：如果您使用 Windows Server 2008 或 [!INCLUDE[winserver2008r2-md](../../includes/winserver2008r2-md.md)]，也需要升級 OS，因為這些 Windows 版本可能不支援較新版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 在 OS 升級過程中會有額外的風險，因此執行並存移轉雖然可能比較謹慎，但也是成本更高的方法。 Windows Server 2008 或 [!INCLUDE[winserver2008r2-md](../../includes/winserver2008r2-md.md)] 的容錯移轉叢集執行個體不支援就地 OS 升級。 

  > [!NOTE]
  > 從 Windows Server 2016 開始，可以進行叢集 OS 輪流升級。

### <a name="resources"></a>資源

[安裝媒體](https://www.microsoft.com/evalcenter/evaluate-sql-server-2017-rtm)   
[使用安裝精靈升級 SQL Server](../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md)

新功能：
- [SQL Server 2016](../what-s-new-in-sql-server-2016.md)
- [SQL Server 2017](../what-s-new-in-sql-server-2017.md) 
- [SQL Server 2019](../what-s-new-in-sql-server-ver15.md)   

硬體需求：
- [SQL Server 2017 與舊版](../install/hardware-and-software-requirements-for-installing-sql-server.md)  
- [SQL Server 2019](../install/hardware-and-software-requirements-for-installing-sql-server-ver15.md)    

支援的版本與版次升級：
- [SQL Server 2016](../../database-engine/install-windows/supported-version-and-edition-upgrades.md?view=sql-server-2016&preserve-view=true) 
- [SQL Server 2017](../../database-engine/install-windows/supported-version-and-edition-upgrades-2017.md)
- [SQL Server 2019](../../database-engine/install-windows/supported-version-and-edition-upgrades-version-15.md)

工具：
-  [資料庫測試助理](../../dea/database-experimentation-assistant-overview.md)有助於評估特定工作負載的目標 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本。 
-  [Data Migration Assistant](../../dma/dma-overview.md) 有助於偵測可能會影響新版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中資料庫功能的相容性問題。 
-  [查詢調整小幫手](../../relational-databases/performance/upgrade-dbcompat-using-qta.md)有助於調整在升級資料庫相容性時可能會遇到不利影響的工作負載。

下圖提供各種 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本多年來的創新範例： 

![25 年來的 SQL Server 創新](media/sql-server-end-of-life-overview/sql-server-version-improvements.png)

## <a name="extend-support"></a>延伸支援 

如果您尚未準備好升級，且尚未準備好移至雲端，則可購買延伸安全性更新訂閱，以在終止支援日期後收到長達三年的 **重大** 安全性更新。  

### <a name="benefits"></a>優點 

- **應用程式支援**：如果您的應用程式在較新版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 上需要重新認證，則這是最佳選項。 這通常適用於未使用[相容性認證](../../database-engine/install-windows/compatibility-certification.md)的應用程式。 
- **一致的基礎結構**：您不需要對基礎結構進行任何方式的變更。 
- **技術支援**：如果您有軟體保證或其他支援方案，則可以繼續從 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 收到終止支援的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 產品技術支援。 這是取得 [!INCLUDE[ssKatmai](../../includes/ssKatmai-md.md)] 和 [!INCLUDE[ssKilimanjaro](../../includes/ssKilimanjaro-md.md)] 支援的唯一方式。 
- **Time**：此選項的可用性為三年，其讓您有額外的時間來認證應用程式。 

### <a name="considerations"></a>考量 

- **有限可用性**：此選項僅適用於具有軟體保證或訂閱授權的客戶。 
- **成本**：此選項的成本可能很高，因為延伸安全性更新每年大約是內部部署授權成本的 75%。
- **有限時間範圍**：此選項的可用性為三年，因此如果想要確保安全性與合規性，您仍然需要在三年期間結束時進行升級或移轉。
- **沒有 Bug 修正**：如果產品發生非安全性 Bug，則 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 不會為此發行修正。 
- **有限支援**：延伸安全性更新不包含新功能、功能改善或客戶要求的修正。 安全性問題修正僅限於 [Microsoft 安全性回應中心 (MSRC)](https://portal.msrc.microsoft.com/) 分級為「重大」的更新。

### <a name="resources"></a>資源

[延伸安全性更新 (ESU) 概觀](sql-server-extended-security-updates.md)       
[詳細的 ESU 常見問題集](https://www.microsoft.com/cloud-platform/extended-security-updates)       
[依現況移轉到 Azure VM 以免費延伸支援](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-server-2008-eos-extend-support)       
[軟體保證](https://www.microsoft.com/licensing/licensing-programs/software-assurance-default)       

## <a name="azure-virtual-machine"></a>Azure 虛擬機器

另一個選項是將您的工作負載移轉到[執行 SQL Server 的 Azure 虛擬機器](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-server-iaas-overview)。 您可以依現況移轉系統並保留終止支援的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，也可以升級至較新版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 這最適用於需要 OS 層級存取的移轉及應用程式。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 虛擬機器可隨即轉移，適用於需要在最少或沒有變更情況下快速移轉到雲端的現有應用程式。 

### <a name="benefits"></a>優點

- **免費的延伸安全性更新**：如果您選擇依現況保留 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 來繼續使用 [!INCLUDE[ssKatmai](../../includes/ssKatmai-md.md)] 或 [!INCLUDE[ssKilimanjaro](../../includes/ssKilimanjaro-md.md)]，則可在終止支援日期後取得三年免費的延伸安全性更新，即使沒有軟體保證也一樣。 
- **節省成本**：您可以節省硬體和伺服器軟體的成本，只需按每小時使用量付費。 
- **隨即轉移**：您可以在最少或沒有變更的情況下，將 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和應用程式基礎結構隨即轉移到雲端。 
- **主控環境**：您會享有主控環境的優點，例如卸載硬體和軟體維護。 
- **自動化**：如果使用 [!INCLUDE[winserver2008r2-md](../../includes/winserver2008r2-md.md)] 和更新版本，您會享有自動修補和自動備份的優點。 
- **OS 控制**：您可以使用熟悉的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 功能集來控制作業系統環境。 
- **快速部署**：您可以從虛擬機器映像庫快速進行部署。 
- **授權行動性**：您可以自備授權，其可降低營運成本。 
- **高可用性**：您不僅受益於 Azure 基礎結構的內建虛擬機器可用性 (正常運作時間據稱高達 99.99%)，也可以利用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 高可用性選項，例如容錯移轉叢集執行個體和 Always On 可用性群組。 
- **對資料庫應用程式的風險很低**：藉由維護與舊版資料庫相同層級的資料庫相容性，現有的資料庫應用程式會受到保護，以防止可能造成不利影響的功能和效能變更。 只有在應用程式需要使用由較新資料庫相容性設定所管制的功能時，才需要完整的重新認證。 如需詳細資訊，請參閱[相容性憑證](../../database-engine/install-windows/compatibility-certification.md)。

### <a name="considerations"></a>考量

- **管理能力**：您仍然必須管理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 與作業系統軟體。 
- **網路**：您必須設定虛擬機器，使其與您的網路和 Active Directory 基礎結構整合，這會增加額外的複雜度。 
- **共用儲存體 FCI**：Azure 虛擬機器僅支援使用儲存空間直接存取或進階檔案共用的容錯移轉叢集執行個體，不支援使用共用儲存體的容錯移轉叢集執行個體。 因此，Azure 虛擬機器只有在使用 Windows Server 2012 或更新版本時，才會支援容錯移轉叢集執行個體。
- **調整規模時停機**：變更 CPU 和儲存體資源時會出現停機。 
- **大小限制**：雖然 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體可以支援所需數量的資料庫，但單一 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的所有資料庫總共累計為 256 TB，而不是內部部署 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的 524 PB。 

### <a name="resources"></a>資源

[SQL Server VM 概觀](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-server-iaas-overview)       
[選擇 Azure SQL 選項](/azure/sql-database/sql-database-paas-vs-sql-server-iaas)       
[將 SQL Server 移轉到 Azure VM](/azure/virtual-machines/windows/sql/virtual-machines-windows-migrate-sql)       
[免費的延伸安全性更新以依現況移轉到 Azure](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-server-2008-eos-extend-support)       
[延伸安全性更新 (ESU) 概觀](sql-server-extended-security-updates.md)       
[詳細的 ESU 常見問題集](https://www.microsoft.com/cloud-platform/extended-security-updates)       
[SQL 虛擬機器自動修補](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-automated-patching)       
[SQL 虛擬機器自動備份](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-automated-backup-v2)       
[SQL 虛擬機器高可用性](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-high-availability-dr)       
[SQL 虛擬機器常見問題集](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-server-iaas-faq)       

## <a name="azure-sql-database-single-database"></a>Azure SQL Database 單一資料庫

如果您想要卸載維護、降低成本，並讓未來不再需要升級，您可以將工作負載移至 [Azure SQL Database 單一資料庫](/azure/sql-database/sql-database-single-database)。 此選項最適用於想要使用最新穩定 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 功能，且開發與行銷有時間限制的現代化雲端應用程式。 

### <a name="benefits"></a>優點

- **成本**：單一資料庫可能符合成本效益，因為已卸載硬體、軟體和維護，且您可以按秒或小時的使用量付費。 
- **彈性**：單一資料庫特別適合針對雲端設計的應用程式使用，因為對於此類應用程式來說，開發人員的生產力和解決方案上市時間快慢至關重要，或是需要外部存取。  
- **常用功能**：提供最常使用的 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 功能，但沒有像 SQL 受控執行個體那麼多。  
- **快速部署**：您可以快速部署單一資料庫。 
- **延展性**：您可以視業務需求快速輕鬆地擴大和縮小，因此提供額外的節省成本效益。 
- **可用性**：服務成本包含儲存體和高可用性，並保證正常運作時間達 99.995%。  
- **自動化**：修補和備份會自動進行，因此為您省下寶貴的維護時間。  
- **Intelligent Insights**：利用內建的智慧分析，取得您資料庫效能的見解。  
- **無版本**：[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 沒有版本，這表示您一律會使用最新版本，而無須擔心升級或停機。 此外，您一律會使用最新且最高的版本，其中包含已事先發行到雲端的最新穩定功能。
- **對資料庫應用程式的風險很低**：藉由維護與內部部署資料庫相同層級的資料庫相容性，現有的應用程式會受到保護，以防止可能造成不利影響的功能和效能變更。 只有在應用程式需要使用由較新資料庫相容性設定所管制的功能時，才需要完整的重新認證。 如需詳細資訊，請參閱[相容性憑證](../../database-engine/install-windows/compatibility-certification.md)。

### <a name="considerations"></a>考量

- **有限移轉選項**：您一次只能移轉單一資料庫，而不是整個執行個體。   
- **功能限制**：雖然提供最常使用的 Azure SQL Database 功能，但單一資料庫的功能集並不如 Azure SQL 受控執行個體或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 一樣完整。 
- **Transact-SQL 差異**：單一資料庫與內部部署 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之間有一些 [!INCLUDE[tsql](../../includes/tsql-md.md)] (T-SQL) 差異。 
- **大小限制**：相較於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的 524 PB 大小，單一資料庫的資料庫大小上限為 100 TB。 
- **維護時間**：不保證確切的維護時間，但近乎透明。 

### <a name="resources"></a>資源

[Azure SQL Database 概觀](/azure/sql-database/sql-database-technical-overview)       
[選擇 Azure SQL 選項](/azure/sql-database/sql-database-paas-vs-sql-server-iaas)       
[SQL Database 功能比較](/azure/sql-database/sql-database-features)       
[將 SQL Server 移轉到單一資料庫](/azure/sql-database/sql-database-single-database-migrate)       
[更廣泛的移轉程序](/azure/cloud-adoption-framework/migrate/expanded-scope/sql-migration)       
[單一資料庫的 T-SQL 差異](/azure/sql-database/sql-database-transact-sql-information)       
[vCore](/azure/sql-database/sql-database-vcore-resource-limits-single-databases) 和 [DTU](/azure/sql-database/sql-database-dtu-resource-limits-single-databases) 資源限制       
[Intelligent Insights](/azure/sql-database/sql-database-intelligent-insights)       

工具：
- [資料移轉小幫手](../../dma/dma-overview.md)
- [Database Migration Service](/azure/dms/dms-overview)

## <a name="sql-managed-instance"></a>SQL 受控執行個體

如果您想要利用卸載維護和成本，但發現 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 單一資料庫的功能集太過侷限，則可移至 [SQL 受控執行個體](/azure/sql-database/sql-database-managed-instance)。 受控執行個體與內部部署 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 非常相似，因此不必擔心硬體故障或修補的問題。 受控執行個體是具有一組共用資源的系統和使用者資料庫集合，可隨即轉移，並可用於大多數的雲端移轉。 此選項最適用於想要在最少變更的情況下使用最新穩定 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 功能，且會移轉到雲端的新應用程式或現有內部部署應用程式。 

### <a name="benefits"></a>優點

- **成本**：您可以藉由卸載軟體和硬體維護來節省成本。  
- **隨即轉移**：您可以在最少或沒有資料庫變更的情況下，將整個 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 內部部署執行個體隨即轉移到受控執行個體 (包括所有資料庫)。 
- **功能**：受控執行個體的功能集與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的內部部署執行個體密切符合，例如跨資料庫查詢、異動複寫發佈和散發、SQL 作業排程，以及 CLR 支援。 
- **延展性**：受控執行個體中的所有資料庫會共用資源，且可以隨時擴大和縮小，而不會出現停機。   
- **自動化**：修補和備份會自動進行，因此為您省下寶貴的維護時間。  
- **可用性**：服務成本包含儲存體和高可用性，並保證正常運作時間達 99.99%。  
- **Intelligent Insights**：利用內建的智慧分析，取得您資料庫效能的見解。  
- **無版本**：[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 沒有版本，這表示您一律會使用最新版本，而無須擔心升級或停機。 此外，您一律會使用最新且最高的版本，其中包含已事先發行到雲端的最新穩定功能。
- **對資料庫應用程式的風險很低**：藉由維護與內部部署資料庫相同層級的資料庫相容性，現有的資料庫應用程式會受到保護，以防止可能造成不利影響的功能和效能變更。 只有在應用程式需要使用由較新資料庫相容性設定所管制的功能時，才需要完整的重新認證。 如需詳細資訊，請參閱[相容性憑證](../../database-engine/install-windows/compatibility-certification.md)。

### <a name="considerations"></a>考量

- **成本**：受控執行個體選項的成本可能比單一資料庫選項更高。  
- **Transact-SQL 差異**：單一資料庫與內部部署 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 之間有一些 [!INCLUDE[tsql](../../includes/tsql-md.md)] (T-SQL) 差異。  
- **部署**：部署受控執行個體可能需要比部署單一資料庫更多的時間。  
- **功能限制**：雖然受控執行個體與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 共用大部分的功能，但仍有一些功能不受支援。 
- **大小限制**：受控執行個體中所有資料庫的合併儲存體大小限制為 8 TB，而不是內部部署 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的 524 PB。  
- **網路**：受控執行個體的網路需求會為您的基礎結構增加額外複雜度，且需要 Azure ExpressRoute 或 VPN 閘道。
- **維護時間**：不保證確切的維護時間，但近乎透明。 

### <a name="resources"></a>資源

[SQL 受控執行個體概觀](/azure/sql-database/sql-database-managed-instance)       
[選擇 Azure SQL 選項](/azure/sql-database/sql-database-paas-vs-sql-server-iaas)       
[SQL Database 功能比較](/azure/sql-database/sql-database-features)       
[將 SQL Server 移轉至 Azure SQL 受控執行個體](/azure/sql-database/sql-database-managed-instance-migrate)       
[更廣泛的移轉程序](/azure/cloud-adoption-framework/migrate/expanded-scope/sql-migration)       

工具：
- [資料移轉小幫手](../../dma/dma-overview.md)
- [Database Migration Service](/azure/dms/dms-overview)

## <a name="non-sql-options"></a>非 SQL 選項

針對某些類型的應用程式，您也可考慮使用非關聯式或 NoSQL 解決方案，例如 Azure Cosmos DB 或 Azure 表格儲存體。

### <a name="azure-cosmos-db"></a>Azure Cosmos DB

若現代化應用程式、可調式應用程式、行動應用程式及 Web 應用程式使用 JSON 資料，且需要兼具強大的查詢及交易資料處理功能，可以考慮使用 Azure Cosmos DB。 如需詳細資訊，請參閱 [Cosmos DB](https://azure.microsoft.com/services/cosmos-db/)。 如需匯入資料的資訊，請參閱[將資料匯入 Cosmos DB](/azure/cosmos-db/import-data/)。

Azure Cosmos DB 具有下列優點：
- 您的文件會編製索引，讓您可以使用熟悉的 SQL 語法加以查詢。
- 資料庫無須設定結構描述。
- 您無須重建索引，就可將屬性加入文件中。
- 資料庫引擎內就能直接提供您 JSON 及 JavaScript 支援。
- 除可獲得地理空間資料的原生支援之外，還可與其他 Azure 服務整合，包括 Azure 搜尋、HDInsight 及資料 Factory。
- 專用的輸送量層級讓儲存體有低延遲、高效能的表現。

### <a name="azure-table-storage"></a>Azure 表格儲存體

若需要價格實惠的解決方案來儲存以 PB 計的半結構化資料，則可考慮使用 Azure 表格儲存體。 如需詳細資訊，請參閱 [資料表儲存體](https://azure.microsoft.com/services/storage/tables/)。

Azure 表格儲存體具有下列優點：
- 您無須將資料下線，就能持續改進您的應用程式與資料表結構描述。
- 您無須分區化您的資料集，就能擴大規模。
- 異地備援支援可將您的資料複寫到多個區域。

## <a name="lifecycle-dates"></a>生命週期日期

下表提供 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 產品的大約生命週期日期。 如需詳細資料和正確性，請參閱 [Microsoft 週期原則](https://support.microsoft.com/hub/4095338/microsoft-lifecycle-policy)頁面。 

| **版本**     | **發行年份** | **主要支援結束年份** | **延伸支援結束年份** |
| :---------------| :--------------- | :------------------------------ | :---------------------------- |
| [SQL Server 2019](https://support.microsoft.com/lifecycle/search?alpha=SQL%20Server%202019) | 2019 | 2025 | 2030 |
| [SQL Server 2017](https://support.microsoft.com/lifecycle/search?alpha=SQL%20Server%202017) | 2017 | 2022 | 2027 |
| [SQL Server 2016](https://support.microsoft.com/lifecycle/search?alpha=SQL%20Server%202016) | 2016 | 2021 | 2026 |
| [SQL Server 2014](https://support.microsoft.com/lifecycle/search?alpha=SQL%20Server%202014) | 2014 | 2019 | 2024 |
| [SQL Server 2012](https://support.microsoft.com/lifecycle/search?alpha=SQL%20Server%202012) | 2012 | 2017 | 2022 |
| [SQL Server 2008 R2](https://support.microsoft.com/lifecycle/search?alpha=SQL%20Server%202008%20R2) | 2010 | 2012 | [2019](https://www.microsoft.com/sql-server/sql-server-2008) |
| [SQL Server 2008](https://support.microsoft.com/lifecycle/search?alpha=SQL%20Server%202008) | 2008 | 2012 | [2019](https://www.microsoft.com/sql-server/sql-server-2008) |
| [SQL Server 2005](https://support.microsoft.com/lifecycle/search?alpha=SQL%20Server%202005) | 2006 | 2011 | [2016](https://www.microsoft.com/sql-server/sql-server-2005) |
| [SQL Server 2000](https://support.microsoft.com/lifecycle/search?alpha=SQL%20Server%202000) | 2000 | 2005 | [2013](/archive/blogs/cdnitmanagers/sql-server-2000-end-of-support-april-2013) |

> [!IMPORTANT]
> 如果此表格與 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 週期頁面之間有任何不一致，則 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 週期會取代此表格，因為此表格僅供大致參考之用。  

## <a name="next-steps"></a>後續步驟  
[SQL Server 2019](https://www.microsoft.com/sql-server/sql-server-2019)   
[不再支援 SQL Server 2005](https://www.microsoft.com/sql-server/sql-server-2005)   
[SQL Server 2008 終止支援](https://www.microsoft.com/cloud-platform/windows-sql-server-2008)   
[延伸安全性更新 (ESU) 概觀](sql-server-extended-security-updates.md)   
[免費的延伸安全性更新 (ESU) 以依現況移轉到 Azure](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-server-2008-eos-extend-support)   
[SQL Server VM 概觀](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-server-iaas-overview)   
[Azure SQL Database 概觀](/azure/sql-database/sql-database-technical-overview)