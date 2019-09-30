---
title: 指令碼元件的程式碼撰寫和偵錯 | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- SSIS Script task, development environment
- Script component [Integration Services], debugging
- Script component [Integration Services], coding
- SSIS Script component, debugging
- Script component [Integration Services], development environment
- debugging [Integration Services], scripts
- SSIS Script component, coding
- VSTA
ms.assetid: c3913c15-66aa-4b61-89b5-68488fa5f0a4
author: chugugrace
ms.author: chugu
ms.openlocfilehash: c4b3337be486123545a187337949da1c160343ad
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/26/2019
ms.locfileid: "71286549"
---
# <a name="coding-and-debugging-the-script-component"></a>指令碼元件的程式碼撰寫和偵錯

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  在 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 設計師中，指令碼元件有中繼資料設計與程式碼設計兩種模式。 當您開啟 [指令碼轉換編輯器]  時，元件就會進入中繼資料設計模式，您可在其中設定中繼資料及元件屬性。 在您於中繼資料設計模式設定好指令碼元件的屬性和輸入及輸出後，就可以切換到程式碼設計模式編寫自訂的指令碼。 如需中繼資料設計模式和程式碼設計模式的詳細資訊，請參閱[在指令碼元件編輯器中設定指令碼元件](../../../integration-services/extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md)。  
  
## <a name="writing-the-script-in-code-design-mode"></a>在程式碼設計模式中撰寫指令碼  
  
### <a name="script-component-development-environment"></a>指令碼元件開發環境  
 若要撰寫指令碼，請在 [指令碼轉換編輯器]  的 [指令碼]  頁面上按一下 [編輯指令碼]  ，開啟 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] Tools for Applications (VSTA) IDE。 VSTA IDE 包含 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] .NET 環境的所有標準功能，例如色彩編碼的 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 編輯器、IntelliSense 和物件瀏覽器。  
  
 指令碼是以 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic 或 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual C# 撰寫。 您可以在 [指令碼轉換編輯器]  中，藉由設定 **ScriptLanguage** 屬性來指定指令碼語言。 如果想要使用其他的程式語言，可以用您所選的語言開發自訂組件，然後在指令碼元件中，從程式碼呼叫其功能。  
  
 您在指令碼元件中建立的指令碼會儲存在封裝定義中， 而沒有個別的指令碼檔案。 因此，使用指令碼元件並不會影響封裝部署。  
  
> [!NOTE]  
>  在您設計封裝時，指令碼會暫時寫入專案檔。 因為將敏感性資訊儲存在檔案中會造成潛在的安全性風險，所以我們建議您不要在指令碼中包含密碼之類的敏感性資訊。  
  
 IDE 中預設會停用 **Option Strict**。  
  
### <a name="script-component-project-structure"></a>指令碼元件專案結構  
 指令碼元件的優點在於可以產生基礎結構程式碼，所以能夠減少所必須撰寫的程式碼量。 這項功能的前提是，輸入和輸出及其資料行和屬性都是固定的，而且已預先知道。 因此，對元件中繼資料所進行的任何後續變更，都可能會造成已撰寫的程式碼無效。 這會在封裝執行期間造成編譯錯誤。  
  
#### <a name="project-items-and-classes-in-the-script-component-project"></a>指令碼元件專案中的專案項目和類別  
 當您切換到程式碼設計模式時，VSTA IDE 就會開啟並顯示 **ScriptMain** 專案項目。 **ScriptMain** 專案項目包含可編輯的 **ScriptMain** 類別，這可充當指令碼的進入點，也就是撰寫程式碼的位置。 類別中的程式碼項目會根據您針對指令碼工作所選取的程式語言而變更。  
  
 指令碼專案包含兩個額外的、自動產生的唯讀專案項目：  
  
-   **ComponentWrapper** 專案項目包含三個類別：  
  
    -   **UserComponent** 類別，這個類別繼承自 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent>，且包含用於處理資料並與套件互動的方法和屬性。 **ScriptMain** 類別繼承自 **UserComponent** 類別。  
  
    -   **Connections** 集合類別，這個類別包含 [指令碼轉換編輯器] 的 [連線管理員] 頁面上所選取連線的參考。  
  
    -   **Variables** 集合類別，這個類別包含 [指令碼轉換編輯器]  的 [指令碼]  頁面上在 **ReadOnlyVariable** 和 **ReadWriteVariables** 屬性中所輸入變數的參考。  
  
-   **BufferWrapper** 專案項目所包含的類別，會針對 [指令碼轉換編輯器]  的 [輸入及輸出]  頁面上所設定的每個輸入和輸出，從 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptBuffer> 進行繼承。 這其中每個類別所包含的類型存取子屬性，都與設定的輸入和輸出資料行以及包含這些資料行的資料流緩衝區相對應。  
  
 如需如何使用這些物件、方法和屬性的資訊，請參閱[了解指令碼元件物件模型](../../../integration-services/extending-packages-scripting/data-flow-script-component/understanding-the-script-component-object-model.md)。 如需如何在特定的指令碼元件類型中使用這些類別的方法和屬性的資訊，請參閱[其他指令碼元件範例](../../../integration-services/extending-packages-scripting-data-flow-script-component-examples/additional-script-component-examples.md)。 範例主題也包含完整的程式碼範例。  
  
 當您將指令碼元件設定為轉換時，**ScriptMain** 專案項目會包含下列自動產生的程式碼。 程式碼範本也會提供指令碼元件的概觀，以及有關如何擷取與操作 SSIS 物件 (例如變數、事件與連接) 的其他資訊。  
  
```vb  
' Microsoft SQL Server Integration Services Script Component  
' Write scripts using Microsoft Visual Basic 2008.  
' ScriptMain is the entry point class of the script.  
  
Imports System  
Imports System.Data  
Imports System.Math  
Imports Microsoft.SqlServer.Dts.Pipeline.Wrapper  
Imports Microsoft.SqlServer.Dts.Runtime.Wrapper  
  
<Microsoft.SqlServer.Dts.Pipeline.SSISScriptComponentEntryPointAttribute> _  
<CLSCompliant(False)> _  
Public Class ScriptMain  
    Inherits UserComponent  
  
    Public Overrides Sub PreExecute()  
        MyBase.PreExecute()  
        '  
        ' Add your code here for preprocessing or remove if not needed  
        '  
    End Sub  
  
    Public Overrides Sub PostExecute()  
        MyBase.PostExecute()  
        '  
        ' Add your code here for postprocessing or remove if not needed  
        ' You can set read/write variables here, for example:  
        ' Me.Variables.MyIntVar = 100  
        '  
    End Sub  
  
    Public Overrides Sub Input0_ProcessInputRow(ByVal Row As Input0Buffer)  
        '  
        ' Add your code here  
        '  
    End Sub  
  
End Class  
```  
  
```csharp  
/* Microsoft SQL Server Integration Services user script component  
*  Write scripts using Microsoft Visual C# 2008.  
*  ScriptMain is the entry point class of the script.*/  
  
using System;  
using System.Data;  
using Microsoft.SqlServer.Dts.Pipeline.Wrapper;  
using Microsoft.SqlServer.Dts.Runtime.Wrapper;  
  
[Microsoft.SqlServer.Dts.Pipeline.SSISScriptComponentEntryPointAttribute]  
public class ScriptMain : UserComponent  
{  
  
    public override void PreExecute()  
    {  
        base.PreExecute();  
        /*  
          Add your code here for preprocessing or remove if not needed  
        */  
    }  
  
    public override void PostExecute()  
    {  
        base.PostExecute();  
        /*  
          Add your code here for postprocessing or remove if not needed  
          You can set read/write variables here, for example:  
          Variables.MyIntVar = 100  
        */  
    }  
  
    public override void Input0_ProcessInputRow(Input0Buffer Row)  
    {  
        /*  
          Add your code here  
        */  
    }  
  
}  
```  
  
#### <a name="additional-project-items-in-the-script-component-project"></a>指令碼元件專案中的其他專案項目  
 指令碼元件專案可以包含預設 **ScriptMain** 項目以外的項目。 您可以在專案中加入類別、模組、程式碼檔案和資料夾，也可以使用資料夾來整理項目群組。  
  
 所有您加入的項目都會保存在封裝內。  
  
#### <a name="references-in-the-script-component-project"></a>指令碼元件專案中的參考  
 您可以在 [專案總管]  中以滑鼠右鍵按一下「指令碼」工作專案，再按 [新增參考]  ，新增 Managed 組件的參考。 如需詳細資訊，請參閱[參考指令碼解決方案中的其他組件](../../../integration-services/extending-packages-scripting/referencing-other-assemblies-in-scripting-solutions.md)。  
  
> [!NOTE]  
>  您可以在 VSTA IDE 中的 [類別檢視]  或 [專案總管]  中，檢視專案參考。 您可以從 [檢視]  功能表中開啟任一個視窗。 您可以從 [專案]  功能表、[專案總管]  或 [類別檢視]  新增參考。  
  
## <a name="interacting-with-the-package-in-the-script-component"></a>與指令碼元件中的封裝互動  
 在指令碼元件中撰寫的自訂指令碼可以在自動產生的基底類別中，透過強型別 (Strongly-Typed) 的存取子從包含的封裝存取及使用變數和連接管理員。 不過，如果想要在指令碼中使用變數和連接管理員，則必須先設定變數和連接管理員，才能進入程式碼設計模式。 您也可以從指令碼元件程式碼引發事件和執行記錄。  
  
 指令碼元件專案中自動產生的專案項目會提供下列物件、方法和屬性，可用於與封裝互動。  
  
|封裝功能|存取方法|  
|---------------------|-------------------|  
|變數|使用 **ComponentWrapper** 專案項目的 **Variables** 集合類別中的具名和類型存取子屬性，這些屬性是透過 **ScriptMain** 類別的 **Variables** 屬性進行公開。<br /><br /> **PreExecute** 方法只能存取唯讀變數。 **PostExecute** 方法可以存取唯讀和讀/寫變數。|  
|連接|使用 **ComponentWrapper** 專案項目的 **Connections** 集合類別中的具名和類型存取子屬性，這些屬性是透過 **ScriptMain** 類別的 **Connections** 屬性進行公開。|  
|事件|使用 **ScriptMain** 類別的 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ComponentMetaData%2A> 屬性以及 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100> 介面的 **Fire\<X>** 方法來引發事件。|  
|記錄|使用 **ScriptMain** 類別的 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.Log%2A> 方法來執行記錄。|  
  
## <a name="debugging-the-script-component"></a>偵錯指令碼元件  
 若要偵錯指令碼元件中的程式碼，請在程式碼中設定至少一個中斷點，然後關閉 VSTA IDE，以便在 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] 中執行封裝。 當封裝執行進入指令碼元件時，VSTA IDE 會在唯讀模式下重新開啟並顯示您的程式碼。 在執行到達中斷點之後，您可以檢查變數值並逐步完成其餘的程式碼。  
  
> [!NOTE]  
>  當您在執行封裝工作的子封裝內執行指令碼元件時，將無法偵錯指令碼元件。 在這些情況下，系統會略過您在子封裝的指令碼元件中設定的中斷點。 您可以分開執行子封裝，以利正常地偵錯子封裝。  
  
> [!NOTE]  
>  當您偵錯包含多個指令碼元件的封裝時，偵錯工具會偵錯其中一個指令碼元件。 如果偵錯工具完成，系統就可以偵錯另一個指令碼元件，如同 Foreach 迴圈或 For 迴圈容器的情況。  
  
 您也可以使用下列方法來監視指令碼元件的執行：  
  
-   使用 **System.Windows.Forms** 命名空間中的 **MessageBox.Show** 方法中斷執行，並顯示強制回應訊息。 (請在完成偵錯程序之後移除此程式碼)。  
  
-   引發資訊訊息、警告和錯誤的事件。 FireInformation、FireWarning 和 FireError 方法會在 Visual Studio [輸出]  視窗中顯示事件描述。 不過，FireProgress 方法、Console.Write 方法和 Console.WriteLine 方法不會在 [輸出]  視窗中顯示任何資訊。 FireProgress 事件的訊息會顯示在 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 設計師的 [進度]  索引標籤上。 如需詳細資訊，請參閱[在指令碼元件中引發事件](../../../integration-services/extending-packages-scripting/data-flow-script-component/raising-events-in-the-script-component.md)。  
  
-   將事件或使用者定義的訊息記錄到啟用的記錄提供者。 如需詳細資訊，請參閱[在指令碼元件中記錄](../../../integration-services/extending-packages-scripting/data-flow-script-component/logging-in-the-script-component.md)。  
  
 如果只需要檢查設定為來源或轉換的指令碼元件的輸出，而不將資料儲存到目的地，可以使用[資料列計數轉換](../../../integration-services/data-flow/transformations/row-count-transformation.md)停止資料流程，並將資料檢視器附加到指令碼元件的輸出。 如需資料檢視器的資訊，請參閱[偵錯資料流程](../../../integration-services/troubleshooting/debugging-data-flow.md)。  
  
## <a name="in-this-section"></a>本節內容  
 如需有關撰寫指令碼元件程式碼的詳細資訊，請參閱此章節中的下列主題：  
  
 [了解指令碼元件物件模型](../../../integration-services/extending-packages-scripting/data-flow-script-component/understanding-the-script-component-object-model.md)  
 說明如何使用指令碼元件中可用的物件、方法和屬性。  
  
 [參考指令碼解決方案中的其他組件](../../../integration-services/extending-packages-scripting/referencing-other-assemblies-in-scripting-solutions.md)  
 說明如何參考指令碼元件中 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 類別庫的物件。  
  
 [模擬指令碼元件的錯誤輸出](../../../integration-services/extending-packages-scripting-data-flow-script-component-examples/simulating-an-error-output-for-the-script-component.md)  
 說明如何由指令碼元件針對在處理期間引發錯誤的資料列來模擬錯誤輸出。  
  
## <a name="external-resources"></a>外部資源  
  
-   blogs.msdn.com 上的部落格文章：[VSTA setup and configuration troubles for SSIS 2008 and R2 installations](https://go.microsoft.com/fwlink/?LinkId=215661) (SSIS 2008 和 R2 安裝的 VSTA 安裝與設定問題)。  
  
## <a name="see-also"></a>另請參閱  
 [在指令碼元件編輯器中設定指令碼元件](../../../integration-services/extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md)  
  
  
