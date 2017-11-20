---
title: "比較指令碼工作和指令碼元件 |Microsoft 文件"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: extending-packages-scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-xml
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
dev_langs:
- VB
helpviewer_keywords:
- Script task [Integration Services], comparing to Script component
- Script component [Integration Services], comparing to Script task
ms.assetid: 4b73753a-4239-491b-b7a6-abc63ba83d2d
caps.latest.revision: 39
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 0413b4b88a1f0326dad1ba261aea647cefd43302
ms.contentlocale: zh-tw
ms.lasthandoff: 08/03/2017

---
# <a name="comparing-the-script-task-and-the-script-component"></a>比較指令碼工作和指令碼元件
  指令碼工作的控制流程 視窗中，您可以使用[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]設計工具 和指令碼元件，可在 [資料流程] 視窗中，有非常不同的用途[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]封裝。 該工作是一般目的之控制流程工具，而該元件則是做為資料流程中的來源、轉換或是目的地。 不過，儘管其目的不同，指令碼工作與指令碼元件在所使用的程式碼編寫工具以及提供給開發人員的封裝中之物件方面，有一些相似之處。 了解其相似性與差異性可協助您更有效率地使用工作與元件。  
  
## <a name="similarities-between-the-script-task-and-the-script-component"></a>指令碼工作和指令碼元件之間的相似性  
 指令碼工作和指令碼元件都有下列常用的功能。  
  
|功能|Description|  
|-------------|-----------------|  
|兩種設計階段模式|在工作與元件中，您可以從在編輯器中指定屬性開始，然後再切換到開發環境以撰寫程式碼。|  
|[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications (VSTA)|工作與元件皆使用相同的 VSTA IDE，並支援 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic 或 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C# 所撰寫的程式碼。|  
|先行編譯的指令碼|從 [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)] 開始，所有指令碼皆會先行編譯。 在舊版中，您可以指定是否已經先行編譯指令碼。<br /><br /> 指令碼已先行編譯成二進位碼，允許更快速的執行，但是會增加封裝大小的成本。|  
|偵錯|工作和元件在設計環境中偵錯時，透過程式碼支援中斷點與逐步執行。 如需詳細資訊，請參閱[編碼和偵錯指令碼工作](../../integration-services/extending-packages-scripting/task/coding-and-debugging-the-script-task.md)和[編碼和偵錯指令碼元件](../../integration-services/extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md)。|  
  
## <a name="differences-between-the-script-task-and-the-script-component"></a>指令碼工作和指令碼元件之間的差異性  
 指令碼工作和指令碼元件具有下列顯著的差異。  
  
|功能|指令碼工作|指令碼元件|  
|-------------|-----------------|----------------------|  
|控制流程 / 資料流程|指令碼工作是在設計工具的 [控制流程] 索引標籤上設定，並在封裝的資料流程之外執行。|指令碼元件是在設計工具的 [資料流程] 頁面上設定，並代表資料流程工作中的來源、轉換或是目的地。|  
|目的|指令碼工作幾乎可以完成任何一般目的之工作。|您必須指定是否要以指令碼元件建立來源、轉換或是目的地。|  
|執行|指令碼工作會在封裝工作流程中的某個點執行自訂程式碼。 除非您將它放在迴圈容器或是事件處理常式中，否則它只會執行一次。|指令碼元件也只會執行一次，但是它通常會為資料流程中的每個資料列，執行一次其主要的處理常式。|  
|編輯器|**指令碼工作編輯器**有三個頁面：**一般**，**指令碼**，和**運算式**。 只有**[readonlyvariables]**和**[readwritevariables]**，和**ScriptLanguage**屬性會直接影響您可以撰寫的程式碼。|**指令碼轉換編輯器**具有最多四個頁面：**的輸入資料行**，**輸入和輸出**，**指令碼**，和**連接管理員**。 在這些頁面上設定的中繼資料與屬性，會決定自動產生的基底類別成員，以供您在撰寫程式碼時使用。|  
|與封裝之間的互動|撰寫指令碼工作的程式碼，在您使用**Dts**屬性來存取封裝的其他功能。 **Dts**屬性所屬的**ScriptMain**類別。|在指令碼元件程式碼中，您使用具有類型的存取子屬性，存取如變數與連接管理員等某些封裝功能。<br /><br /> **PreExecute**方法可以存取只有唯讀變數。 **PostExecute**方法可以存取唯讀和讀/寫變數。<br /><br /> 如需有關這些方法的詳細資訊，請參閱[編碼和偵錯指令碼元件](../../integration-services/extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md)。|  
|使用變數|指令碼工作使用<xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Variables%2A>屬性**Dts**物件可透過工作的存取變數<xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptTask.ReadOnlyVariables%2A>和<xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptTask.ReadWriteVariables%2A>屬性。 例如：<br /><br /> [Visual Basic]<br /><br /> `Dim myVar as String` <br /> `myVar = Dts.Variables(“MyStringVariable”).Value.ToString`<br /><br /> [C#]<br /><br /> `string myVar;` <br /> `myVar = Dts.Variables["MyStringVariable"].Value.ToString();`|指令碼元件使用自動產生的基底類別之具有類型的存取子屬性，從元件的 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ReadOnlyVariables%2A> 與 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ReadWriteVariables%2A> 屬性中建立。 例如：<br /><br /> [Visual Basic]<br /><br /> `Dim myVar as String` <br /> `myVar = Me.Variables.MyStringVariable`<br /><br /> [C#]<br /><br /> `string myVar;` <br /> `myVar = this.Variables.MyStringVariable;`|  
|使用連接|指令碼工作使用<xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Connections%2A>屬性**Dts**存取連接管理員封裝內定義的物件。 例如：<br /><br /> [Visual Basic]<br /><br /> `Dim myFlatFileConnection As String` <br /> `myFlatFileConnection = _     DirectCast(Dts.Connections("Test Flat File Connection").AcquireConnection(Dts.Transaction), _     String)`<br /><br /> [C#]<br /><br /> `string myFlatFileConnection;` <br /> `myFlatFileConnection = (Dts.Connections["Test Flat File Connection"].AcquireConnection(Dts.Transaction) as String);`|指令碼元件使用自動產生的基底類別之具有類型的存取子屬性，從編輯器的 [連接管理員] 頁面上之使用者所輸入的連接管理員清單中建立。 例如：<br /><br /> [Visual Basic]<br /><br /> `Dim connMgr As IDTSConnectionManager100` <br /> `connMgr = Me.Connections.MyADONETConnection`<br /><br /> [C#]<br /><br /> `IDTSConnectionManager100 connMgr;` <br /> `connMgr = this.Connections.MyADONETConnection;`|  
|引發事件|指令碼工作使用<xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Events%2A>屬性**Dts**引發事件的物件。 例如：<br /><br /> [Visual Basic]<br /><br /> `Dts.Events.FireError(0, "Event Snippet", _     ex.Message & ControlChars.CrLf & ex.StackTrace, _     "", 0)`<br /><br /> [C#]<br /><br /> `Dts.Events.FireError(0, "Event Snippet", ex.Message + "\r" + ex.StackTrace, "", 0);`|指令碼元件會透過使用 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100> 屬性傳回的 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ComponentMetaData%2A> 介面，引發錯誤、警告和參考用訊息。 例如：<br /><br /> [Visual Basic]<br /><br /> `Dim myMetadata as IDTSComponentMetaData100 myMetaData = Me.ComponentMetaData myMetaData.FireError(...)`|  
|記錄|指令碼工作使用<xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Log%2A>方法**Dts**物件來記錄資訊來啟用記錄提供者。 例如：<br /><br /> [Visual Basic]<br /><br /> `Dim bt(0) As Byte Dts.Log("Test Log Event", _     0, _     bt)`<br /><br /> [C#]<br /><br /> `byte[] bt = new byte[0];` <br /> `Dts.Log("Test Log Event", 0, bt);`|指令碼元件會使用自動產生之基底類別的 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.Log%2A> 方法，將資訊記錄到啟用的記錄提供者。 例如：<br /><br /> [Visual Basic]<br /><br /> `Dim bt(0) As Byte`<br /><br /> `Me.Log("Test Log Event", _`<br /><br /> `0, _`<br /><br /> `bt)`<br /><br /> [C#]<br /><br /> `byte[] bt = new byte[0]; this.Log("Test Log Event", 0, bt);`|  
|傳回結果|指令碼工作會同時使用<xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.TaskResult%2A>屬性和選擇性<xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.ExecutionValue%2A>屬性**Dts**物件通知執行階段其結果。|指令碼元件以資料流程工作的一部分執行，而且不會使用這些屬性的任何一個來報告結果。|  
  
## <a name="see-also"></a>另請參閱  
 [Extending the Package with the Script Task](../../integration-services/extending-packages-scripting/task/extending-the-package-with-the-script-task.md)   
 [擴充 with the Script Component 資料流程](../../integration-services/extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md)   
  
  

