---
title: 使用 SQL Server 的多個版本和執行個體 | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- concurrent installations [SQL Server]
- versions [SQL Server], multiple
- side-by-side installations [SQL Server]
- multiple SQL Server component versions
- installing SQL Server, side-by-side installations
- Setup [SQL Server], side-by-side installations
- 64-bit edition [SQL Server]
- 32-bit edition [SQL Server]
- editions [SQL Server], side-by-side installations
ms.assetid: 93acefa8-bb41-4ccc-b763-7801f51134e0
caps.latest.revision: 63
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 920e7295d56f3b7bfadf91a9532f638911535d44
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37246368"
---
# <a name="work-with-multiple-versions-and-instances-of-sql-server"></a>使用 SQL Server 的多個版本和執行個體
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支援同一部電腦上的多個 [!INCLUDE[ssDE](../../includes/ssde-md.md)]、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]和 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 執行個體。 您也可以升級舊版的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，或在已安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 舊版的電腦上安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 如需支援的升級案例，請參閱 [支援的版本與版本升級](../../database-engine/install-windows/supported-version-and-edition-upgrades.md)。  
  
## <a name="version-components-and-numbering"></a>版本元件和編號  
 下列概念對於了解 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]並存執行個體的行為很有幫助。  
  
 適用於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的標準產品版本格式為 MM.nn.bbbb.rr，每一個區段定義如下：  
  
 MM - 主要版本  
  
 nn - 次要版本  
  
 bbbb - 組建編號  
  
 rr - 組建修訂編號  
  
 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的每一個主要或次要版本中，版本號碼都會遞增，以便與之前的版本區別。 這項版本變更可用於許多用途。 其中包括在使用者介面中顯示版本資訊、控制升級期間如何取代檔案、套用 Service Pack，同時也是在後續版本之間區分功能的一項機制。  
  
### <a name="components-shared-by-all-versions-of-includessnoversionincludesssnoversion-mdmd"></a>所有版本共用的元件 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 所有已安裝之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]版本的所有執行個體會共用某些元件。 當您在同一部電腦上並存安裝不同版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 時，這些元件會自動升級到最新的版本。 當解除安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的最後一個執行個體時，通常會自動解除安裝這類元件。  
  
 範例： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 和 Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] VSS Writer。  
  
### <a name="components-shared-across-all-instances-of-the-same-major-version-of-includessnoversionincludesssnoversion-mdmd"></a>在相同主要版本的所有執行個體之間共用的元件 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 具有相同主要版本的版本會在所有執行個體之間共用某些元件。 如果在升級期間選取共用元件，現有的元件都會升級到最新的版本。  
  
 範例： [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]、 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]、 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]及 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 線上叢書。  
  
### <a name="components-shared-across-minor-versions"></a>次要版本之間共用的元件  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 具有相同 major.minor 版本共用元件的版本。  
  
 範例：安裝程式支援檔案。  
  
### <a name="components-specific-to-an-instance-of-includessnoversionincludesssnoversion-mdmd"></a>執行個體特有的元件 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 某些 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 元件或服務是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體所特有， 也可感知執行個體。 這些元件或服務也會與裝載它們的執行個體共用相同的版本，並專門用於該執行個體。  
  
 範例： [!INCLUDE[ssDE](../../includes/ssde-md.md)]、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]和 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]。  
  
### <a name="components-that-are-independent-of-the-includessnoversionincludesssnoversion-mdmd-versions"></a>與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本無關的元件  
 某些元件會在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝期間安裝，但是與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的版本無關。 這些元件可能會在主要版本之間共用，或是由所有的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本共用。  
  
 範例：Microsoft Sync Framework、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact。  
  
 如需詳細資訊[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Compact 安裝，請參閱 <<c2> [ 從安裝精靈安裝 SQL Server 2014&#40;安裝&#41;](../../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md)。</c2> 如需如何解除安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact 的詳細資訊，請參閱[解除安裝現有的 SQL Server 執行個體 &#40;安裝程式&#41;](../../../2014/sql-server/install/uninstall-an-existing-instance-of-sql-server-setup.md)。  
  
## <a name="using-includessnoversionincludesssnoversion-mdmd-side-by-side-with-previous-versions-of-includessnoversionincludesssnoversion-mdmd"></a>並存使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 與舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 您可以在已執行舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的電腦上安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 如果預設執行個體已存在於電腦上， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 必須安裝成具名執行個體。  
  
> [!CAUTION]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SysPrep 不支援在同一部電腦上並存安裝 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 的備妥執行個體和舊版的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 例如，您無法在並存準備 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 執行個體和備妥的 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]執行個體。 不過，您可以在同一部電腦上合併安裝屬於相同主要版本之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的多個備妥執行個體。 如需詳細資訊，請參閱＜ [Considerations for Installing SQL Server Using SysPrep](../../database-engine/install-windows/considerations-for-installing-sql-server-using-sysprep.md)＞。  
>   
>  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 無法在執行 Windows Server 2008 R2 Server Core SP1 的電腦上，與舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 並存安裝。 如需有關 Server Core 安裝的詳細資訊，請參閱[在 Server Core 上安裝 SQL Server 2014](../../database-engine/install-windows/install-sql-server-on-server-core.md)。  
  
 下表顯示對 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]的並存支援：  
  
|現有的執行個體 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]|並存支援|  
|--------------------------------------------------|----------------------------|  
|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] (32 位元)|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] (32 位元)<br /><br /> [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] (64 位元) [!INCLUDE[vcprx64](../../includes/vcprx64-md.md)]<br /><br /> [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] (32 位元)<br /><br /> [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] (64 位元) [!INCLUDE[vcprx64](../../includes/vcprx64-md.md)]<br /><br /> [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] (32 位元)<br /><br /> [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] (64 位元) [!INCLUDE[vcprx64](../../includes/vcprx64-md.md)]<br /><br /> [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] (32 位元)<br /><br /> [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] (64 位元) [!INCLUDE[vcprx64](../../includes/vcprx64-md.md)]<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] (32 位元)<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] (64 位元) [!INCLUDE[vcprx64](../../includes/vcprx64-md.md)]|  
|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] (64 位元) [!INCLUDE[vcprx64](../../includes/vcprx64-md.md)]|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] (32 位元)<br /><br /> [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] (64 位元) [!INCLUDE[vcprx64](../../includes/vcprx64-md.md)]<br /><br /> [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] (32 位元)<br /><br /> [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] (64 位元) [!INCLUDE[vcprx64](../../includes/vcprx64-md.md)]<br /><br /> [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] (32 位元)<br /><br /> [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] (64 位元) [!INCLUDE[vcprx64](../../includes/vcprx64-md.md)]<br /><br /> [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] (32 位元)<br /><br /> [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] (64 位元) [!INCLUDE[vcprx64](../../includes/vcprx64-md.md)]<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] (32 位元)<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] (64 位元) [!INCLUDE[vcprx64](../../includes/vcprx64-md.md)]|  
  
## <a name="preventing-ip-address-conflicts"></a>防止 IP 位址衝突  
 當 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 容錯移轉叢集執行個體與 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]的獨立執行個體並行安裝時，務必避免 IP 位址發生 TCP 通訊埠編號衝突。 通常兩個 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體同樣設定為使用預設 TCP 通訊埠 (1433) 時，就會發生衝突。 為避免發生衝突，請將其中一個執行個體設定為使用非預設固定通訊埠。 在獨立執行個體上設定固定通訊埠通常最為簡單。 將 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 設定為使用不同的通訊埠，通常就能防止發生非預期的 IP 位址/TCP 通訊埠衝突，以免造成 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 容錯移轉叢集執行個體失敗而移轉至待命節點時，執行個體無法啟動。  
  
## <a name="see-also"></a>另請參閱  
 [硬體和 Software Requirements for Installing SQL Server 2014](hardware-and-software-requirements-for-installing-sql-server.md)   
 [從安裝精靈安裝 SQL Server 2014&#40;安裝程式&#41;](../../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md)   
 [支援的版本與版本升級](../../database-engine/install-windows/supported-version-and-edition-upgrades.md)   
 [升級到 SQL Server 2014](../../database-engine/install-windows/upgrade-sql-server.md)   
 [SQL Server 2014 各版本所支援的功能](../../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md)   
 [回溯相容性](../../../2014/getting-started/backward-compatibility.md)   
 [使用 Upgrade Advisor 來準備升級](../../../2014/sql-server/install/use-upgrade-advisor-to-prepare-for-upgrades.md)  
  
  
