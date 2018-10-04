---
title: 將元件分組或取消分組 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- grouping containers
- tasks [Integration Services], grouping
- containers [Integration Services], grouping
- grouping tasks
ms.assetid: 34320838-c271-4f8c-90b3-1254690890bb
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 75850ed20566d013fac8e2a855b76f2a375d3734
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48095218"
---
# <a name="group-or-ungroup-components"></a>將元件分組或取消分組
  **設計師中的**[控制流程] **、**[資料流程] **和** [事件處理常式] [!INCLUDE[ssIS](../includes/ssis-md.md)] 索引標籤都支援可摺疊的群組。 如果封裝具有許多元件，這些索引標籤可能會變得十分擁擠，因而難以同時檢視所有元件並找到您要使用的項目。 可摺疊的群組功能可以節省工作介面的空間，讓您更輕易地使用大型封裝。  
  
 您可以先選取要分組的元件、將它們分組，然後視工作需要展開或摺疊群組。 展開群組可讓您存取群組中元件的屬性。 與工作和容器連接的優先順序條件約束會自動包含在群組中。  
  
 下面是將元件分組的考量。  
  
-   若要將元件分組，控制流程、資料流程和事件處理常式必須包含多個元件。  
  
-   群組也可以呈巢狀，這樣就能在群組中建立群組。 雖然設計介面可以實作多個非巢狀群組，不過除非群組是巢狀的，否則一個元件只能屬於一個群組。  
  
-   儲存封裝時， [!INCLUDE[ssIS](../includes/ssis-md.md)] 設計師會儲存群組，但是群組並不會影響封裝執行。 將元件分組的能力是設計階段功能，不會影響封裝的執行階段行為。  
  
### <a name="to-group-components"></a>若要將元件分組  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，開啟包含所需封裝的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案。  
  
2.  在 [方案總管] 中，按兩下封裝將其開啟。  
  
3.  按一下 **[控制流程]**、 **[資料流程]** 或 **[事件處理常式]** 索引標籤。  
  
4.  在索引標籤的設計介面上，選取您要分組的元件、以滑鼠右鍵按一下選取的元件，然後按一下 [群組]。  
  
5.  若要儲存已更新的封裝，請在 **[檔案]** 功能表上，按一下 **[儲存選取項目]** 。  
  
### <a name="to-ungroup-components"></a>若要取消元件的分組  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，開啟包含所需封裝的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案。  
  
2.  在 [方案總管] 中，按兩下封裝將其開啟。  
  
3.  按一下 **[控制流程]**、 **[資料流程]** 或 **[事件處理常式]** 索引標籤。  
  
4.  在索引標籤的設計介面上，選取包含您要取消分組之元件的群組、按一下滑鼠右鍵，然後按一下 [取消群組]。  
  
5.  若要儲存已更新的封裝，請在 **[檔案]** 功能表上，按一下 **[儲存選取項目]** 。  
  
## <a name="see-also"></a>另請參閱  
 [在控制流程中新增或刪除工作或容器](control-flow/add-or-delete-a-task-or-a-container-in-a-control-flow.md)  
     
 [使用預設的優先順序條件約束來連接工作和容器](../../2014/integration-services/connect-tasks-and-containers-by-using-a-default-precedence-constraint.md)  
  
  
