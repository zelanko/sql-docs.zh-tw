---
title: 使用指令碼元件建立非同步轉換 | Microsoft Docs
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
- asynchronous outputs [Integration Services]
- transformation components [Integration Services]
- Script component [Integration Services], transformation components
ms.assetid: 0d814404-21e4-4a68-894c-96fa47ab25ae
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 71370adeca366b2002244c7f0aabfbca639579c7
ms.sourcegitcommit: 8d288ca178e30549d793c40510c4e1988130afb0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/16/2019
ms.locfileid: "65805199"
---
# <a name="creating-an-asynchronous-transformation-with-the-script-component"></a>使用指令碼元件建立非同步轉換

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  您在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝的資料流程中使用轉換元件，以修改及分析從來源傳遞到目的地的資料。 具有同步輸出的轉換會處理通過該元件的每個輸入資料列。 具有非同步輸出的轉換可能會等候完成其處理作業，直到轉換作業收到所有輸入資料列為止，或者轉換作業可能會在收到所有輸入資料列以前先輸出某些資料列。 本主題將討論非同步轉換。 如果您的處理需要同步轉換，請參閱[使用指令碼元件建立同步轉換](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-synchronous-transformation-with-the-script-component.md)。 如需同步與非同步元件之間差異的詳細資訊，請參閱[了解同步和非同步轉換](../../integration-services/understanding-synchronous-and-asynchronous-transformations.md)。  
  
 如需指令碼元件的概觀，請參閱[使用指令碼元件擴充資料流程](../../integration-services/extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md)。  
  
 指令碼元件以及它為您產生的基礎結構程式碼，可簡化開發自訂資料流程元件的程序。 不過，若要了解指令碼元件運作方式，請參閱[開發自訂資料流程元件](../../integration-services/extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md)一節中有關開發自訂資料流程元件所必須遵循的步驟，尤其是[開發具有同步輸出的自訂轉換元件](../../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-transformation-component-with-synchronous-outputs.md)，可能會非常有幫助。  
  
## <a name="getting-started-with-an-asynchronous-transformation-component"></a>開始使用非同步轉換元件  
 當您將指令碼元件新增至 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計工具的 [資料流程] 索引標籤時，就會開啟 [選取指令碼元件類型] 對話方塊，提示您將此元件預先設定為來源、轉換或目的地。 在這個對話方塊中，選取 [轉換]。  
  
## <a name="configuring-an-asynchronous-transformation-component-in-metadata-design-mode"></a>在中繼資料設計模式中設定非同步轉換元件  
 在您選取可建立轉換元件的選項之後，請使用 [指令碼轉換編輯器] 來設定元件。 如需詳細資訊，請參閱[在指令碼元件編輯器中設定指令碼元件](../../integration-services/extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md)。  
  
 若要選取指令碼元件將要使用的指令碼語言，請在 [指令碼轉換編輯器] 對話方塊的 [指令碼] 頁面上設定 [ScriptLanguage] 屬性。  
  
> [!NOTE]  
>  若要為指令碼元件設定預設的指令碼語言，請使用 [選項] 對話方塊中 [一般] 頁面上的 [指令碼語言] 選項。 如需相關資訊，請參閱 [General Page](../general-page-of-integration-services-designers-options.md)。  
  
 資料流程轉換元件有一個輸入，而且支援一或多個輸出。 設定元件的輸入與輸出是您必須在中繼資料設計模式下完成的其中一個步驟，方法是在撰寫自訂指令碼之前先使用 [指令碼轉換編輯器]。  
  
### <a name="configuring-input-columns"></a>設定輸入資料行  
 使用指令碼元件建立的轉換元件具有單一輸入。  
  
 在 [指令碼轉換編輯器] 的 [輸入資料行] 頁面上，資料行清單會從資料流程中的上游元件輸出顯示可用的資料行。 選取要轉換或通過的資料行。 將任何您要就地轉換的資料行標示成「讀取/寫入」。  
  
 如需 [指令碼轉換編輯器] 的 [輸入資料行] 頁面的詳細資訊，請參閱[指令碼轉換編輯器 &#40;輸入資料行頁面&#41;](../../integration-services/data-flow/transformations/script-transformation-editor-input-columns-page.md)。  
  
### <a name="configuring-inputs-outputs-and-output-columns"></a>設定輸入、輸出及輸出資料行  
 轉換元件支援一或多個輸出。  
  
 通常具有非同步輸出的轉換有兩個輸出。 例如，當您計算位於特定城市的位址數時，您可能會想要將此位址資料傳遞給某個輸出，而將彙總的結果傳送給另一個輸出。 彙總輸出也需要新的輸出資料行。  
  
 在 [指令碼轉換編輯器] 的 [輸入及輸出] 頁面上，您會看到預設已建立單一輸出，但是尚未建立輸出資料行。 在編輯器的這個頁面上，您可設定下列項目：  
  
-   您可能會想要建立一或多個其他輸出，例如彙總結果的輸出。 使用 [新增輸出] 和 [移除輸出] 按鈕管理非同步轉換元件的輸出。 將每一個輸出的 **SynchronousInputID** 屬性設定為零，指出輸出不會只是通過上游元件中的資料，或是在現有的資料列和資料行中就地轉換它。 這項設定會讓輸出與輸入不同步。  
  
-   您可能會想要將易記名稱指派給輸入和輸出。 指令碼元件使用這些名稱來產生具類型的存取子屬性，您將使用這些屬性來參考指令碼中的輸入和輸出。  
  
-   一般而言，非同步轉換會將資料行加入資料流程。 如果輸出的 **SynchronousInputID** 屬性設定為零，指示輸出不會只是通過上游元件中的資料，或是在現有的資料列和資料行中就地轉換它，則您必須明確地在輸出上新增和設定輸出資料行。 輸出資料行不需要與其對應的輸入資料行同名。  
  
-   您可能會想要加入更多的資料行來包含其他資訊。 您必須撰寫自己的程式碼，才能用資料填滿其他資料行。 如需重新產生標準錯誤輸出之行為的資訊，請參閱[模擬指令碼元件的錯誤輸出](../../integration-services/extending-packages-scripting-data-flow-script-component-examples/simulating-an-error-output-for-the-script-component.md)。  
  
 如需 [指令碼轉換編輯器] 之 [輸入及輸出] 頁面的詳細資訊，請參閱[指令碼轉換編輯器 &#40;輸入及輸出頁面&#41;](../../integration-services/data-flow/transformations/script-transformation-editor-inputs-and-outputs-page.md)。  
  
### <a name="adding-variables"></a>加入變數  
 如果有任何要在指令碼中使用其值的現有變數，則可以在 [指令碼轉換編輯器] 的 [指令碼] 頁面上，將它們新增至 ReadOnlyVariables 和 ReadWriteVariables 屬性欄位中。  
  
 當您在屬性欄位中加入多個變數時，請用逗號分隔變數名稱。 您也可以按一下 [ReadOnlyVariables] 和 [ReadWriteVariables] 屬性欄位旁邊的省略符號 ([...]) 按鈕，然後在 [選取變數] 對話方塊中選取變數，來選取多個變數。  
  
 如需如何利用指令碼元件使用變數的一般資訊，請參閱[在指令碼元件中使用變數](../../integration-services/extending-packages-scripting/data-flow-script-component/using-variables-in-the-script-component.md)。  
  
 如需 [指令碼轉換編輯器] 的 [指令碼] 頁面的詳細資訊，請參閱[指令碼轉換編輯器 &#40;指令碼頁面&#41;](../../integration-services/data-flow/transformations/script-transformation-editor-script-page.md)。  
  
## <a name="scripting-an-asynchronous-transformation-component-in-code-design-mode"></a>在程式碼設計模式中編寫非同步轉換元件的指令碼  
 在您設定好元件的所有中繼資料之後，便可撰寫自訂指令碼。 在 [指令碼轉換編輯器] 的 [指令碼] 頁面上，按一下 [編輯指令碼]，開啟 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications (VSTA) IDE 以新增自訂指令碼。 所使用的指令碼語言取決於您選取 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic 還是 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C# 作為 [指令碼] 頁面上 **ScriptLanguage** 屬性的指令碼語言。  
  
 如需使用指令碼元件所建立之各種元件都適用的重要資訊，請參閱[編碼和偵錯指令碼元件](../../integration-services/extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md)。  
  
### <a name="understanding-the-auto-generated-code"></a>了解自動產生的程式碼  
 當您在建立和設定轉換元件之後開啟 VSTA IDE 時，可編輯的 **ScriptMain** 類別會出現在程式碼編輯器中，並包括 ProcessInputRow 和 CreateNewOutputRows 方法的 Stub。 ScriptMain 類別是您將撰寫自訂程式碼的地方，而 ProcessInputRow 則是轉換元件中最重要的方法。 **CreateNewOutputRows** 方法通常比較常在來源元件中使用，這就像非同步轉換，因為兩個元件都必須建立自己的輸出資料列。  
  
 如果您開啟 VSTA [專案總管] 視窗，則可以看到指令碼元件也會產生唯讀的 **BufferWrapper** 和 **ComponentWrapper** 專案項目。 ScriptMain 類別繼承自 **ComponentWrapper** 專案項目中的 UserComponent 類別。  
  
 在執行階段，資料流程引擎會呼叫 **UserComponent** 類別中的 PrimeOutput 方法，它會覆寫 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent> 父類別的 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.PrimeOutput%2A> 方法。 PrimeOutput 方法接著會呼叫 CreateNewOutputRows 方法。  
  
 接下來，資料流程引擎會叫用 UserComponent 類別中的 ProcessInput 方法，它會覆寫 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent> 父類別的 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ProcessInput%2A> 方法。 ProcessInput 方法接著會在輸入緩衝區的資料列中執行迴圈，並為每個資料列呼叫一次 ProcessInputRow 方法。  
  
### <a name="writing-your-custom-code"></a>撰寫您的自訂程式碼  
 若要完成自訂非同步轉換元件的建立，您必須使用覆寫的 ProcessInputRow 方法來處理輸入緩衝區之每個資料列中的資料。 因為輸出與輸入不同步，所以您必須將資料列明確寫入輸出中。  
  
 在非同步轉換中，您可以使用 AddRow 方法，從 ProcessInputRow 或 ProcessInput 方法適當地將資料列新增至輸出。 您不需要使用 CreateNewOutputRows 方法。 如果您要將單一結果資料列 (如彙總結果) 寫入特定輸出，您可以事先使用 CreateNewOutputRows 方法建立輸出資料列，然後在處理所有輸入資料列之後填入它的值。 不過，在 CreateNewOutputRows 方法中建立多個資料列並不實用，因為指令碼元件只能讓您在輸入或輸出中使用目前的資料列。 在沒有輸入資料列要處理的來源元件中，CreateNewOutputRows 方法比較重要。  
  
 您可能也會想要覆寫 ProcessInput 方法本身，好讓您在輸入緩衝區內執行迴圈及針對每一個資料列呼叫 ProcessInputRow 之前或之後，可以執行其他初步或最終處理。 例如，本主題中的其中一個程式碼範例會覆寫 ProcessInput 以計算特定城市內的地址數目，因為 ProcessInputRow 會在資料列中執行迴圈。 這個範例會在處理所有資料列之後，將摘要值寫入至第二個輸出。 此範例會完成 ProcessInput 中的輸出，因為呼叫 PostExecute 時輸出緩衝區將不再可用。  
  
 視您的需求而定，您也可能會想要在 PreExecute 和 PostExecute 方法 (可在 ScriptMain 類別中取得) 中撰寫指令碼，以執行任何初步或最終處理。  
  
> [!NOTE]  
>  如果您從頭開始來開發自訂資料流程元件，則覆寫 PrimeOutput 方法來快取輸出緩衝區的參考，好讓您可以在之後將資料列新增至緩衝區是很重要的事情。 在指令碼元件中，這不是必要的，因為您已經在 **BufferWrapper** 專案項目中自動產生代表每一個輸出緩衝區的類別。  
  
## <a name="example"></a>範例  
 此範例示範在 ScriptMain 類別中所需的自訂程式碼，以建立非同步轉換元件。  
  
> [!NOTE]  
>  這些範例使用 **AdventureWorks** 範例資料庫中的 **Person.Address** 資料表，並透過資料流程傳遞其第一個和第四個資料行：**intAddressID** 和 **nvarchar(30)City** 資料行。 在本章節中的來源、轉換和目的地範例使用相同的資料。 每個範例都會記載其他必要條件與假設。  
  
 此範例示範具有兩個輸出的非同步轉換元件。 此轉換會通過 **AddressID** 和 **City** 資料行傳遞給一個輸出，而它會計算位於特定城市 (美國華盛頓州 Redmond 城市) 的地址數目，然後將產生的值輸出給第二個輸出。  
  
 如果您要執行這個範例程式碼，必須依下列方式設定封裝與元件：  
  
1.  將新指令碼元件加入資料流程設計師介面，並將它設定為轉換。  
  
2.  將來源的輸出或另一個轉換的輸出連接到設計師中的新轉換元件。 這個輸出應該從 **AdventureWorks** 範例資料庫的 **Person.Address** 資料表中提供資料，這個資料表至少包含 **AddressID** 和 **City** 資料行。  
  
3.  開啟**指令碼轉換編輯器**。 在 [輸入資料行] 頁面上，選取 [AddressID] 與 [City] 資料行。  
  
4.  在 [輸入及輸出] 頁面上，於第一個輸出新增和設定 **AddressID** 和 **City** 輸出資料行。 加入第二個輸出，然後在第二個輸出上加入摘要值的輸出資料行。 將第一個輸出的 SynchronousInputID 屬性設定為 0，因為這個範例會將每一個輸入資料列明確地複製到第一個輸出。 新建立之輸出的 SynchronousInputID 屬性已經設定為 0。  
  
5.  重新命名輸入、輸出和新的輸出資料行，為它們提供更具描述性的名稱。 此範例使用 **MyAddressInput** 作為輸入的名稱、使用 **MyAddressOutput** 和 **MySummaryOutput** 作為輸出，並使用 **MyRedmondCount** 作為第二個輸出的輸出資料行。  
  
6.  在 [指令碼] 頁面上，按一下 [編輯指令碼]，並輸入以下指令碼。 然後關閉指令碼開發環境以及 [指令碼轉換編輯器]。  
  
7.  針對第一個輸出建立及設定需要 **AddressID** 和 **City** 資料行的目的地元件，例如 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 目的地，或是在[使用指令碼元件建立目的地](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-destination-with-the-script-component.md)中所示範的範例目的地元件。 然後將轉換的第一個輸出 **MyAddressOutput** 連線至目的地元件。 您可以在 **AdventureWorks** 資料庫中執行下列 [!INCLUDE[tsql](../../includes/tsql-md.md)] 命令，以建立目的地資料表：  
  
    ```sql
    CREATE TABLE [Person].[Address2]([AddressID] [int] NOT NULL,  
        [City] [nvarchar](30) NOT NULL)  
    ```  
  
8.  為第二個輸出建立及設定另一個目的地元件。 然後將轉換的第二個輸出 **MySummaryOutput** 連線至目的地元件。 因為第二個輸出會寫入具有單一值的單一資料列，所以您可以輕鬆地使用一般檔案連接管理員來設定目的地，此管理員會連接到具有單一資料行的新檔案。 在此範例中，這個目的地資料行命名為 **MyRedmondCount**。  
  
9. 執行範例。  
  
```vb  
Public Class ScriptMain  
    Inherits UserComponent  
  
    Private myRedmondAddressCount As Integer  
  
    Public Overrides Sub CreateNewOutputRows()  
  
        MySummaryOutputBuffer.AddRow()  
  
    End Sub  
  
    Public Overrides Sub MyAddressInput_ProcessInput(ByVal Buffer As MyAddressInputBuffer)  
  
        While Buffer.NextRow()  
            MyAddressInput_ProcessInputRow(Buffer)  
        End While  
  
        If Buffer.EndOfRowset Then  
            MyAddressOutputBuffer.SetEndOfRowset()  
            MySummaryOutputBuffer.MyRedmondCount = myRedmondAddressCount  
            MySummaryOutputBuffer.SetEndOfRowset()  
        End If  
  
    End Sub  
  
    Public Overrides Sub MyAddressInput_ProcessInputRow(ByVal Row As MyAddressInputBuffer)  
  
        With MyAddressOutputBuffer  
            .AddRow()  
            .AddressID = Row.AddressID  
            .City = Row.City  
        End With  
  
        If Row.City.ToUpper = "REDMOND" Then  
            myRedmondAddressCount += 1  
        End If  
  
    End Sub  
  
End Class  
```  
  
```csharp  
public class ScriptMain:  
    UserComponent  
  
{  
    private int myRedmondAddressCount;  
  
    public override void CreateNewOutputRows()  
    {  
  
        MySummaryOutputBuffer.AddRow();  
  
    }  
  
    public override void MyAddressInput_ProcessInput(MyAddressInputBuffer Buffer)  
    {  
  
        while (Buffer.NextRow())  
        {  
            MyAddressInput_ProcessInputRow(Buffer);  
        }  
  
        if (Buffer.EndOfRowset())  
        {  
            MyAddressOutputBuffer.SetEndOfRowset();  
            MySummaryOutputBuffer.MyRedmondCount = myRedmondAddressCount;  
            MySummaryOutputBuffer.SetEndOfRowset();  
        }  
  
    }  
  
    public override void MyAddressInput_ProcessInputRow(MyAddressInputBuffer Row)  
    {  
  
        {  
            MyAddressOutputBuffer.AddRow();  
            MyAddressOutputBuffer.AddressID = Row.AddressID;  
            MyAddressOutputBuffer.City = Row.City;  
        }  
  
        if (Row.City.ToUpper() == "REDMOND")  
        {  
            myRedmondAddressCount += 1;  
        }  
  
    }  
  
}  
  
```  
  
## <a name="see-also"></a>另請參閱  
 [了解同步和非同步轉換](../../integration-services/understanding-synchronous-and-asynchronous-transformations.md)   
 [使用指令碼元件建立同步轉換](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-synchronous-transformation-with-the-script-component.md)   
 [開發具有非同步輸出的自訂轉換元件](../../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-transformation-component-with-asynchronous-outputs.md)  
  
  
