---
title: 在 Analysis Services 中編寫管理工作的腳本 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- automatic Analysis Services administration
- administering Analysis Services
ms.assetid: 106415df-81ff-4ec3-b2e1-ca66324f4cab
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 69ccdaf9bf0f8b67309a1f88c0c44a90f3167b6b
ms.sourcegitcommit: 187f6d327421e64f1802a3085f88bbdb0c79b707
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/16/2019
ms.locfileid: "69530924"
---
# <a name="script-administrative-tasks-in-analysis-services"></a>在 Analysis Services 中編寫管理工作的指令碼
  您可以撰寫或產生可手動執行或透過 SQL Server Agent 排程的指令碼，將 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 管理工作自動化。 下表摘要說明可用的指令碼選項，並提供詳細資訊的連結。  
  
 下列所有方法都支援可儲存至檔案並以獨立作業方式執行的指令碼。 因為用於表格式模型和 PowerPivot 活頁簿的 Data Analysis Expression (DAX) 語言不符合此準則，所以未將它包含在下列清單中。  
  
|方法|檔案格式|描述|連結|  
|-----------------|-----------------|-----------------|-----------|  
|PowerShell|.ps1|Analysis Services 透過從命令列加入物件導覽的新提供者，以及用於備份、還原、處理和角色管理等管理工作的新指令程式，可支援 SQL Server PowerShell 指令碼環境。<br /><br /> 此外，SQL Server PowerPivot (SQLPS) 提供者也包含一般用途指令程式 `Invoke-ASCmd`，可讓您從 PowerShell 工作階段內執行 XMLA、MDX 或 DMX 指令碼檔。<br /><br /> 多維度和表格式模型都支援 Analysis Services PowerShell 指令碼，但從 SharePoint 存取的 PowerPivot 活頁簿不支援它。|[Analysis Services PowerShell](analysis-services-powershell.md)<br /><br /> [Windows PowerShell 生存指南](https://go.microsoft.com/fwlink/?LinkId=233747)|  
|ASSL 或 XMLA 指令碼|.xmla|Analysis Services 指令碼語言 (ASSL) 是 XMLA 的延伸模組，提供對表格式或多維度模式的 Analysis Services 執行個體上之物件和作業進行資料存取。 ASSL 包含資料定義和命令語言支援，讓 Analysis Services 物件和作業能夠以 XML 格式完整表示。 使用 ASSL 所提供之物件和命令的指令碼儲存為 .xmla 檔案。 在 Analysis Services 內容中，依慣例會將 ASSL 稱為 XMLA 指令碼。 當您的需求包含下列時，選擇這種方法：<br /><br /> 您的指令碼直接在伺服器上建立物件，或執行資料定義和操作工作 (例如，重新建立和處理資料庫)。<br /><br /> 您需要跨多個工具和技術重複使用指令碼以發揮至極致。 XMLA 指令碼可加入至 SQL Server Agent 中的 Analysis Services 命令工作、在 SSIS 封裝中參考，或在 PowerShell 指令碼中參考。<br /><br /> 指令碼必須自動執行。 您可以使用 SQL Server Agent，來排程包含 XMLA 指令碼的作業或包含 XMLA 的 SSIS 封裝。<br /><br /> 您有使用 XMLA 的應用程式需求。 XMLA 是不需要 Managed 程式碼環境的介面。 您可以在不使用 .NET Framework 的應用程式中執行 XMLA 指令碼。|[在 Management Studio 中建立 Analysis Services 指令碼](instances/create-analysis-services-scripts-in-management-studio.md)<br /><br /> [在 SQL Server Management Studio 中使用 Analysis Services 範本](instances/use-analysis-services-templates-in-sql-server-management-studio.md)<br /><br /> [使用 SQL Server Agent 排程 SSAS 管理工作](instances/schedule-ssas-administrative-tasks-with-sql-server-agent.md)<br /><br /> [使用 Analysis Services 指令碼語言 &#40;ASSL&#41; 開發](multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md)<br /><br /> [Invoke-ASCmd cmdlet](/powershell/module/sqlserver/invoke-ascmd)|  
|||若要建立 XMLA 指令碼，您可以使用 Management Studio 中的指令碼產生器。 在物件層級中，以滑鼠右鍵按一下物件，即可產生建立、改變或刪除物件的指令碼。 在命令層級中，例如用於處理、備份或還原、彙總設計或另一個命令，您可以使用對話方塊中的指令碼功能，選擇將指令碼放在新視窗、檔案或剪貼簿中的選項，來產生指令碼。 您也可以在文字或程式碼編輯器中手動撰寫 XMLA 指令碼，或使用範本總管中的範本。 若要執行指令碼，請使用下列其中一個方法：<br /><br /> 使用 Management Studio，在 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 執行個體上直接建立或修改物件。<br /><br /> 使用 SQL Server Agent 來排程包含 Analysis Services 命令工作的作業。<br /><br /> 使用 Invoke-ASCmd 指令程式，在 PowerShell 工作階段中執行指令碼。||  
|MDX 指令碼|.mdx|多維度運算式 (MDX) 語言是分析資料來源的業界標準查詢語言，它也是 XMLA 規格的一部分。<br /><br /> 您可以建立查詢資料或系統資訊的獨立 MDX 指令碼檔。 例如，公開本機伺服器作業和伺服器健全狀況相關資訊的動態管理檢視 (DMV) 是透過 MDX Select 陳述式來存取。<br /><br /> MDX 指令碼會在多維度和表格式模式的伺服器上執行。 您可以從 SQL Server Management Studio 以互動方式執行指令碼，或使用 `Invoke-ASCmd` 從 PowerShell 工作階段執行指令碼。|[MDX 指令碼基礎觀念 &#40;Analysis Services&#41;](multidimensional-models/mdx/mdx-scripting-fundamentals-analysis-services.md)<br /><br /> [使用動態管理檢視 &#40;DMV&#41; 監視 Analysis Services](instances/use-dynamic-management-views-dmvs-to-monitor-analysis-services.md)<br /><br /> [在 SQL Server Management Studio 中使用 Analysis Services 範本](instances/use-analysis-services-templates-in-sql-server-management-studio.md)|  
|DMX 指令碼|.dmx|資料採礦延伸模組 (DMX) 是資料採礦模型的資料定義、資料操作和資料查詢語言。 您可以使用範本做為入門方式。|[在 SQL Server Management Studio 中建立 DMX 查詢](data-mining/create-a-dmx-query-in-sql-server-management-studio.md)<br /><br /> [在 SQL Server Management Studio 中使用 Analysis Services 範本](instances/use-analysis-services-templates-in-sql-server-management-studio.md)|  
|[!INCLUDE[ssIS](../includes/ssis-md.md)] 封裝|.dtsx|[!INCLUDE[ssIS](../includes/ssis-md.md)] 提供的工作和資料流程會建立、修改、刪除和處理 Analysis Services 物件，包括資料採礦模型。 您可以使用 SQL Server Agent 來排程封裝執行。|[Analysis Services 執行 DDL 工作](../integration-services/control-flow/analysis-services-execute-ddl-task.md)<br /><br /> [Analysis Services 處理工作](../integration-services/control-flow/analysis-services-processing-task.md)<br /><br /> [資料採礦查詢工作](../integration-services/control-flow/data-mining-query-task.md)<br /><br /> [資料採礦模型定型目的地](../integration-services/data-flow/data-mining-model-training-destination.md)<br /><br /> [維度處理目的地](../integration-services/data-flow/dimension-processing-destination.md)<br /><br /> [資料分割處理目的地](../integration-services/data-flow/partition-processing-destination.md)|  
|分析管理物件||分析管理物件 (AMO) 是 Managed 介面，程式設計人員可以用它來開發自動化管理作業的自訂應用程式。 使用 AMO，您可以開發自訂應用程式來執行您所提供的 XMLA、MDX 或 DMX 指令碼。|[使用 AMO 進行管理工作的程式設計](https://docs.microsoft.com/bi-reference/amo/programming-administrative-tasks-with-amo)|  
  
## <a name="see-also"></a>另請參閱  
 [Analysis Services 指令碼語言&#40;ASSL&#41;參考](https://docs.microsoft.com/bi-reference/assl/analysis-services-scripting-language-assl-for-xmla)   
 [使用分析管理物件 &#40;AMO&#41; 來開發](https://docs.microsoft.com/bi-reference/amo/developing-with-analysis-management-objects-amo)   
 [多維度模型物件處理](multidimensional-models/processing-a-multidimensional-model-analysis-services.md)  
  
  
