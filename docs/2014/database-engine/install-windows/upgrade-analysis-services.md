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
ms.openlocfilehash: cdd9e34e57694efc1234a2f0245833596644cb73
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68889188"
---
# <a name="upgrade-analysis-services"></a>升級 Analysis Services
  使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式來升級 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 如需有關以 SharePoint [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]模式升級的詳細資訊，請參閱[升級 PowerPivot for SharePoint](upgrade-power-pivot-for-sharepoint.md)。 如需升級現有 SQL Server 實例的詳細資訊，請參閱[使用安裝精靈升級至 SQL Server 2014 &#40;安裝程式&#41;](upgrade-sql-server-using-the-installation-wizard-setup.md)。  
  
## <a name="known-upgrade-issues"></a>已知的升級問題  
 在升級至[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]之前，請檢查下列事項：  
  
-   [SQL Server 2014 版本](https://go.microsoft.com/fwlink/?LinkID=296445)資訊。  
  
-   若要瞭解[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]哪些特性和功能已停止、已被取代或變更，請參閱[Analysis Services 回溯相容性](https://docs.microsoft.com/analysis-services/analysis-services-backward-compatibility)。  
  
## <a name="pre-upgrade-checklist"></a>升級前檢查清單  
 升級之前，請先檢閱下列資訊：  
  
-   [支援的版本與版本升級](supported-version-and-edition-upgrades.md)  
  
-   [Hardware and Software Requirements for Installing SQL Server 2014](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)  
  
-   [檢查 System Configuration Checker 的參數](check-parameters-for-the-system-configuration-checker.md)  
  
-   [SQL Server 安裝的安全性考量](../../sql-server/install/security-considerations-for-a-sql-server-installation.md)  
  
-   [備份與還原 Analysis Services 資料庫](https://docs.microsoft.com/analysis-services/multidimensional-models/backup-and-restore-of-analysis-services-databases)  
  
-   [使用 Upgrade Advisor 來準備升級](../../sql-server/install/use-upgrade-advisor-to-prepare-for-upgrades.md)  
  
## <a name="upgrading-analysis-services"></a>升級 Analysis Services  
 您可以選擇許多方式來升級伺服器和資料：  
  
-   **就地升級**會以[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]程式檔案取代現有的程式檔案。 資料庫會保持在相同的位置。 程式資料夾會更新以反映新的名稱。  
  
-   **並存升級**是指[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]在具有現有 Analysis Services 實例的同一部電腦上的新安裝。 您可以將資料庫移至相同電腦上的新執行個體，然後解除安裝舊版 (如果不再使用它的話)。  
  
-   您也可以在新的硬體上安裝 Analysis Services，然後將現有的資料庫移轉至該伺服器。  
  
## <a name="in-place-upgrade"></a>就地升級  
 您可以將現有的[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]實例升級至[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ，而在升級過程中，會將現有的資料庫從舊的實例自動遷移到新的實例。 由於這兩個版本之間的中繼資料和二進位資料是相容的，所以在您升級之後將會保留資料，而且不必手動移轉資料。  
  
 若要升級現有的執行個體，請執行安裝程式，並指定現有執行個體的名稱做為新執行個體的名稱。  
  
## <a name="upgrading-databases"></a>升級資料庫  
 在舊版 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中建立的資料庫會使用舊的資料庫相容性層級設定，在升級的伺服器上執行。 在下列版本中建立的資料庫，其資料庫相容性層級為 105。 如果您想要使用的功能需要更新的資料庫相容性層級，就可以變更相容性層級。 否則，您可以使用原始設定，在升級的伺服器上執行資料庫。 如需詳細資訊，請參閱[將多維度資料庫的相容性層級設定 &#40;Analysis Services&#41;](https://docs.microsoft.com/analysis-services/multidimensional-models/compatibility-level-of-a-multidimensional-database-analysis-services)。  
  
-   [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]  
  
-   [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]  
  
-   [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]  
  
-   [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server 2014 版本所支援的功能](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)   
 [規劃 SQL Server 安裝](../../sql-server/install/planning-a-sql-server-installation.md)   
 [瞭解 Microsoft OLAP 架構](https://docs.microsoft.com/analysis-services/multidimensional-models/olap-physical/understanding-microsoft-olap-architecture)   
 [升級 PowerPivot for SharePoint](upgrade-power-pivot-for-sharepoint.md)   
 [以多維度和資料採礦模式安裝 Analysis Services](../../sql-server/install/install-analysis-services-in-multidimensional-and-data-mining-mode.md)   
 [PowerPivot for SharePoint 2010 安裝](../../sql-server/install/powerpivot-for-sharepoint-2010-installation.md)  
  
  
