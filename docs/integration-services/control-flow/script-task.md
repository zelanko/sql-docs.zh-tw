---
description: 指令碼工作
title: 指令碼工作 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.scripttask.f1
- sql13.dts.designer.scripttask.general.f1
- sql13.dts.designer.scripttask.script.f1
helpviewer_keywords:
- scripts [Integration Services], tasks
- Script task [Integration Services], about Script task
- Script task [Integration Services]
ms.assetid: f6cce7df-4bd6-4b75-9f89-6c37b4bb5558
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 506b99d81a47df7a88a2ef33ea91815b99e165fb
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88425880"
---
# <a name="script-task"></a>指令碼工作

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  指令碼工作提供程式碼，用來執行無法在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 提供的內建工作和轉換中使用的函式。 指令碼工作亦可在一個指令碼中結合函數，而不使用多項工作和轉換。 您可以使用指令碼工作處理必須在封裝中執行一次 (或是每個列舉物件一次) 的工作，而非每個資料列執行一次的工作。  
  
 您可將指令碼工作用於下列用途：  
  
-   使用其他不受內建連接類型支援的技術存取資料。 例如，指令碼可使用「Active Directory 服務介面」(ADSI) 存取並擷取 Active Directory 中的使用者名稱。  
  
-   建立封裝專屬的效能計數器。 例如，指令碼可建立效能計數器，並於複雜或效能不佳的工作執行時進行更新。  
  
-   識別指定的檔案是否空白或其中包含多少資料列，然後根據這項資訊，判斷其是否會影響封裝中的控制流程。 例如，如果檔案包含零個資料列，變數值便會設為 0，而評估該值的優先順序條件約束則會讓「檔案系統」工作無法複製檔案。  
  
 如果您必須使用指令碼在集合的每一列資料上執行相同的工作，您應該使用指令碼元件，而非指令碼工作。 例如，如果要評估合理的郵資金額，並略過金額過高或過低的資料列，請使用「指令碼」元件。 如需詳細資訊，請參閱 [指令碼元件](../../integration-services/data-flow/transformations/script-component.md)。  
  
 如果有多個封裝使用指令碼，請考慮撰寫自訂工作，而不要使用指令碼工作。 如需詳細資訊，請參閱 [開發自訂工作](../../integration-services/extending-packages-custom-objects/task/developing-a-custom-task.md)。  
  
 確定指令碼工作是適用於您封裝的選擇之後，您必須同時開發該工作使用的指令碼，以及設定工作本身。  
  
## <a name="writing-and-running-the-script-that-the-task-uses"></a>撰寫並執行工作使用的指令碼  
 指令碼工作使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications (VSTA) 作為撰寫指令碼的環境，以及執行這些指令碼的引擎。  
  
 VSTA 提供 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 環境的所有標準功能，例如色彩編碼的 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 編輯器、IntelliSense 和 [物件總管]****。 VSTA 也使用其他 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 開發工作使用的相同偵錯工具。 指令碼中的中斷點能與 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 工作和容器上的中斷點合作無間。 VSTA 支援 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic 和 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C# 程式語言。  
  
 若要執行指令碼，必須在封裝執行的電腦上安裝 VSTA。 當封裝執行時，工作會載入指令碼引擎並執行指令碼。 您可以在專案中將參考加入至組件，藉此在指令碼中存取外部 .NET 組件。 目前不支援 .NET Core 和 .NET Standard 元件參考。  
  
> [!NOTE]  
>  不像在舊版中可以指出是否已經先行編譯指令碼，所有指令碼在 [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)] 和更新的版本中都會先行編譯。 指令碼經過先行編譯後，在執行階段不會載入語言引擎，因此封裝的執行速度會更快。 不過，先行編譯的二進位檔案會使用大量的磁碟空間。  
  
## <a name="configuring-the-script-task"></a>設定指令碼工作  
 您可以利用下列方式設定指令碼工作：  
  
-   提供工作執行的自訂指令碼。  
  
-   在 VSTA 專案中，將 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 執行階段呼叫的方法指定為指令碼工作程式碼的進入點。  
  
-   指定指令碼語言。  
  
-   選擇性地提供於指令碼中使用的唯讀和讀/寫變數清單。  
  
 您可以透過「 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師」或以程式設計的方式來設定這些屬性。  
  
### <a name="configuring-the-script-task-in-the-designer"></a>在設計師中設定指令碼工作  
 下表描述可以針對指令碼工作所記錄的 **ScriptTaskLogEntry** 事件。 系統會在 [設定 SSIS 記錄]**** 對話方塊的 [詳細資料]**** 索引標籤上，選取要記錄的 **ScriptTaskLogEntry** 事件。 如需詳細資訊，請參閱 [集成服務 &#40;SSIS&#41; 記錄](../../integration-services/performance/integration-services-ssis-logging.md)。  
  
|記錄項目|描述|  
|---------------|-----------------|  
|**ScriptTaskLogEntry**|報告在指令碼內實作記錄的結果。 每次呼叫 **Dts** 物件的 **Log** 方法時，工作都會寫入記錄項目。 工作會在程式碼執行時撰寫這些項目。 如需詳細資訊，請參閱 [Logging in the Script Task](../../integration-services/extending-packages-scripting/task/logging-in-the-script-task.md)。|  
  
 如需有關可在「 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師」中設定之屬性的詳細資訊，請參閱下列主題：  
  
-   [指令碼工作編輯器 &#40;一般頁面&#41;](../../integration-services/control-flow/script-task-editor-general-page.md)  
  
-   [指令碼工作編輯器 &#40;指令碼頁面&#41;](../../integration-services/control-flow/script-task-editor-script-page.md)  
  
-   [運算式頁面](../../integration-services/expressions/expressions-page.md)  
  
 如需有關如何在「 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師」中設定這些屬性的詳細資訊，請參閱下列主題：  
  
-   [設定工作或容器的屬性](https://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
### <a name="configuring-the-script-task-programmatically"></a>以程式設計的方式設定指令碼工作  
 如需有關以程式設計方式設定這些屬性的詳細資訊，請參閱以下主題：  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptTask>  
  
## <a name="script-task-editor-general-page"></a>指令碼工作編輯器 (一般頁面)
  使用 **[指令碼工作編輯器]** 對話方塊的 **[一般]** 頁面，即可命名和描述指令碼工作。  
  
 若要深入了解指令碼工作，請參閱＜ [Script Task](../../integration-services/control-flow/script-task.md) ＞和＜ [在指令碼工作編輯器設定指令碼工作](../../integration-services/extending-packages-scripting/task/configuring-the-script-task-in-the-script-task-editor.md)＞。 若要了解如何以程式設計方式編寫指令碼工作，請參閱＜ [Extending the Package with the Script Task](../../integration-services/extending-packages-scripting/task/extending-the-package-with-the-script-task.md)＞。  
  
### <a name="options"></a>選項。  
 **名稱**  
 為指令碼工作提供唯一的名稱。 這個名稱是作為工作圖示中的標籤使用。  
  
> [!NOTE]  
>  工作名稱在封裝內必須是唯一的。  
  
 **說明**  
 輸入指令碼工作的描述。  
  
## <a name="script-task-editor-script-page"></a>指令碼工作編輯器 (指令碼頁面)
  使用 **[指令碼工作編輯器]** 對話方塊的 **[指令碼]** 頁面，即可設定指令碼屬性以及指定指令碼可存取的變數。  
  
> [!NOTE]  
>  在 [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)] 和更新的版本中，所有指令碼都是先行編譯。 在舊版中，您會設定 **[PrecompileScriptIntoBinaryCode]** 屬性來指定指令碼已先行編譯。  
  
 若要深入了解指令碼工作，請參閱＜ [Script Task](../../integration-services/control-flow/script-task.md) ＞和＜ [在指令碼工作編輯器設定指令碼工作](../../integration-services/extending-packages-scripting/task/configuring-the-script-task-in-the-script-task-editor.md)＞。 若要了解如何以程式設計方式編寫指令碼工作，請參閱＜ [Extending the Package with the Script Task](../../integration-services/extending-packages-scripting/task/extending-the-package-with-the-script-task.md)＞。  
  
### <a name="options"></a>選項。  
 **ScriptLanguage**  
 為此工作選取指令碼語言，可以是 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic 或 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C#。  
  
 當您為此工作建立指令碼之後，就無法變更 **[ScriptLanguage]** 屬性的值。  
  
 若要為指令碼工作設定預設指令碼語言，請使用 **[選項]** 對話方塊上 **[一般]** 頁面上的 **[指令碼語言]** 選項。 如需相關資訊，請參閱 [General Page](../../integration-services/control-flow/script-task-editor-general-page.md)。  
  
 **EntryPoint**  
 將 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 執行階段呼叫的方法指定為指令碼工作程式碼的進入點。 指定的方法必須位於 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications (VSTA) 專案的 ScriptMain 類別內。ScriptMain 類別是指令碼範本所產生的預設類別。  
  
 如果您在 VSTA 專案內變更此方法的名稱，您就必須變更 **[EntryPoint]** 屬性的值。  
  
 **ReadOnlyVariables**  
 鍵入以逗號分隔且指令碼可以使用的唯讀變數清單，或是按一下省略符號 (**...**) 按鈕，並在 [選取變數]**** 對話方塊中選取變數。  
  
> [!NOTE]  
>  變數名稱會區分大小寫。  
  
 **ReadWriteVariables**  
 鍵入以逗號分隔且指令碼可以使用的可讀寫變數清單，或是按一下省略符號 (**...**) 按鈕，並在 [選取變數]**** 對話方塊中選取變數。  
  
> [!NOTE]  
>  變數名稱會區分大小寫。  
  
 **編輯指令碼**  
 開啟 VSTA IDE，您可在此建立或修改指令碼。  
  
## <a name="related-content"></a>相關內容  
  
-   shareourideas.com 上的技術文件： [如何在 C# 中傳送包含傳遞通知的電子郵件](https://go.microsoft.com/fwlink/?LinkId=237625)(如何在 C# 中傳送包含傳遞通知的電子郵件)  
  
  
