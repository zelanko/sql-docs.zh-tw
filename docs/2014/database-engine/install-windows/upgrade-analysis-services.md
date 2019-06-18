---
title: 升級 Analysis Services | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- upgrading databases
- databases [Analysis Services], upgrading
- installing Analysis Services, side-by-side installations
- Analysis Services upgrades
- Analysis Services upgrades, about upgrading Analysis Services
- SSAS, database migration
- upgrading Analysis Services
- installing Analysis Services, upgrading
- SSAS, upgrading
ms.assetid: a131d329-386e-4470-aaa9-ffcde4e5ec0c
author: Minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8bbec3cd552434070d76913f72812b302440bcdb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62775015"
---
# <a name="upgrade-analysis-services"></a>升級 Analysis Services
  使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式來升級 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 如需升級的詳細資訊[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]在 SharePoint 模式中，請參閱[升級 PowerPivot for SharePoint](upgrade-power-pivot-for-sharepoint.md)。 如需有關升級現有的 SQL Server 執行個體，請參閱 <<c0> [ 升級到使用的 SQL Server 2014 安裝精靈&#40;安裝&#41;](upgrade-sql-server-using-the-installation-wizard-setup.md)。</c0>  
  
## <a name="known-upgrade-issues"></a>已知的升級問題  
 在升級至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]之前，請檢閱下列文章：  
  
-   [SQL Server 2014 版本資訊](https://go.microsoft.com/fwlink/?LinkID=296445)。  
  
-   若要了解哪些[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]特性與功能已停用、 已被取代，或變更查看[Analysis Services Backward Compatibility](../../analysis-services/analysis-services-backward-compatibility.md)。  
  
## <a name="pre-upgrade-checklist"></a>升級前檢查清單  
 升級之前，請先檢閱下列資訊：  
  
-   [支援的版本與版本升級](supported-version-and-edition-upgrades.md)  
  
-   [安裝 SQL Server 2014 的硬體與軟體需求](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)  
  
-   [檢查 System Configuration Checker 的參數](check-parameters-for-the-system-configuration-checker.md)  
  
-   [SQL Server 安裝的安全性考量](../../sql-server/install/security-considerations-for-a-sql-server-installation.md)  
  
-   [備份與還原 Analysis Services 資料庫](../../analysis-services/multidimensional-models/backup-and-restore-of-analysis-services-databases.md)  
  
-   [使用 Upgrade Advisor 來準備升級](../../sql-server/install/use-upgrade-advisor-to-prepare-for-upgrades.md)  
  
## <a name="upgrading-analysis-services"></a>升級 Analysis Services  
 您可以選擇許多方式來升級伺服器和資料：  
  
-   **就地升級**現有的程式檔案的取代[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]程式檔案。 資料庫會保持在相同的位置。 程式資料夾會更新以反映新的名稱。  
  
-   A**並排顯示升級**新安裝的[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]具有現有 Analysis Services 執行個體在相同電腦上。 您可以將資料庫移至相同電腦上的新執行個體，然後解除安裝舊版 (如果不再使用它的話)。  
  
-   您也可以在新的硬體上安裝 Analysis Services，然後將現有的資料庫移轉至該伺服器。  
  
## <a name="in-place-upgrade"></a>就地升級  
 您可以將 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的現有執行個體升級到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] and, as part of the upgrade process, au的現有執行個體升級到matically migrate existing databases from the old instance 的現有執行個體升級到 the new instance. 由於這兩個版本之間的中繼資料和二進位資料是相容的，所以在您升級之後將會保留資料，而且不必手動移轉資料。  
  
 若要升級現有的執行個體，請執行安裝程式，並指定現有執行個體的名稱做為新執行個體的名稱。  
  
## <a name="upgrading-databases"></a>升級資料庫  
 在舊版 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中建立的資料庫會使用舊的資料庫相容性層級設定，在升級的伺服器上執行。 在下列版本中建立的資料庫，其資料庫相容性層級為 105。 如果您想要使用的功能需要更新的資料庫相容性層級，就可以變更相容性層級。 否則，您可以使用原始設定，在升級的伺服器上執行資料庫。 如需詳細資訊，請參閱 <<c0> [ 設定多維度資料庫的相容性層級&#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/compatibility-level-of-a-multidimensional-database-analysis-services.md)。</c0>  
  
-   [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]  
  
-   [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]  
  
-   [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]  
  
-   [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server 2014 各版本所支援的功能](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)   
 [規劃 SQL Server 安裝](../../sql-server/install/planning-a-sql-server-installation.md)   
 [了解 Microsoft OLAP 架構](../../analysis-services/multidimensional-models/olap-physical/understanding-microsoft-olap-architecture.md)   
 [升級 PowerPivot for SharePoint](upgrade-power-pivot-for-sharepoint.md)   
 [以多維度及資料採礦模式安裝 Analysis Services](../../sql-server/install/install-analysis-services-in-multidimensional-and-data-mining-mode.md)   
 [PowerPivot for SharePoint 2010 安裝](../../sql-server/install/powerpivot-for-sharepoint-2010-installation.md)  
  
  
