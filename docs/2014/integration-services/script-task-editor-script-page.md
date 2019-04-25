---
title: 指令碼工作編輯器 （指令碼頁面） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.scripttask.script.f1
helpviewer_keywords:
- Script Task Editor
ms.assetid: 93da0e0d-83f5-406d-b144-4cce216571cb
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 18be600182e3ebef6a13e19fecd7af06be2c19ec
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62766729"
---
# <a name="script-task-editor-script-page"></a>指令碼工作編輯器 (指令碼頁面)
  使用 **[指令碼工作編輯器]** 對話方塊的 **[指令碼]** 頁面，即可設定指令碼屬性以及指定指令碼可存取的變數。  
  
> [!NOTE]  
>  在 [!INCLUDE[ssISversion10](../includes/ssisversion10-md.md)] 和更新的版本中，所有指令碼都是先行編譯。 在舊版中，您會設定 **[PrecompileScriptIntoBinaryCode]** 屬性來指定指令碼已先行編譯。  
  
 若要深入了解指令碼工作，請參閱＜ [Script Task](control-flow/script-task.md) ＞和＜ [在指令碼工作編輯器設定指令碼工作](extending-packages-scripting/task/configuring-the-script-task-in-the-script-task-editor.md)＞。 若要了解如何以程式設計方式編寫指令碼工作，請參閱＜ [Extending the Package with the Script Task](extending-packages-scripting/task/extending-the-package-with-the-script-task.md)＞。  
  
## <a name="options"></a>選項。  
 **ScriptLanguage**  
 為此工作選取指令碼語言，可以是 [!INCLUDE[msCoName](../includes/msconame-md.md)] Visual Basic 或 [!INCLUDE[msCoName](../includes/msconame-md.md)] Visual C#。  
  
 當您為此工作建立指令碼之後，就無法變更 **[ScriptLanguage]** 屬性的值。  
  
 若要為指令碼工作設定預設指令碼語言，請使用 **[選項]** 對話方塊上 **[一般]** 頁面上的 **[指令碼語言]** 選項。 如需相關資訊，請參閱 [General Page](general-page-of-integration-services-designers-options.md)。  
  
 **EntryPoint**  
 將 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 執行階段呼叫的方法指定為指令碼工作程式碼的進入點。 指定的方法必須位於 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] Tools for Applications (VSTA) 專案的 ScriptMain 類別內。ScriptMain 是指令碼範本所產生的預設類別。  
  
 如果您在 VSTA 專案內變更此方法的名稱，您就必須變更 **[EntryPoint]** 屬性的值。  
  
 **ReadOnlyVariables**  
 鍵入以逗號分隔且指令碼可以使用的唯讀變數清單，或是按一下省略符號 (**...**) 按鈕，並在 [選取變數] 對話方塊中選取變數。  
  
> [!NOTE]  
>  變數名稱會區分大小寫。  
  
 **ReadWriteVariables**  
 鍵入以逗號分隔且指令碼可以使用的可讀寫變數清單，或是按一下省略符號 (**...**) 按鈕，並在 [選取變數] 對話方塊中選取變數。  
  
> [!NOTE]  
>  變數名稱會區分大小寫。  
  
 **編輯指令碼**  
 開啟 VSTA IDE，您可在此建立或修改指令碼。  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services 錯誤和訊息參考](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [General Page](general-page-of-integration-services-designers-options.md)   
 [指令碼工作編輯器 &#40;一般頁面&#41;](../../2014/integration-services/script-task-editor-general-page.md)   
 [運算式頁面](expressions/expressions-page.md)   
 [指令碼工作範例](extending-packages-scripting-task-examples/script-task-examples.md)   
 [Integration Services &#40;SSIS&#41; 變數](integration-services-ssis-variables.md)   
 [加入、刪除、變更封裝中使用者定義變數的範圍](../../2014/integration-services/add-delete-change-scope-of-user-defined-variable-in-a-package.md)  
  
  
