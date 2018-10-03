---
title: 指令碼工作 | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.scripttask.f1
helpviewer_keywords:
- scripts [Integration Services], tasks
- Script task [Integration Services], about Script task
- Script task [Integration Services]
ms.assetid: f6cce7df-4bd6-4b75-9f89-6c37b4bb5558
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 38586615ce582ed4534bf23612bfca64b53af461
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48224408"
---
# <a name="script-task"></a>指令碼工作
  指令碼工作提供程式碼，用來執行無法在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 提供的內建工作和轉換中使用的函數。 指令碼工作亦可在一個指令碼中結合函數，而不使用多項工作和轉換。 您可以使用指令碼工作處理必須在封裝中執行一次 (或是每個列舉物件一次) 的工作，而非每個資料列執行一次的工作。  
  
 您可將指令碼工作用於下列用途：  
  
-   使用其他不受內建連接類型支援的技術存取資料。 例如，指令碼可使用「Active Directory 服務介面」(ADSI) 存取並擷取 Active Directory 中的使用者名稱。  
  
-   建立封裝專屬的效能計數器。 例如，指令碼可建立效能計數器，並於複雜或效能不佳的工作執行時進行更新。  
  
-   識別指定的檔案是否空白或其中包含多少資料列，然後根據這項資訊，判斷其是否會影響封裝中的控制流程。 例如，如果檔案包含零個資料列，變數值便會設為 0，而評估該值的優先順序條件約束則會讓「檔案系統」工作無法複製檔案。  
  
 如果您必須使用指令碼在集合的每一列資料上執行相同的工作，您應該使用指令碼元件，而非指令碼工作。 例如，如果要評估合理的郵資金額，並略過金額過高或過低的資料列，請使用「指令碼」元件。 如需詳細資訊，請參閱 [指令碼元件](../data-flow/transformations/script-component.md)。  
  
 如果有多個封裝使用指令碼，請考慮撰寫自訂工作，而不要使用指令碼工作。 如需詳細資訊，請參閱 [開發自訂工作](../extending-packages-custom-objects/task/developing-a-custom-task.md)。  
  
 確定指令碼工作是適用於您封裝的選擇之後，您必須同時開發該工作使用的指令碼，以及設定工作本身。  
  
## <a name="writing-and-running-the-script-that-the-task-uses"></a>撰寫並執行工作使用的指令碼  
 指令碼工作使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications (VSTA) 當做撰寫指令碼以及執行這些指令碼之引擎的環境。  
  
 VSTA 提供 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 環境的所有標準功能，例如色彩編碼的 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 編輯器、IntelliSense 和 [物件總管]。 VSTA 也使用其他 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 開發工作使用的相同偵錯工具。 指令碼中的中斷點能與 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 工作和容器上的中斷點合作無間。 VSTA 支援 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic 和 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C# 程式語言。  
  
 若要執行指令碼，必須在封裝執行的電腦上安裝 VSTA。 當封裝執行時，工作會載入指令碼引擎並執行指令碼。 您可以在專案中將參考加入至組件，藉此在指令碼中存取外部 .NET 組件。  
  
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
 下表描述可以為指令碼工作記錄的 `ScriptTaskLogEntry` 事件。 `ScriptTaskLogEntry`選取的登入事件**詳細資料**索引標籤**設定 SSIS 記錄** 對話方塊。 如需詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 記錄](../performance/integration-services-ssis-logging.md)和[自訂訊息以進行記錄](../custom-messages-for-logging.md)。  
  
|記錄項目|描述|  
|---------------|-----------------|  
|`ScriptTaskLogEntry`|報告在指令碼內實作記錄的結果。 工作寫入記錄項目，每次呼叫`Log`方法的`Dts`物件。 工作會在程式碼執行時撰寫這些項目。 如需詳細資訊，請參閱 [Logging in the Script Task](../extending-packages-scripting/task/logging-in-the-script-task.md)。|  
  
 如需有關可在「 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師」中設定之屬性的詳細資訊，請參閱下列主題：  
  
-   [指令碼工作編輯器&#40;一般頁面&#41;](../general-page-of-integration-services-designers-options.md)  
  
-   [指令碼工作編輯器&#40;指令碼 頁面&#41;](../script-task-editor-script-page.md)  
  
-   [運算式頁面](../expressions/expressions-page.md)  
  
 如需有關如何在「 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師」中設定這些屬性的詳細資訊，請參閱下列主題：  
  
-   [設定工作或容器的屬性](../set-the-properties-of-a-task-or-container.md)  
  
### <a name="configuring-the-script-task-programmatically"></a>以程式設計的方式設定指令碼工作  
 如需有關以程式設計方式設定這些屬性的詳細資訊，請參閱以下主題：  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptTask>  
  
## <a name="related-content"></a>相關內容  
  
-   shareourideas.com 上的技術文件： [How to send email with delivery notification in C#](http://go.microsoft.com/fwlink/?LinkId=237625)(如何在 C# 中傳送包含傳遞通知的電子郵件)  
  
  
