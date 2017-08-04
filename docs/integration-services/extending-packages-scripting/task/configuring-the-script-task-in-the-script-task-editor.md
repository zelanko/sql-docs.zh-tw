---
title: "在指令碼工作編輯器中設定指令碼工作 |Microsoft 文件"
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-xml
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
dev_langs:
- VB
helpviewer_keywords:
- Script task [Integration Services], configuring
- Script Task Editor
- SSIS Script task, configuring
ms.assetid: 232de0c9-b24d-4c38-861d-6c1f4a75bdf3
caps.latest.revision: 35
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 182a7b8f04c2339a8f3d3b986c978a7998c8a9c3
ms.contentlocale: zh-tw
ms.lasthandoff: 08/03/2017

---
# <a name="configuring-the-script-task-in-the-script-task-editor"></a>在指令碼工作編輯器設定指令碼工作
  您在指令碼工作中撰寫自訂程式碼之前，您會設定其主要屬性中的三個頁面**指令碼工作編輯器**。 您可以使用 [屬性] 視窗，設定其他非指令碼工作專用的工作屬性。  
  
> [!NOTE]  
>  不同於在舊版中可以指出是否已編譯了指令碼，所有指令碼在 [!INCLUDE[ssISversion10](../../../includes/ssisversion10-md.md)] 中皆會先進行編譯。  
  
## <a name="general-page-of-the-script-task-editor"></a>指令碼工作編輯器的一般頁面  
 在**一般**頁面**指令碼工作編輯器**，您指派唯一的名稱和描述指令碼工作。  
  
## <a name="script-page-of-the-script-task-editor"></a>指令碼工作編輯器的指令碼頁面  
 **指令碼**頁面**指令碼工作編輯器**顯示指令碼工作的自訂屬性。  
  
### <a name="scriptlanguage-property"></a>ScriptLanguage 屬性  
 [!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] Tools for Applications (VSTA) 可支援[!INCLUDE[msCoName](../../../includes/msconame-md.md)]Visual Basic 或[!INCLUDE[msCoName](../../../includes/msconame-md.md)]Visual C# 程式設計語言。 指令碼工作中建立指令碼之後，您無法變更值**ScriptLanguage**屬性。  
  
 若要設定指令碼工作和指令碼元件的預設指令碼語言，使用**ScriptLanguage**屬性**一般**頁面**選項** 對話方塊。 如需相關資訊，請參閱 [General Page](https://msdn.microsoft.com/library/ms189436(v=sql.110).aspx)。  
  
### <a name="entrypoint-property"></a>EntryPoint 屬性  
 **EntryPoint**屬性方法指定**ScriptMain**類別在 VSTA 專案[!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)]執行階段所呼叫的指令碼工作程式碼的進入點。 **ScriptMain**類別是指令碼範本所產生的預設類別。  
  
 如果您在 VSTA 專案內變更此方法的名稱，您就必須變更 **[EntryPoint]** 屬性的值。  
  
### <a name="readonlyvariables-and-readwritevariables-properties"></a>ReadOnlyVariables 與 ReadWriteVariables 屬性  
 您可以輸入現有變數的逗號分隔清單做為這些屬性的值，使得變數可在指令碼工作程式碼中以唯讀或讀取/寫入的方式來存取。 這兩種類型的變數存取程式碼透過<xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Variables%2A>屬性**Dts**物件。 如需詳細資訊，請參閱 [在指令碼工作中使用變數](../../../integration-services/extending-packages-scripting/task/using-variables-in-the-script-task.md)。  
  
> [!NOTE]  
>  變數名稱會區分大小寫。  
  
 若要選取變數，按一下省略符號 (**...**) 屬性欄位旁邊的按鈕。 如需詳細資訊，請參閱[選取變數頁面](../../../integration-services/control-flow/select-variables-page.md)。  
  
### <a name="edit-script-button"></a>編輯指令碼按鈕  
 **編輯指令碼**按鈕會啟動 VSTA 開發環境，您可以在其中撰寫自訂指令碼。 如需詳細資訊，請參閱[編碼和偵錯指令碼工作](../../../integration-services/extending-packages-scripting/task/coding-and-debugging-the-script-task.md)。  
  
## <a name="expressions-page-of-the-script-task-editor"></a>指令碼工作編輯器的運算式頁面  
 在**運算式**頁面**指令碼工作編輯器**，您可以使用運算式來提供值，如上面所列的指令碼工作的屬性以及許多其他工作屬性。 如需詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 運算式](../../../integration-services/expressions/integration-services-ssis-expressions.md)。  
  
## <a name="see-also"></a>另請參閱  
 [編碼和偵錯指令碼工作](../../../integration-services/extending-packages-scripting/task/coding-and-debugging-the-script-task.md)  
  
  
