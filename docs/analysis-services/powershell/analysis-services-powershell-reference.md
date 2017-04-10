---
title: "Analysis Services PowerShell 參考 | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "reference"
ms.assetid: 6c435e40-bfaf-4073-8cef-bc3260602246
caps.latest.revision: 9
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 9
---
# Analysis Services PowerShell 參考
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 包含 PowerShell 提供者 (SQLAS) 和 Cmdlet (SQLASCMDLETS)，讓您可以使用 Windows PowerShell 來導覽、管理和查詢 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 物件。 如需載入及使用提供者和 Cmdlet 的詳細資訊，請參閱 [Analysis Services 中的 PowerShell 指令碼](../../analysis-services/instances/powershell-scripting-in-analysis-services.md)。 如需如何以 PowerShell 使用 AMO 類型建立表格式資料庫的範例，請參閱 [AMO PowerShell Example](../../analysis-services/powershell/amo-powershell-example.md)。  
  
##  <a name="bkmk_cmdlets"></a> Analysis Services 指令程式  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 提供對應到 **Microsoft.AnalysisServices** 命名空間之方法的 Cmdlet。 下表描述每個指令程式，並提供對應 AMO 方法的連結。  
  
 如果您要使用 PowerShell 執行未在下列清單中表示的工作 (例如建立或同步處理資料庫)，可以為該動作撰寫 TMSL 或 XMLA 指令碼，然後使用 **Invoke-ASCmd** Cmdlet 執行它。  
  
|指令程式|說明|對等 AMO 方法|  
|------------|-----------------|----------------------------|  
|[Add-RoleMember 指令程式](../../analysis-services/powershell/add-rolemember-cmdlet.md)|將成員加入至資料庫角色。|<xref:Microsoft.AnalysisServices.RoleMemberCollection.Add%2A>|  
|[Backup-ASDatabase 指令程式](../../analysis-services/powershell/backup-asdatabase-cmdlet.md)|備份 Analysis Services 資料庫。|<xref:Microsoft.AnalysisServices.Database.Backup%2A>|  
|[Invoke-ASCmd 指令程式](../../analysis-services/powershell/invoke-ascmd-cmdlet.md)|執行 XMLA 或 TSML (JSON) 格式的查詢或指令碼。|<xref:Microsoft.AnalysisServices.Server.Execute%2A>|  
|[Invoke-ProcessASDatabase](../../analysis-services/powershell/invoke-processasdatabase.md)|處理資料庫。|<xref:Microsoft.AnalysisServices.IProcessable.Process%2A>|  
|[Invoke-ProcessCube 指令程式](../../analysis-services/powershell/invoke-processcube-cmdlet.md)|處理 Cube。|<xref:Microsoft.AnalysisServices.IProcessable.Process%2A>|  
|[Invoke-ProcessDimension 指令程式](../../analysis-services/powershell/invoke-processdimension-cmdlet.md)|處理維度。|<xref:Microsoft.AnalysisServices.IProcessable.Process%2A>|  
|[Invoke-ProcessPartition 指令程式](../../analysis-services/powershell/invoke-processpartition-cmdlet.md)|處理資料分割。|<xref:Microsoft.AnalysisServices.IProcessable.Process%2A>|  
|[Invoke-ProcessTable Cmdlet](../../analysis-services/powershell/invoke-processtable-cmdlet.md)|處理相容性模型 1200 或更新版本之表格式模型中的資料表。|<xref:Microsoft.AnalysisServices.IProcessable.Process%2A>|  
|[Merge-Partition 指令程式](../../analysis-services/powershell/merge-partition-cmdlet.md)|合併資料分割。|<xref:Microsoft.AnalysisServices.Partition.Merge%2A>|  
|[New-RestoreFolder 指令程式](../../analysis-services/powershell/new-restorefolder-cmdlet.md)|建立要包含資料庫備份的資料夾。|<xref:Microsoft.AnalysisServices.RestoreFolder>|  
|[New-RestoreLocation 指令程式](../../analysis-services/powershell/new-restorelocation-cmdlet.md)|指定一個或多個要還原資料庫的遠端伺服器。|<xref:Microsoft.AnalysisServices.RestoreLocation>|  
|[Remove-RoleMember 指令程式](../../analysis-services/powershell/remove-rolemember-cmdlet.md)|從資料庫角色中移除成員。|<xref:Microsoft.AnalysisServices.RoleMemberCollection.Remove%2A>|  
|[Restore-ASDatabase 指令程式](../../analysis-services/powershell/restore-asdatabase-cmdlet.md)|在伺服器執行個體上還原資料庫。|<xref:Microsoft.AnalysisServices.Server.Restore%2A>|  
  
## 請參閱＜  
 [表格式模型指令碼語言 &#40;TMSL&#41; 參考](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)   
 [Analysis Services 中表格式模型的相容性層級](../../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)   
 [Analysis Services 指令碼語言 &#40;ASSL for XMLA&#41;](../../analysis-services/scripting/analysis-services-scripting-language-assl-for-xmla.md)   
 [PowerShell scripting in Analysis Services](../../analysis-services/instances/powershell-scripting-in-analysis-services.md)  
  
  