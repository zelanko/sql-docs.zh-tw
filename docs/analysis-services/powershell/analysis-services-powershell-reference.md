---
title: Analysis Services PowerShell 參考 |Microsoft Docs
ms.date: 06/25/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: powershell
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 13ea15a23bbf6de6c50b494f709f65cae2f7c48b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62509833"
---
# <a name="analysis-services-powershell-reference"></a>Analysis Services PowerShell 參考
[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 在包含 PowerShell cmdlet [SqlServer 模組](https://www.powershellgallery.com/packages/SqlServer/21.0.17099)。 
  
>[!NOTE] 
> Azure Analysis Services 資料庫作業會使用與 SQL Server Analysis Services 相同之 SqlServer 模組。 不過，並非所有的 cmdlet 會支援 Azure Analysis Services。 若要進一步了解，請參閱[使用 PowerShell 管理 Azure Analysis Services](https://docs.microsoft.com/azure/analysis-services/analysis-services-powershell)。
  
##  <a name="bkmk_cmdlets"></a> Analysis Services 指令程式  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 提供對應到 **Microsoft.AnalysisServices** 命名空間之方法的 Cmdlet。 下表描述每個指令程式，並提供對應 AMO 方法的連結。  
  
 如果您要使用 PowerShell 執行未在下列清單中表示的工作 (例如建立或同步處理資料庫)，可以為該動作撰寫 TMSL 或 XMLA 指令碼，然後使用 **Invoke-ASCmd** Cmdlet 執行它。  
  
|指令程式|描述|對等 AMO 方法|  
|------------|-----------------|----------------------------|  
|[Add-RoleMember 指令程式](https://docs.microsoft.com/powershell/module/sqlserver/Add-RoleMember)|將成員加入至資料庫角色。|<xref:Microsoft.AnalysisServices.RoleMemberCollection.Add%2A>|  
|[Backup-ASDatabase 指令程式](https://docs.microsoft.com/powershell/module/sqlserver/backup-asdatabase)|備份 Analysis Services 資料庫。|[Database.Backup](https://msdn.microsoft.com/library/microsoft.analysisservices.database.backup.aspx)|  
|[Invoke-ASCmd cmdlet](https://docs.microsoft.com/powershell/module/sqlserver/invoke-ascmd)|執行 XMLA 或 TSML (JSON) 格式的查詢或指令碼。|<xref:Microsoft.AnalysisServices.Core.Server.Execute%2A>|  
|[Invoke-ProcessASDatabase](https://docs.microsoft.com/powershell/module/sqlserver/invoke-processasdatabase)|處理資料庫。|<xref:Microsoft.AnalysisServices.IProcessable.Process%2A>|  
|[Invoke-ProcessCube cmdlet](https://docs.microsoft.com/powershell/module/sqlserver/invoke-processcube)|處理 Cube。|<xref:Microsoft.AnalysisServices.IProcessable.Process%2A>|  
|[Invoke-ProcessDimension cmdlet](https://docs.microsoft.com/powershell/module/sqlserver/invoke-processdimension)|處理維度。|<xref:Microsoft.AnalysisServices.IProcessable.Process%2A>|  
|[Invoke-ProcessPartition 指令程式](https://docs.microsoft.com/powershell/module/sqlserver/invoke-processpartition)|處理資料分割。|<xref:Microsoft.AnalysisServices.IProcessable.Process%2A>|  
|[Invoke-ProcessTable cmdlet](https://docs.microsoft.com/powershell/module/sqlserver/invoke-processtable)|處理表格式模型中，1200年或更高的相容性模型中的資料表。|<xref:Microsoft.AnalysisServices.IProcessable.Process%2A>|  
|[Merge-Partition cmdlet](https://docs.microsoft.com/powershell/module/sqlserver/merge-partition)|合併資料分割。|<xref:Microsoft.AnalysisServices.Partition.Merge%2A>|  
|[New-RestoreFolder cmdlet](https://docs.microsoft.com/powershell/module/sqlserver/new-restorefolder)|建立要包含資料庫備份的資料夾。|<xref:Microsoft.AnalysisServices.RestoreFolder>|  
|[New-RestoreLocation 指令程式](https://docs.microsoft.com/powershell/module/sqlserver/new-restorelocation)|指定一個或多個要還原資料庫的遠端伺服器。|<xref:Microsoft.AnalysisServices.RestoreLocation>|  
|[Remove-RoleMember 指令程式](https://docs.microsoft.com/powershell/module/sqlserver/remove-rolemember)|從資料庫角色中移除成員。|<xref:Microsoft.AnalysisServices.RoleMemberCollection.Remove%2A>|  
|[Restore-ASDatabase cmdlet](https://docs.microsoft.com/powershell/module/sqlserver/restore-asdatabase)|在伺服器執行個體上還原資料庫。|<xref:Microsoft.AnalysisServices.Core.Server.Restore%2A>|  
  

  
  
