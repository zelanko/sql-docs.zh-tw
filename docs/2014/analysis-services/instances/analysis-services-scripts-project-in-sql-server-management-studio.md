---
title: Analysis Services 指令碼專案，在 SQL Server Management Studio |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- scripts [Analysis Services]
- scripts [Analysis Services], projects
- projects [Analysis Services], Analysis Server Scripts project
- projects [Analysis Services], creating
- Analysis Server Scripts project
- items [Analysis Services]
ms.assetid: c4f5a06b-e2e4-4660-a3a8-6fd356742c02
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c0bcc06655333dfef073757218d9a740c1dfb0dd
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66080360"
---
# <a name="analysis-services-scripts-project-in-sql-server-management-studio"></a>SQL Server Management Studio 中的 Analysis Services 指令碼專案
  在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]中，可於 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 建立 Analysis Server 指令碼專案，將相關的指令碼組合在一起，以供開發、管理和原始檔控制使用。 如果 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中目前未載入方案，則建立新的 Analysis Server 指令碼專案會自動建立新方案。 否則，可以將新的 Analysis Server 指令碼專案加入到現有的方案，或是在新的方案中建立。  
  
 您使用下列基本步驟，即可在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中建立 Analysis Server 指令碼專案：  
  
1.  在 [檔案] 功能表上，指向 [開新檔案]，然後按一下 [專案]。  
  
     選取 **Analysis Server 指令碼**專案範本，然後指定新專案的名稱和位置。  
  
2.  以滑鼠右鍵按一下 [連接]，在方案總管中於 Analysis Server 指令碼專案的 [連接] 資料夾裡建立新連接。  
  
     此資料夾包含 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 執行個體的連接字串，Analysis Server 指令碼專案所包含的指令碼可以在這些執行個體上執行。 一個 Analysis Server 指令碼專案中可以有多個連接，而且您可以在執行專案所包含的指令碼時，選擇要使用的連接。  
  
3.  以滑鼠右鍵按一下 [查詢]，在方案總管中於 Analysis Server 指令碼專案的 [指令碼] 資料夾裡建立多維度運算式 (MDX)、資料採礦延伸模組 (DMX)，以及 XML for Analysis (XMLA) 指令碼。 如需詳細資訊，請參閱[在 Analysis Services 中編寫管理工作的指令碼](../script-administrative-tasks-in-analysis-services.md)。  
  
4.  以滑鼠右鍵按一下專案，指向 [加入]，然後選取 [現有項目]，在方案總管中於 Analysis Server 指令碼專案的 [其他] 資料夾裡加入任何其他檔案，例如包含專案附註的文字檔。 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 會忽略這些檔案。  
  
## <a name="file-types"></a>檔案類型  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 方案可包含數種檔案類型，視您包括在方案中的專案及您包括在該方案中之每個專案的項目而定。 如需 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中方案檔案類型的詳細資訊，請參閱 [管理方案和專案的檔案](../../ssms/solution/files-that-manage-solutions-and-projects.md)。 通常， [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 方案中每個專案的檔案是儲存在方案資料夾內，每一個專案都有個別的資料夾。  
  
 Analysis Server 指令碼專案的專案資料夾，可以包含下表列出的檔案類型。  
  
|檔案類型|描述|  
|---------------|-----------------|  
|Analysis Server 指令碼專案定義檔案 (.ssmsasproj)|包含在方案總管中所顯示之資料夾的中繼資料，也包含資訊指出哪些資料夾應該顯示專案中所包含的檔案。<br /><br /> 專案定義檔案也包含專案中之 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 連接的中繼資料，以及在連接和專案中所包含的指令碼檔案之間產生關聯的中繼資料。|  
|DMX 指令碼檔案 (.dmx)|包含專案中的 DMX 指令碼。|  
|MDX 指令碼檔案 (.mdx)|包含專案中的 MDX 指令碼。|  
|XMLA 指令碼檔案 (.xmla)|包含專案中的 XMLA 指令碼。|  
  
## <a name="analysis-services-templates"></a>Analysis Services 範本  
 將新的 MDX、DMX 或 XMLA 指令碼加入到 Analysis Server 指令碼專案時，您可以選擇使用範本總管來尋找 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 範本，這些範本是示範如何執行指定動作之預先定義指令碼或陳述式的集合。 您可以在 [檢視] 功能表上使用範本總管，其中包含了 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 和 [!INCLUDE[ssEW](../../includes/ssew-md.md)] 的範本。 如需詳細資訊，請參閱[在 SQL Server Management Studio 中使用 Analysis Services 範本](use-analysis-services-templates-in-sql-server-management-studio.md)。  
  
## <a name="see-also"></a>另請參閱  
 [使用 SQL Server 資料工具 &#40;SSDT&#41; 建立多維度模型](../multidimensional-models/creating-multidimensional-models-using-sql-server-data-tools-ssdt.md)   
 [多維度運算式 &#40;MDX&#41 參考](/sql/mdx/multidimensional-expressions-mdx-reference)   
 [資料採礦延伸模組 &#40;DMX&#41; 參考](/sql/dmx/data-mining-extensions-dmx-reference)   
 [Analysis Services 指令碼語言&#40;ASSL&#41;參考](https://docs.microsoft.com/bi-reference/assl/analysis-services-scripting-language-assl-for-xmla)   
 [Analysis Services 指令碼語言&#40;ASSL&#41;參考](https://docs.microsoft.com/bi-reference/assl/analysis-services-scripting-language-assl-for-xmla)  
  
  
