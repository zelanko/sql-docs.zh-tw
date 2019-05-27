---
title: 執行 Upgrade Advisor （使用者介面） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Upgrade Advisor Report Viewer
- Upgrade Advisor [SQL Server], running
- launching Upgrade Advisor
- Upgrade Advisor Analysis Wizard
- starting Upgrade Advisor
- SQL Server Upgrade Advisor, running
ms.assetid: 7f47c9b3-88d3-43d6-837e-f157b49a55ac
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 5aecaea9bef359ad24aebbd20dd5e9547497043b
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/23/2019
ms.locfileid: "66092451"
---
# <a name="running-upgrade-advisor-user-interface"></a>執行 Upgrade Advisor (使用者介面)
  在升級規劃期間，您可以執行 Upgrade Advisor 來分析本機或遠端元件。 Upgrade Advisor 會針對分析的每個元件和執行個體產生一份報表。  
  
> [!IMPORTANT]  
>  Upgrade Advisor 不會分析 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 的遠端執行個體。 若要分析 [!INCLUDE[ssRS](../../includes/ssrs.md)] 執行個體，您必須將 Upgrade Advisor 安裝在已安裝 [!INCLUDE[ssRS](../../includes/ssrs.md)] 的電腦上。  
>   
>  若要分析[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Integration Services，您必須擁有[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssDE](../../includes/ssde-md.md)]安裝和[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]安裝在同一部電腦上。  
  
## <a name="running-the-upgrade-advisor-analysis-wizard"></a>執行 Upgrade Advisor 分析精靈  
 執行 Upgrade Advisor 分析精靈具有六個步驟：  
  
1.  從 Upgrade Advisor 開始頁面啟動精靈。  
  
2.  識別要分析的伺服器和元件。  
  
3.  蒐集驗證資訊。  
  
4.  根據元件類型，蒐集其他參數。  
  
5.  分析選取的元件。  
  
6.  產生升級問題的報表。  
  
 如需有關 Upgrade Advisor 分析精靈的詳細資訊，請參閱[How to:執行 Upgrade Advisor 分析精靈](../../../2014/sql-server/install/how-to-run-the-upgrade-advisor-analysis-wizard.md)。  
  
 所需的每個步驟的特定資訊，請參閱[Upgrade Advisor 使用者介面參考](../../../2014/sql-server/install/upgrade-advisor-user-interface-reference.md)。  
  
## <a name="running-the-upgrade-advisor-report-viewer"></a>執行 Upgrade Advisor 報表檢視器  
 您可以使用 Upgrade Advisor 報表檢視器來檢視 Upgrade Advisor 分析精靈所產生的報表。 載入報表時，您可以依據下列因數來篩選報表的元件：  
  
-   所有問題  
  
-   所有升級的問題  
  
-   升級前的問題  
  
-   所有移轉的問題  
  
-   已解決的問題  
  
-   未解決的問題  
  
 如需使用報表檢視器的逐步指示，請參閱下列主題：  
  
-   [如何：檢視 Upgrade Advisor 報表](../../../2014/sql-server/install/how-to-view-an-upgrade-advisor-report.md)  
  
-   [如何：篩選報表](../../../2014/sql-server/install/how-to-filter-reports.md)  
  
-   [如何：將報表匯出](../../../2014/sql-server/install/how-to-export-reports.md)  
  
## <a name="see-also"></a>另請參閱  
 [如何：執行 Upgrade Advisor 分析精靈](../../../2014/sql-server/install/how-to-run-the-upgrade-advisor-analysis-wizard.md)   
 [Upgrade Advisor 使用者介面參考](../../../2014/sql-server/install/upgrade-advisor-user-interface-reference.md)   
 [解決升級問題](../../../2014/sql-server/install/resolving-upgrade-issues.md)   
 [使用升級建議程式](../../../2014/sql-server/install/working-with-upgrade-advisor.md)  
  
  
