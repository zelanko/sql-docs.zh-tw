---
title: 使用 Upgrade Advisor 來準備升級 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Upgrade Advisor [SQL Server]
- upgrading SQL Server, Upgrade Advisor
- upgrading SQL Server, preparing to upgrade
- SQL Server Upgrade Advisor
- analyzing installations for upgrading [SQL Server]
ms.assetid: d85b0833-ddeb-42e3-9397-97ea60d521b7
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ce60db3b720b046c44d7507d3164c2f2e6c9173f
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/23/2019
ms.locfileid: "66091259"
---
# <a name="use-upgrade-advisor-to-prepare-for-upgrades"></a>使用 Upgrade Advisor 來準備升級
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Upgrade Advisor 可以協助您完成升級到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 的相關準備工作。 Upgrade Advisor 會分析已安裝的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 舊版元件，然後產生報告，以指出在您升級之前或之後要修正的問題。  
  
## <a name="how-upgrade-advisor-works"></a>Upgrade Advisor 如何運作  
 當您執行 Upgrade Advisor 時，Upgrade Advisor 首頁會出現。 您可以從首頁執行下列工具：  
  
-   Upgrade Advisor 分析精靈  
  
-   Upgrade Advisor 報表檢視器  
  
-   Upgrade Advisor 說明  
  
 第一次使用 Upgrade Advisor 時，請執行 Upgrade Advisor Analysis 精靈分析 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 元件。 當精靈完成分析時，請在 Upgrade Advisor 報表檢視器中檢視產生的報表。 每一份報告都會提供 Upgrade Advisor 說明資訊的連結，以協助您修正或降低已知問題的影響。  
  
## <a name="upgrade-advisor-analysis"></a>Upgrade Advisor 分析  
 Upgrade Advisor 會分析下列 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 元件：  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]  
  
 分析會檢查可以存取的物件，例如指令碼、預存程序、觸發程序和追蹤檔案。 Upgrade Advisor 無法分析桌面應用程式或加密的預存程序。  
  
 輸出為 XML 報表的形式。 請使用 Upgrade Advisor 報表檢視器來檢視 XML 報表。  
  
> [!NOTE]  
>  報表可能包含「其他升級問題」項目。 這個項目會連結到 Upgrade Advisor 不會偵測，但您的伺服器或應用程式中可能存在的問題清單。 您應該檢閱無法偵測到的問題清單，並判斷您是否因為這些無法偵測到的問題，而必須變更伺服器或應用程式。  
  
## <a name="how-to-install-and-run-upgrade-advisor"></a>如何安裝和執行 Upgrade Advisor  
 安裝 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Upgrade Advisor 的位置取決於您要分析的項目。 Upgrade Advisor 支援所有支援元件 ([!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 除外) 的遠端分析。 如果不要掃描 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 的執行個體，可以將 Upgrade Advisor 安裝在可連接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體，且符合 Upgrade Advisor 必要條件的任何電腦上。 如需詳細資訊，請參閱 [支援的版本與版本升級](../../database-engine/install-windows/supported-version-and-edition-upgrades.md)。 如果您要掃描 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]的執行個體，則必須將 Upgrade Advisor 安裝在報表伺服器上。  
  
 功能套件提供 Upgrade Advisor。  
  
 安裝及執行 Upgrade Advisor 的先決條件如下：  
  
-   [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)] SP2、Windows 7 SP1 及 [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1。  
  
-   Windows Installer 從版本 4.5 開始。 您可以安裝 Windows Installer 從[Windows Installer 網站](https://go.microsoft.com/fwlink/?LinkId=49112)。  
  
-   Microsoft .NET Framework 4。 .NET framework 4 是位於[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]產品媒體，以及從[.NET Framework 4 下載頁面](https://go.microsoft.com/fwlink/?LinkId=209895)。  
  
    -   若要從 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 媒體安裝 .NET Framework 4，請找出光碟機的根目錄。 然後，在 \redist 資料夾上按兩下滑鼠按鈕後於 DotNetFrameworks 資料夾上再按兩下滑鼠按鈕，然後執行 dotNetFx40_Full_x86_x64.exe (32 位元作業系統或 64 位元作業系統)。  
  
 若要從網路安裝 Upgrade Advisor，請在下載網頁上按一下 [下載] 按鈕。 接著您可立即執行安裝，或是儲存 SQLUA.msi 檔，並於稍後再執行。 如果要從產品光碟安裝，請直接從產品光碟執行 SQLUA.msi。  
  
 安裝 Upgrade Advisor 之後，您可以開啟從**啟動**功能表：  
  
-   按一下 **開始**，指向**所有程式**，指向[!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)]，然後按一下 **[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Upgrade Advisor**。  
  
 如需詳細資訊，請參閱 Upgrade Advisor 下載以及 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 版本資訊中的 Upgrade Advisor 文件。  
  
## <a name="see-also"></a>另請參閱  
 [使用多個版本和 SQL Server 執行個體](../../../2014/sql-server/install/work-with-multiple-versions-and-instances-of-sql-server.md)   
 [支援的版本與版本升級](../../database-engine/install-windows/supported-version-and-edition-upgrades.md)   
 [回溯相容性](../../../2014/getting-started/backward-compatibility.md)  
  
  
