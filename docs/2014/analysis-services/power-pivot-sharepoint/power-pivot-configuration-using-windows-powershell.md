---
title: 使用 Windows PowerShell 的 PowerPivot 設定 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 4d83e53e-04f1-417d-9039-d9e81ae0483d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9282fce8e0004495ae8c10b0b3f75fec205d6b34
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "72782811"
---
# <a name="powerpivot-configuration-using-windows-powershell"></a>使用 Windows PowerShell 的 PowerPivot 組態
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 包括您可以用來設定 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]安裝的 Windows PowerShell 指令程式。 若要使用 PowerShell 完整設定安裝，需要使用 SharePoint 指令程式和 PowerPivot for SharePoint 指令程式。 大部分組態都可以使用其中一項 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 工具來完成。 如需這些工具的詳細資訊，請參閱[PowerPivot 組態工具](power-pivot-configuration-tools.md)。  
  
> [!IMPORTANT]  
>  如果是 SharePoint 2010 伺服器陣列，您必須先安裝 SharePoint 2010 SP1，才可設定 PowerPivot for SharePoint 或使用 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 資料庫伺服器的 SharePoint 伺服器陣列。 如果您尚未安裝該 Service Pack，請在開始設定伺服器之前先加以安裝。  
  
## <a name="benefits-of-configuring-powerpivot-for-sharepoint-using-powershell"></a>使用 PowerShell 設定 PowerPivot for SharePoint 的優點  
 您可以建立 Windows PowerShell (.ps1) 檔案，將組態工作自動化。 如果您需要可以在任何伺服器上執行的指令碼式安裝和設定步驟，建議使用此方法。 您可以需要此種指令碼做為災難復原計畫的一部分，才能在發生硬體故障時重建伺服器。  
  
## <a name="view-a-list-of-the-powerpivot-cmdlets-on-a-server"></a>在伺服器上檢視 PowerPivot 指令程式的清單  
 若要查看[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] Cmdlet 的內容和範例，請參閱[PowerPivot for SharePoint 的 PowerShell 參考](/sql/analysis-services/powershell/powershell-reference-for-power-pivot-for-sharepoint)。  
  
 使用 PowerShell 檢視 PowerPivot 指令程式的清單：  
  
1.  使用 [以系統管理員身分執行]**** 選項，開啟 SharePoint 管理命令介面。  
  
2.  輸入下列命令：  
  
    ```powershell
    Get-Help *powerpivot*  
    ```  
  
     您應該查看在指令程式名稱中包含 PowerPivot 的指令程式清單。 例如 `Get-PowerPivotServiceApplication` 。 可用的指令程式數目取決於您使用的 Analysis Services 版本。  
  
    -   SQL Server 2012 SP1 Analysis Services 伺服器附帶的 10 個指令程式是在 SharePoint 模式和 SharePoint 2013 中進行設定。 2012 SP1 版使用新的架構，允許 Analysis Server 從 SharePoint 伺服器陣列外部執行，而且所需的 Windows PowerShell 指令程式管理更少。  
  
    -   SQL Server 2012 Analysis Services 伺服器附帶的 17 個指令程式是在 SharePoint 模式和 SharePoint 2010 中進行設定。  
  
     如果清單中未傳回任何命令，或您看到類似 "`get-help could not find *powerpivot* in a help file in this session.`" 的錯誤訊息，請參閱本主題中的下一節，以取得有關如何在伺服器上啟用 PowerPivot Cmdlet 的指示。  
  
     所有指令程式都有線上說明。 下列範例顯示如何檢視 `New-PowerPivotServiceApplication` 指令程式的線上說明：  
  
    ```powershell
    Get-Help new-powerpivotserviceapplication -Full  
    ```  
  
     或者，若只要檢視範例，影使用下列語法：  
  
    ```powershell
    Get-Help new-powerpivotserviceapplication -Example  
    ```  
  
## <a name="enable-powerpivot-cmdlets-on-a-server"></a>在伺服器上啟用 PowerPivot 指令程式  
 在您安裝 PowerPivot for SharePoint 並部署伺服器陣列方案之後，可以使用 PowerPivot 指令程式。 這些方案會在您執行 PowerPivot 組態工具時部署。 請依照下列步驟啟用指令程式：  
  
1.  使用 [以系統管理員身分執行]**** 選項，開啟 SharePoint 管理命令介面。  
  
2.  執行第一個 Cmdlet：  
  
    ```powershell
    Add-SPSolution -LiteralPath "C:\Program Files\Microsoft SQL Server\110\Tools\PowerPivotTools\ConfigurationTool\Resources\PowerPivotFarm.wsp"  
    ```  
  
     此指令程式會傳回方案的名稱、方案識別碼及 Deployed=False。 在下個步驟中，您將部署方案。  
  
3.  執行第二個 Cmdlet 部署方案：  
  
    ```powershell
    Install-SPSolution -Identity PowerPivotFarm.wsp -GACDeployment -Force  
    ```  
  
4.  關閉視窗。 再次使用 [以系統管理員身分執行]**** 選項重新開啟該視窗。  
  
## <a name="related-content"></a>相關內容  
 [管理中心的 PowerPivot 伺服器管理和設定](power-pivot-server-administration-and-configuration-in-central-administration.md)  
  
 [PowerPivot 設定工具](power-pivot-configuration-tools.md)  
  
 [PowerPivot for SharePoint 的 PowerShell 參考](/sql/analysis-services/powershell/powershell-reference-for-power-pivot-for-sharepoint)  
