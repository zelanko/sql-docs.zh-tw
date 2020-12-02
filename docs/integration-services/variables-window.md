---
description: 變數視窗
title: 變數視窗 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.variables.f1
- sql13.dts.designer.variableoptionswindow.f1
helpviewer_keywords:
- Variables Window dialog box
ms.assetid: f405e5ce-ef69-4c58-8c7d-a3d44dfe9ab0
author: chugugrace
ms.author: chugu
ms.openlocfilehash: aa326be8b57eed58f0aa52876d0d32b889320c58
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "92193736"
---
# <a name="variables-window"></a>變數視窗

[!INCLUDE[sqlserver-ssis](../includes/applies-to-version/sqlserver-ssis.md)]


  使用 [變數] 視窗，即可建立和修改使用者定義的變數，並檢視系統變數。  
  
 依預設，[變數] 視窗位於 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 中 [SSIS 設計師] 的 [連線管理員] 區域下方。 如果您未看見 [變數] 視窗，請按一下 [SSIS] 功能表上的 [變數] 來顯示視窗。  
  
 您可以將 View.Variables 命令對應到您在 [選項] 對話方塊的 [鍵盤] 頁面中所選擇的組合鍵，以選擇性地顯示 [變數] 視窗。  
  
> [!NOTE]
>  **Name** 和 **Namespace** 屬性的值必須以 Unicode Standard 2.0 中定義的字母字元或底線 (_) 為開頭。 後續的字元可以是 Unicode Standard 2.0 中定義的字母或數字，或是底線 (\_)。  
  
## <a name="options"></a>選項。  
 **加入變數**  
 加入使用者自訂變數。  
  
 **移動變數**  
 按一下清單中的變數，然後按一下 [移動變數] 以變更變數範圍。 在 [選取新的範圍] 對話方塊中，選取封裝或容器、工作或是封裝中的事件處理常式，以變更變數範圍。  
  
 如需變數範圍的詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 變數](../integration-services/integration-services-ssis-variables.md)。  
  
 **刪除變數**  
 從清單中選取變數，然後按一下 [刪除變數]。  
  
 **方格選項**  
 按一下以開啟 [變數方格選項] 對話方塊，在其中您可以變更資料行選取範圍以及將篩選套用到 [變數] 視窗。 如需詳細資訊，請參閱 [變數方格選項]()。  
  
 **名稱**  
 檢視變數名稱。 您可以更新使用者定義變數的名稱。  
  
 **範圍**  
 檢視變數的範圍。 變數會具有整個封裝的範圍，或是容器或工作的範圍。 變數的範圍必須足夠，讓需要讀取或設定其值的任何其他工作或元件都看得到該變數。  
  
 您可以透過按一下變數，然後按一下 [變數] 視窗中的 [移動變數] 來變更範圍。  
  
 **資料類型**  
 檢視變數的資料類型。 您可以從使用者定義變數的清單中選取資料類型。  
  
> [!NOTE]  
>  若您將運算式指派給變數，則無法變更資料類型。  
  
 **ReplTest1**  
 檢視變數值。 您可以更新使用者定義變數的值。 此值可以是常值或運算式，而且此值可以是多行字串。 若要將運算式指派給變數，請按一下 [變數] 視窗中 [運算式] 資料行旁邊的省略符號按鈕。  
  
 **Namespace**  
 檢視命名空間名稱。 使用者定義變數最初是在 [使用者] 命名空間中建立的，但是您可以在 [命名空間] 欄位中變更此命名空間名稱。 若要顯示此資料行，請按一下 [方格選項]。  
  
 **引發變更事件**  
 指出某個值變更時，是否要引發 **OnVariableValueChanged** 事件。 您可以更新使用者定義及系統變數的值。 依預設，[變數] 視窗不會列出此資料行。 若要顯示此資料行，請按一下 [方格選項]。  
  
 **說明**  
 檢視變數描述。 您可以變更使用者定義變數的描述。 依預設，[變數] 視窗不會列出此資料行。 若要顯示此資料行，請按一下 [方格選項]。  
  
 **運算式**  
 檢視指派給變數的運算式。 若要指派運算式，請按一下省略符號按鈕。  
  
 若您將運算式指派給變數，變數旁邊會顯示特殊圖示標記。 此特殊圖示標記也會顯示在已經設定運算式的連接管理員及工作旁邊。  

## <a name="variable-grid-options-dialog-box"></a>[變數方格選項] 對話方塊
 使用 **[變數方格選項]** 對話方塊選擇將顯示在 **[變數]** 視窗中的資料行，並選取要套用到此變數清單的篩選。 如需所對應之變數屬性的詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 變數](../integration-services/integration-services-ssis-variables.md)。  
  
### <a name="options-for-filter"></a>篩選選項  
 **顯示系統變數**  
 選取此選項即可在 [變數] 視窗中列出系統變數。 系統變數是預先定義的， 您無法加入或刪除系統變數。 但您可以修改 **RaiseChangedEvent** 屬性設定。  
  
 此清單有色碼。 系統變數是灰色，而使用者定義的變數是黑色。  
  
 **顯示所有範圍的變數**  
 選取此選項即可顯示封裝範圍內、和封裝中的容器、工作及事件處理常式範圍內的變數。 清除此選項則只會顯示封裝範圍內以及所選取之容器、工作或事件處理常式範圍內的變數。  
  
 如需變數範圍的詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 變數](../integration-services/integration-services-ssis-variables.md)。  
  
### <a name="options-for-columns"></a>資料行選項  
 選取您想要在 **[變數]** 視窗中顯示的資料行。  
  
-   **範圍**  
  
-   **Data type**  
  
-   **ReplTest1**  
  
-   **Namespace**  
  
-   **變數值變更時引發事件**  
  
-   **說明**  
  
-   **運算式**  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services &#40;SSIS&#41; 變數](../integration-services/integration-services-ssis-variables.md)   
 [在封裝中使用變數](./integration-services-ssis-variables.md)   
 [Integration Services &#40;SSIS&#41; 運算式](../integration-services/expressions/integration-services-ssis-expressions.md)   
 [產生套件執行的傾印檔案](../integration-services/troubleshooting/generating-dump-files-for-package-execution.md)  
  
