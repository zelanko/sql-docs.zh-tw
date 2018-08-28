---
title: 在指令碼工作編輯器設定指令碼工作 | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: ''
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
manager: craigg
ms.openlocfilehash: c1bc21e3fce77b02f6e628c1c14eac336dff4925
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/16/2018
ms.locfileid: "40405392"
---
# <a name="configuring-the-script-task-in-the-script-task-editor"></a>在指令碼工作編輯器設定指令碼工作
  在指令碼工作內撰寫自訂程式碼之前，必須先在 [指令碼工作編輯器] 的三個頁面中設定其主要屬性。 您可以使用 [屬性] 視窗，設定其他非指令碼工作專用的工作屬性。  
  
> [!NOTE]  
>  不同於在舊版中可以指出是否已編譯了指令碼，所有指令碼在 [!INCLUDE[ssISversion10](../../../includes/ssisversion10-md.md)] 中皆會先進行編譯。  
  
## <a name="general-page-of-the-script-task-editor"></a>指令碼工作編輯器的一般頁面  
 在 [指令碼工作編輯器] 的 [一般] 頁面上，為指令碼工作指派唯一的名稱與描述。  
  
## <a name="script-page-of-the-script-task-editor"></a>指令碼工作編輯器的指令碼頁面  
 [指令碼工作編輯器] 的 [指令碼] 頁面會顯示指令碼工作的自訂屬性。  
  
### <a name="scriptlanguage-property"></a>ScriptLanguage 屬性  
 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] Tools for Applications (VSTA) 支援 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic 或 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual C# 程式設計語言。 當您在指令碼工作內建立指令碼之後，就無法變更 **ScriptLanguage** 屬性的值。  
  
 若要為指令碼工作和指令碼元件設定預設指令碼語言，請使用 [選項] 對話方塊之 [一般] 頁面上的 **ScriptLanguage** 屬性。 如需相關資訊，請參閱 [General Page](../../general-page-of-integration-services-designers-options.md)。  
  
### <a name="entrypoint-property"></a>EntryPoint 屬性  
 **EntryPoint** 屬性會將 VSTA 專案中 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 執行階段所呼叫的 **ScriptMain** 類別方法指定為指令碼工作程式碼的進入點。 **ScriptMain** 類別是指令碼範本所產生的預設類別。  
  
 如果您在 VSTA 專案內變更此方法的名稱，您就必須變更 **[EntryPoint]** 屬性的值。  
  
### <a name="readonlyvariables-and-readwritevariables-properties"></a>ReadOnlyVariables 與 ReadWriteVariables 屬性  
 您可以輸入現有變數的逗號分隔清單做為這些屬性的值，使得變數可在指令碼工作程式碼中以唯讀或讀取/寫入的方式來存取。 您可以透過 **Dts** 物件的 <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Variables%2A> 屬性在程式碼中存取這兩種類型的變數。 如需詳細資訊，請參閱 [在指令碼工作中使用變數](../../../integration-services/extending-packages-scripting/task/using-variables-in-the-script-task.md)。  
  
> [!NOTE]  
>  變數名稱會區分大小寫。  
  
 若要選取變數，請按一下屬性欄位旁邊的省略符號 (**…**) 按鈕。 如需詳細資訊，請參閱[選取變數頁面](../../../integration-services/control-flow/select-variables-page.md)。  
  
### <a name="edit-script-button"></a>編輯指令碼按鈕  
 [編輯指令碼] 按鈕會啟動您用來撰寫自訂指令碼的 VSTA 開發環境。 如需詳細資訊，請參閱[指令碼工作的程式碼撰寫和偵錯](../../../integration-services/extending-packages-scripting/task/coding-and-debugging-the-script-task.md)。  
  
## <a name="expressions-page-of-the-script-task-editor"></a>指令碼工作編輯器的運算式頁面  
 在 [指令碼工作編輯器] 的 [運算式] 頁面上，您可以使用運算式，針對上面列出之指令碼工作的屬性及許多其他工作屬性來提供值。 如需詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 運算式](../../../integration-services/expressions/integration-services-ssis-expressions.md)。  
  
## <a name="see-also"></a>另請參閱  
 [編碼和偵錯指令碼工作](../../../integration-services/extending-packages-scripting/task/coding-and-debugging-the-script-task.md)  
  
  
