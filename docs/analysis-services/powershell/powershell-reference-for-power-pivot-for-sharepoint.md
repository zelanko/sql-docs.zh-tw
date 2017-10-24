---
title: "Power Pivot for SharePoint 的 PowerShell 參考 |Microsoft 文件"
ms.custom:
- SQL2016_New_Updated
ms.date: 11/16/2015
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: c01735a8-f919-48ad-8d74-35d75a18f821
caps.latest.revision: 11
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 39567e2b212761ac2dd726a1f8f33893a83f245c
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="powershell-reference-for-power-pivot-for-sharepoint"></a>Power Pivot for SharePoint 的 PowerShell 參考

[!INCLUDE[ssas-appliesto-sqlas-all](../../includes/ssas-appliesto-sqlas-all.md)]

  本節列出用來設定或管理 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 安裝的 PowerShell 指令程式。 如需啟用 Cmdlet 與檢視內建說明的詳細資訊，請參閱 [使用 Windows PowerShell 的 Power Pivot 組態](../../analysis-services/power-pivot-sharepoint/power-pivot-configuration-using-windows-powershell.md)。  

>[!NOTE] 
>這份文件可能包含過時的資訊和範例。 使用 Get-help cmdlet 取得最新。
  
## <a name="cmdlet-list"></a>指令程式清單  
 從 PowerShell 提示字元查看 Cmdlet 清單︰  
  
1.  使用 [以系統管理員身分執行] 選項，開啟 SharePoint 管理命令介面。  
  
2.  輸入下列命令： `Get-help *powerpivot*`  
  
|指令程式|支援的版本|  
|------------|------------------------|  
|[Get-PowerPivotServiceApplication 指令程式](../../analysis-services/powershell/get-powerpivotserviceapplication-cmdlet.md)|SharePoint 2013 &#124; SharePoint 2016|  
|[Get-PowerPivotSystemService 指令程式](../../analysis-services/powershell/get-powerpivotsystemservice-cmdlet.md)|SharePoint 2013 &#124; SharePoint 2016|  
|[Get-PowerPivotSystemServiceInstance 指令程式](../../analysis-services/powershell/get-powerpivotsystemserviceinstance-cmdlet.md)|SharePoint 2013 &#124; SharePoint 2016|  
|[New-PowerPivotServiceApplication 指令程式](../../analysis-services/powershell/new-powerpivotserviceapplication-cmdlet.md)|SharePoint 2013 &#124; SharePoint 2016|  
|[New-PowerPivotSystemServiceInstance 指令程式](../../analysis-services/powershell/new-powerpivotsystemserviceinstance-cmdlet.md)|SharePoint 2013 &#124; SharePoint 2016|  
|[Remove-PowerPivotServiceApplication 指令程式](../../analysis-services/powershell/remove-powerpivotserviceapplication-cmdlet.md)|SharePoint 2013 &#124; SharePoint 2016|  
|[Remove-PowerPivotSystemServiceInstance 指令程式](../../analysis-services/powershell/remove-powerpivotsystemserviceinstance-cmdlet.md)|SharePoint 2013 &#124; SharePoint 2016|  
|[Set-PowerPivotServiceApplication 指令程式](../../analysis-services/powershell/set-powerpivotserviceapplication-cmdlet.md)|SharePoint 2013 &#124; SharePoint 2016|  
|[Set-PowerPivotSystemService 指令程式](../../analysis-services/powershell/set-powerpivotsystemservice-cmdlet.md)|SharePoint 2013 &#124; SharePoint 2016|  
|[Update-PowerPivotSystemService 指令程式](../../analysis-services/powershell/update-powerpivotsystemservice-cmdlet.md)|SharePoint 2013 &#124; SharePoint 2016|  
  
 注意：下列 Cmdlet 只適用於 SharePoint 2010，不支援 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 。  
  
-   Get-PowerPivotEngineService  
  
-   Get-PowerPivotEngineServiceInstance  
  
-   New-PowerPivotEngineServiceInstance  
  
-   Remove-PowerPivotEngineServiceInstance  
  
-   Set-PowerPivotEngineService  
  
-   Set-PowerPivotEngineServiceInstance  
  
-   Update-PowerPivotEngineService  
  
  

