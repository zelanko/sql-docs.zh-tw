---
title: 加入、 刪除、 變更封裝中的使用者定義變數的範圍 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- variables [Integration Services], adding
ms.assetid: cbf40c7f-3c8a-48cd-aefa-8b37faf8b40e
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: abc9f00432128750e4b61e971038bbc32dd85e86
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48125698"
---
# <a name="add-delete-change-scope-of-user-defined-variable-in-a-package"></a>加入、刪除、變更封裝中使用者定義變數的範圍
  這些程序描述如何使用 [變數] 視窗，在封裝中加入、刪除及變更使用者定義變數的範圍。  
  
 如需變數範圍的詳細資訊，請參閱[Integration Services &#40;SSIS&#41;變數](integration-services-ssis-variables.md)。  
  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 也提供系統變數，在執行階段，讓系統資訊可用，而且可以使用封裝和事件處理常式等容器中。 您無法刪除系統變數。  
  
### <a name="to-add-a-variable"></a>加入變數  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，開啟您要使用的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 封裝。  
  
2.  在 [方案總管] 中，按兩下封裝將其開啟。  
  
3.  在 [[!INCLUDE[ssIS](../includes/ssis-md.md)] 設計師] 中，若要定義變數的範圍，請執行下列其中之一：  
  
    -   若要將範圍設為封裝，按一下 [控制流程] 索引標籤之設計介面上的任意位置。  
  
    -   若要將範圍設為事件處理常式，在 [事件處理常式] 索引標籤的設計介面上，選取可執行檔和事件處理常式。  
  
    -   若要將範圍設為工作或容器，在 [控制流程] 索引標籤或 [事件處理常式] 索引標籤的設計介面上，按一下工作或容器。  
  
4.  在 [SSIS] 功能表上，按一下 [變數]。 您可以將 View.Variables 命令對應到您在 [選項] 對話方塊的 [鍵盤] 頁面中所選擇的組合鍵，以選擇性地顯示 [變數] 視窗。  
  
5.  在 [變數] 視窗中，按一下**加入變數**圖示。 新變數便會加入清單。  
  
6.  選擇性地按一下**方格選項**圖示，在 [變數方格選項] 對話方塊中選取要顯示的其他資料行，然後按一下 [確定]。  
  
7.  選擇性地設定變數屬性。 如需詳細資訊，請參閱 [設定使用者定義變數的屬性](../../2014/integration-services/set-the-properties-of-a-user-defined-variable.md)。  
  
8.  若要儲存已更新的封裝，請在 **[檔案]** 功能表上，按一下 **[儲存選取項目]** 。  
  
### <a name="to-delete-a-variable"></a>刪除變數  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，開啟包含所需封裝的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案。  
  
2.  在 [方案總管] 中，以滑鼠右鍵按一下封裝將其開啟。  
  
3.  在 **[SSIS]** 功能表上，按一下 **變數**。 您可以將 View.Variables 命令對應到您在 [選項] 對話方塊的 [鍵盤] 頁面中所選擇的組合鍵，以選擇性地顯示 [變數] 視窗。  
  
4.  選取要刪除的變數，然後按一下 [刪除變數]。  
  
     若您在 [變數] 視窗中沒看到變數，請按一下 [方格選項]，然後選取 [顯示所有範圍的變數]。  
  
5.  如果 [確認刪除變數] 對話方塊開啟，按一下 [是] 確認。  
  
6.  若要儲存已更新的封裝，請在 **[檔案]** 功能表上，按一下 **[儲存選取項目]** 。  
  
### <a name="to-change-the-scope-of-a-variable"></a>變更變數的範圍  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，開啟包含所需封裝的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案。  
  
2.  在 [方案總管] 中，以滑鼠右鍵按一下封裝將其開啟。  
  
3.  在 **[SSIS]** 功能表上，按一下 **變數**。 您可以將 View.Variables 命令對應到您在 [選項] 對話方塊的 [鍵盤] 頁面中所選擇的組合鍵，以選擇性地顯示 [變數] 視窗。  
  
4.  選取變數，然後按一下 [移動變數]。  
  
     若您在 [變數] 視窗中沒看到變數，請按一下 [方格選項]，然後選取 [顯示所有範圍的變數]。  
  
5.  在 [選取新的範圍] 對話方塊中，選取封裝或容器、工作或是封裝中的事件處理常式，以變更變數範圍。  
  
6.  若要儲存已更新的封裝，請在 **[檔案]** 功能表上，按一下 **[儲存選取項目]** 。  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services &#40;SSIS&#41;變數](integration-services-ssis-variables.md)   
 [在封裝中使用變數](../../2014/integration-services/use-variables-in-packages.md)   
 [設定使用者定義變數的屬性](../../2014/integration-services/set-the-properties-of-a-user-defined-variable.md)   
 [在子套件中使用變數和參數的值](../../2014/integration-services/use-the-values-of-variables-and-parameters-in-a-child-package.md)  
  
  
