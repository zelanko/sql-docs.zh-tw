---
title: 處理的工具和方法（Analysis Services） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- process [Analysis Services]
- processing [Analysis Services]
ms.assetid: 82347a16-4145-4655-8adf-2a300f1fdf99
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a6bcc8e830c682c800f7dbdd586b25b88ca8577f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "69530936"
---
# <a name="tools-and-approaches-for-processing-analysis-services"></a>處理的工具和方式 (Analysis Services)
  處理是 Analysis Services 查詢關聯式資料來源，然後使用該資料來擴展 Analysis Services 物件的作業。  
  
 身為 Analysis Services 系統管理員的您，可以使用這些方法執行及監視 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 物件的處理：  
  
-   執行影響分析，以了解物件相依性和作業範圍  
  
-   在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]  
  
-   在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]  
  
-   執行影響分析，以檢閱將會因為目前動作而取消處理之相關物件的清單。  
  
-   在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 的 [ [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] XMLA 查詢] 視窗中，產生及執行指令碼，以處理個別或多個物件  
  
-   使用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] PowerShell 指令程式  
  
-   使用 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 封裝中的控制流程和工作  
  
-   使用 SQL Server Profiler 來監視處理  
  
-   使用 AMO 進行自訂方案程式設計。 如需相關資訊，請參閱 [Programming AMO OLAP Basic Objects](https://docs.microsoft.com/bi-reference/amo/programming-amo-olap-basic-objects)。  
  
 處理是可高度設定的作業，由決定在物件層級上發生完整處理或累加式處理的一組處理選項所控制。 如需處理選項和物件的詳細資訊，請參閱[處理選項和設定 &#40;Analysis Services&#41;](processing-options-and-settings-analysis-services.md) 和[處理 Analysis Services 物件](processing-analysis-services-objects.md)。  
  
> [!NOTE]  
>  此主題描述用於處理多維度模型的工具和方法。 如需有關處理表格式模型的詳細資訊，請參閱[處理資料庫、資料表或資料分割](../tabular-models/process-database-table-or-partition-analysis-services.md)和[處理資料 &#40;SSAS 表格式&#41;](../process-data-ssas-tabular.md)。  
  
### <a name="processing-objects-in-sql-server-management-studio"></a>在 SQL Server Management Studio 中處理物件  
  
1.  啟動 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 並連接到 Analysis Services。  
  
2.  以滑鼠右鍵按一下您要處理的 Analysis Services 物件，然後按一下 [處理]****。 您可以在這些任何層級處理資料：  
  
    -   資料庫  
  
    -   Cube  
  
    -   量值群組或量值群組中的個別分割區  
  
    -   維度  
  
    -   採礦模型  
  
    -   採礦結構  
  
     Analysis Services 物件是階層式。 如果您選擇資料庫，資料庫中包含的所有物件都可以進行處理。 實際上是否進行處理會依您選取的處理選項和物件的狀態而有所不同。 明確地說，如果物件未經過處理，處理其父系將會導致該物件進行處理。 如需有關物件相依性的詳細資訊，請參閱＜ [Processing Analysis Services Objects](processing-analysis-services-objects.md)＞。  
  
3.  在 **[處理]** 對話方塊的 **[處理選項]** 中，使用提供的預設值或從清單選取不同的選項。 如需每個選項的詳細資訊，請參閱[處理選項和設定 &#40;Analysis Services&#41;](processing-options-and-settings-analysis-services.md)。  
  
4.  如果 [處理] 對話方塊中所列出的物件已經處理，請按一下 **[影響分析]** 來識別及選擇性地處理受影響的相依物件。  
  
5.  或者，按一下 **[變更設定]** 來修改處理順序、相對於特定類型錯誤的處理行為，以及其他設定。  
  
6.  按一下 [確定]  。  
  
     [處理進度] 對話方塊會提供每個命令的進行中狀態。 如果狀態訊息遭到截斷，您可以按一下 **[檢視詳細資料]** 來讀取完整訊息。  
  
### <a name="processing-objects-in-sql-server-data-tools"></a>在 SQL Server 資料工具中處理物件  
  
1.  啟動 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 並開啟已部署的專案。  
  
2.  在 [方案總管] 中，已部署的專案之下，展開 **[維度]** 資料夾。  
  
3.  以滑鼠右鍵按一下維度，然後按一下 [處理]****。 您可以用滑鼠右鍵按一下多個維度，一次處理多個物件。 如需詳細資訊，請參閱 [批次處理 &#40;Analysis Services&#41;](batch-processing-analysis-services.md)。  
  
4.  在 **[處理維度]** 對話方塊中，於 **[物件清單]** 下的 **[處理選項]** 資料行中，確認這個資料行的選項是 **[完整處理]**。 如果不是，請在 [處理選項]**** 之下，按一下選項，然後從下拉式清單中選取 [完整處理]****。  
  
5.  按一下 **[執行]** 。  
  
6.  當處理完成時，請按一下 **[關閉]**。  
  
##  <a name="bkmk_impactanalysis"></a>執行影響分析以識別物件相依性和作業範圍  
  
1.  在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 或 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 中處理 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]物件之前，您可以按一下其中一個 **[處理物件]** 對話方塊中的 **[影響分析]** ，來分析對相關物件的影響。  
  
2.  以滑鼠右鍵按一下維度、Cube、量值群組或分割區，開啟 [處理物件]**** 對話方塊。  
  
3.  按一下 **[影響分析]**。 
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 就會掃描模型，並報告與已選取進行處理物件相關之物件的重新處理需求。  
  
### <a name="processing-objects-using-xmla"></a>使用 XMLA 處理物件  
  
1.  啟動 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 並連接到 Analysis Services。  
  
2.  以滑鼠右鍵按一下要處理的物件，然後按一下 [處理]****。  
  
3.  在 **[處理]** 對話方塊中，選取要使用的處理選項。 修改其他任何設定。 執行 [影響分析] 來識別您可能需要進行的所有變更。  
  
4.  按一下 **[處理物件]** 畫面上的 **[指令碼]** 。  
  
     如此即可產生 XMLA 指令碼，並開啟 [ [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] XMLA 查詢] 視窗。  
  
5.  關閉對話方塊。 該指令碼包含在對話方塊中指定的處理命令和選項。  
  
6.  (選擇性) 如果您要在同一個批次中處理其他物件，可以繼續加入至指令碼。 若要繼續，請重複先前步驟附加產生的指令碼，以便在單一指令碼中包含所有處理作業。 若要檢視範例，請參閱＜ [Schedule SSAS Administrative Tasks with SQL Server Agent](../instances/schedule-ssas-administrative-tasks-with-sql-server-agent.md)＞。  
  
7.  從功能表列中按一下 **[查詢]**，然後按一下 **[執行]**。  
  
### <a name="processing-objects-using-powershell"></a>使用 PowerShell 處理物件  
  
1.  從這個版本的 SQL Server 開始，您可以使用 Analysis Services PowerShell 指令程式處理物件。 下列指令程式可以以互動方式或指令碼執行：  
  
    -   [Invoke-processcube 程式 Cmdlet](/powershell/module/sqlserver/invoke-processcube)  
  
    -   [Invoke-processdimension Cmdlet](/powershell/module/sqlserver/invoke-processdimension)  
  
    -   [ProcessPartition Cmdlet](/powershell/module/sqlserver/invoke-processpartition)  
  
    -   [ASCmd 指令程式](/powershell/module/sqlserver/invoke-ascmd)，可用於執行包含處理命令的 XMLA、MDX 或 DMX 腳本。  
  
### <a name="monitoring-object-processing-using-sql-server-profiler"></a>使用 SQL Server Profiler 監視物件處理  
  
1.  在 SQL Server Profiler 中連接到 Analysis Services 執行個體。  
  
2.  在 [事件選取範圍] 中，按一下 **[顯示所有事件]** 將所有事件加入至清單。  
  
3.  選擇下列事件：  
  
    -   啟動和停止處理時所要顯示的**命令開始**和**命令結束**  
  
    -   用來捕捉任何錯誤的**錯誤**  
  
    -   [**進度報表開始**]、[**目前的進度報表**] 和 [**進度報表結束**] 以報告處理狀態，並顯示用來抓取資料的 SQL 查詢  
  
    -   **執行 Mdx 腳本開始**和**執行 mdx 腳本結束**以顯示 cube 計算  
  
    -   (選擇性) 如果您要診斷處理相關的效能問題，可加入鎖定事件  
  
### <a name="process-analysis-services-objects-using-integration-services"></a>使用 Integration Services 來處理 Analysis Services 物件  
  
1.  在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]中建立封裝，當您定期更新來源關聯式資料庫時，它會使用 Analysis Services 處理工作自動以新資訊擴展物件。  
  
2.  在 SSIS 工具箱****，按兩下 [Analysis Services 處理]**** 將其加入到封裝。  
  
3.  編輯工作，以指定資料庫連接、要處理的物件和處理選項。 如需有關如何實作這項工作的詳細資訊，請參閱＜ [Analysis Services Processing Task](../../integration-services/control-flow/analysis-services-processing-task.md)＞。  
  
## <a name="see-also"></a>另請參閱  
 [多維度模型物件處理](processing-a-multidimensional-model-analysis-services.md)  
  
  
