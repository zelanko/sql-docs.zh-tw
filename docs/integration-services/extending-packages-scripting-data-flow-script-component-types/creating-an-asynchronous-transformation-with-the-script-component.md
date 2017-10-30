---
title: "使用指令碼元件建立非同步轉換 |Microsoft 文件"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
dev_langs:
- VB
helpviewer_keywords:
- asynchronous outputs [Integration Services]
- transformation components [Integration Services]
- Script component [Integration Services], transformation components
ms.assetid: 0d814404-21e4-4a68-894c-96fa47ab25ae
caps.latest.revision: 63
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 4da61e00337430a3eaef84e40f9f732a572cc45b
ms.contentlocale: zh-tw
ms.lasthandoff: 09/26/2017

---
# <a name="creating-an-asynchronous-transformation-with-the-script-component"></a>使用指令碼元件建立非同步轉換
  您在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝的資料流程中使用轉換元件，以修改及分析從來源傳遞到目的地的資料。 具有同步輸出的轉換會處理通過該元件的每個輸入資料列。 具有非同步輸出的轉換可能會等候完成其處理程序，直到轉換作業收到所有輸入資料列，或轉換可能會收到所有輸入資料列之前輸出某些資料列。 本主題將討論非同步轉換。 如果您的處理需要同步轉換，請參閱[使用指令碼元件建立同步轉換](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-synchronous-transformation-with-the-script-component.md)。 如需有關同步和非同步元件之間差異的詳細資訊，請參閱[了解同步和非同步轉換](../../integration-services/understanding-synchronous-and-asynchronous-transformations.md)。  
  
 如需指令碼元件的概觀，請參閱[Extending the Data Flow with Script Component](../../integration-services/extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md)。  
  
 指令碼元件以及它為您產生的基礎結構程式碼，可簡化開發自訂資料流程元件的程序。 不過，若要了解指令碼元件如何運作，您可能會發現閱讀開發自訂資料流程元件中的，您必須遵循的步驟[開發自訂資料流程元件](../../integration-services/extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md) 區段中，並特別是[開發具有同步輸出的自訂轉換元件](../../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-transformation-component-with-synchronous-outputs.md)。  
  
## <a name="getting-started-with-an-asynchronous-transformation-component"></a>開始使用非同步轉換元件  
 當您將指令碼元件加入至 [資料流程] 索引標籤的[!INCLUDE[ssIS](../../includes/ssis-md.md)]設計工具中，**選取指令碼元件類型** 對話方塊隨即出現，提示您將預先設定為來源、 轉換或目的地的元件。 在此對話方塊中，選取**轉換**。  
  
## <a name="configuring-an-asynchronous-transformation-component-in-metadata-design-mode"></a>在中繼資料設計模式中設定非同步轉換元件  
 您選取選項以建立轉換元件之後，您會設定元件利用**指令碼轉換編輯器**。 如需詳細資訊，請參閱[設定指令碼元件指令碼元件編輯器中](../../integration-services/extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md)。  
  
 若要選取指令碼元件會使用的指令碼語言，您將設定**ScriptLanguage**屬性**指令碼**頁面**指令碼轉換編輯器**對話方塊方塊。  
  
> [!NOTE]  
>  若要設定預設的指令碼語言指令碼元件，請使用**指令碼語言**選項**一般**頁面**選項** 對話方塊。 如需相關資訊，請參閱 [General Page](https://msdn.microsoft.com/library/ms189436(v=sql.110).aspx)。  
  
 資料流程轉換元件有一個輸入，而且支援一或多個輸出。 設定輸入與元件的輸出是其中一個步驟，您必須使用中繼資料設計模式中，在完成**指令碼轉換編輯器**，然後才能在您撰寫自訂指令碼。  
  
### <a name="configuring-input-columns"></a>設定輸入資料行  
 使用指令碼元件建立的轉換元件具有單一輸入。  
  
 在**的輸入資料行**頁面**指令碼轉換編輯器**，清單 欄會顯示可用的資料行，從上游元件的輸出資料流中。 選取要轉換或通過的資料行。 將任何您要就地轉換的資料行標示成「讀取/寫入」。  
  
 如需有關**的輸入資料行**頁面**指令碼轉換編輯器**，請參閱[指令碼轉換編輯器 &#40; 輸入資料行頁面 &#41;](../../integration-services/data-flow/transformations/script-transformation-editor-input-columns-page.md)。  
  
### <a name="configuring-inputs-outputs-and-output-columns"></a>設定輸入、輸出及輸出資料行  
 轉換元件支援一或多個輸出。  
  
 通常具有非同步輸出的轉換有兩個輸出。 例如，當您計算位於特定城市的位址數時，您可能會想要將此位址資料傳遞給某個輸出，而將彙總的結果傳送給另一個輸出。 彙總輸出也需要新的輸出資料行。  
  
 在**輸入和輸出**頁面**指令碼轉換編輯器**，您會看到根據預設，已建立單一輸出，但尚未建立任何輸出資料行。 在編輯器的這個頁面上，您可設定下列項目：  
  
-   您可能會想要建立一或多個其他輸出，例如彙總結果的輸出。 使用**加入輸出**和**移除輸出**按鈕管理非同步轉換元件的輸出。 設定**SynchronousInputID**屬性為零來指示輸出不只是通過上游元件的資料，或現有的資料列和資料行中就地轉換它的每個輸出。 這項設定會讓輸出與輸入不同步。  
  
-   您可能會想要將易記名稱指派給輸入和輸出。 指令碼元件使用這些名稱來產生具類型的存取子屬性，您將使用這些屬性來參考指令碼中的輸入和輸出。  
  
-   一般而言，非同步轉換會將資料行加入資料流程。 當**SynchronousInputID**輸出的屬性為零，表示輸出不只是通過上游元件資料或您必須新增並設定現有的資料列和資料行中就地轉換它在輸出上明確的輸出資料行。 輸出資料行不需要與其對應的輸入資料行同名。  
  
-   您可能會想要加入更多的資料行來包含其他資訊。 您必須撰寫自己的程式碼，才能用資料填滿其他資料行。 重現行為的標準錯誤輸出的相關資訊，請參閱[模擬錯誤輸出指令碼元件](../../integration-services/extending-packages-scripting-data-flow-script-component-examples/simulating-an-error-output-for-the-script-component.md)。  
  
 如需有關**輸入和輸出**頁面**指令碼轉換編輯器**，請參閱[指令碼轉換編輯器 &#40; 輸入及輸出頁面 &#41;](../../integration-services/data-flow/transformations/script-transformation-editor-inputs-and-outputs-page.md)。  
  
### <a name="adding-variables"></a>加入變數  
 如果有任何現有變數的值，您想要使用指令碼中，您可以新增它們在 ReadOnlyVariables 與 ReadWriteVariables 屬性欄位中上**指令碼**頁面**指令碼轉換編輯器**.  
  
 當您在屬性欄位中加入多個變數時，請用逗號分隔變數名稱。 您也可以選取多個變數，依序按一下省略符號 (**...**) 旁邊**readonlyvariables**和**readwritevariables**屬性欄位，然後選取 在變數**選取變數**對話方塊。  
  
 如需如何使用指令碼元件中使用變數的一般資訊，請參閱[在指令碼元件中使用變數](../../integration-services/extending-packages-scripting/data-flow-script-component/using-variables-in-the-script-component.md)。  
  
 如需有關**指令碼**頁面**指令碼轉換編輯器**，請參閱[指令碼轉換編輯器 &#40;指令碼頁面 &#41;](../../integration-services/data-flow/transformations/script-transformation-editor-script-page.md).  
  
## <a name="scripting-an-asynchronous-transformation-component-in-code-design-mode"></a>在程式碼設計模式中編寫非同步轉換元件的指令碼  
 在您設定好元件的所有中繼資料之後，便可撰寫自訂指令碼。 在**指令碼轉換編輯器**上**指令碼**頁面上，按一下**編輯指令碼**開啟[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications (VSTA) IDE您可以在其中加入自訂指令碼。 您使用的指令碼語言，取決於您選取[!INCLUDE[msCoName](../../includes/msconame-md.md)]Visual Basic 或[!INCLUDE[msCoName](../../includes/msconame-md.md)]Visual C# 做為指令碼語言**ScriptLanguage**屬性**指令碼**頁面。  
  
 適用於所有類型的元件所使用的指令碼元件建立的重要資訊，請參閱[編碼和偵錯指令碼元件](../../integration-services/extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md)。  
  
### <a name="understanding-the-auto-generated-code"></a>了解自動產生的程式碼  
 當您在建立和設定轉換元件，可編輯之後開啟 VSTA IDE 時**ScriptMain** ProcessInputRow 和 CreateNewOutputRows 方法類別會出現在程式碼編輯器，為虛設常式。 ScriptMain 類別是您將撰寫自訂程式碼，而且 ProcessInputRow 轉換元件中最重要的方法。 **CreateNewOutputRows**方法通常用於來源元件，也就是像非同步轉換，因為這兩個元件必須建立自己的輸出資料列。  
  
 如果您在 VSTA 中開啟**Project Explorer**視窗中，您可以看到，指令碼元件也會產生唯讀**BufferWrapper**和**ComponentWrapper**專案項目. ScriptMain 類別繼承自 UserComponent 類別中**ComponentWrapper**專案項目。  
  
 在執行階段，資料流程引擎呼叫 PrimeOutput 方法中**UserComponent**類別，它會覆寫<xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.PrimeOutput%2A>方法<xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent>父類別。 PrimeOutput 方法接著呼叫 CreateNewOutputRows 方法。  
  
 接下來，資料流程引擎會叫用的 ProcessInput 方法於在 UserComponent 類別中，會覆寫<xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ProcessInput%2A>方法<xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent>父類別。 ProcessInput 方法接著會透過輸入緩衝區中的資料列執行迴圈，並呼叫 ProcessInputRow 方法一次，每個資料列。  
  
### <a name="writing-your-custom-code"></a>撰寫您的自訂程式碼  
 若要完成建立自訂非同步轉換元件，您必須使用覆寫的 ProcessInputRow 方法來處理輸入緩衝區的每個資料列中的資料。 因為輸出與輸入不同步，所以您必須將資料列明確寫入輸出中。  
  
 在非同步轉換中，您可以使用 AddRow 方法將資料列加入 ProcessInputRow 或 ProcessInput 方法從適當的輸出。 您沒有使用 CreateNewOutputRows 方法。 如果您要的結果，例如彙總結果的單一資料列寫入特定輸出，您可以事先建立使用 CreateNewOutputRows 方法的輸出資料列，並處理所有輸入資料列之後，再填入其值。 不過它不是用於在 CreateNewOutputRows 方法中，建立多個資料列因為指令碼元件只能讓您使用目前的資料列中輸入或輸出。 CreateNewOutputRows 方法是更重要的來源元件中有未處理的輸入資料列。  
  
 您可能也需要覆寫的 ProcessInput 方法本身，以便您可以執行其他初步或最終處理之前或之後您輸入緩衝區執行迴圈，並呼叫 ProcessInputRow 每個資料列。 例如，本主題中的程式碼範例的其中一個覆寫來計算特定城市中的位址數目做為資料列的 ProcessInputRow 迴圈 ProcessInput**。** 範例寫入的摘要值的第二個輸出處理所有資料列之後。 此範例會完成在 ProcessInput 輸出，因為輸出緩衝區 PostExecute 呼叫時便無法再使用。  
  
 根據您的需求，您也可以執行任何初步或最終處理 ScriptMain 類別中可用的 PreExecute 和 PostExecute 方法中撰寫指令碼。  
  
> [!NOTE]  
>  如果您要開發自訂資料流程元件從頭，務必覆寫以快取參考加入輸出緩衝區的 PrimeOutput 方法，好讓您無法加入到緩衝區的資料列更新版本。 在指令碼元件中，這不需要因為自動產生的類別代表在每一個輸出緩衝區**BufferWrapper**專案項目。  
  
## <a name="example"></a>範例  
 此範例示範建立非同步轉換元件需要 ScriptMain 類別中的自訂程式碼。  
  
> [!NOTE]  
>  這些範例使用**Person.Address**資料表中**AdventureWorks**範例資料庫，並傳遞其第一個和第四個資料行， **intAddressID**和**nvarchar (30) 縣 （市)** ，經過資料流資料行。 在本章節中的來源、轉換和目的地範例使用相同的資料。 每個範例都會記載其他必要條件與假設。  
  
 此範例示範具有兩個輸出的非同步轉換元件。 此轉換會通過**AddressID**和**縣 （市)**至一個輸出，而它會計算的位址位於特定城市 （Redmond，Washington，美國），然後按一下 輸出資料行第二個輸出產生的值。  
  
 如果您要執行這個範例程式碼，必須依下列方式設定封裝與元件：  
  
1.  將新指令碼元件加入資料流程設計師介面，並將它設定為轉換。  
  
2.  將來源的輸出或另一個轉換的輸出連接到設計師中的新轉換元件。 這個輸出應該會提供來自資料**Person.Address**資料表**AdventureWorks**範例資料庫包含最少為**AddressID**和**縣 （市)**資料行。  
  
3.  開啟**指令碼轉換編輯器**。 在**的輸入資料行**頁面上，選取**AddressID**和**縣 （市)**資料行。  
  
4.  在**輸入和輸出**頁面上，新增和設定**AddressID**和**縣 （市)**輸出上的第一個輸出資料行。 加入第二個輸出，然後在第二個輸出上加入摘要值的輸出資料行。 將第一個輸出的 SynchronousInputID 屬性設定為 0，因為這個範例會將每一個輸入資料列明確地複製到第一個輸出。 新建立之輸出的 SynchronousInputID 屬性已經設定為 0。  
  
5.  重新命名輸入、輸出和新的輸出資料行，為它們提供更具描述性的名稱。 此範例會使用**MyAddressInput**做為名稱的輸入， **MyAddressOutput**和**MySummaryOutput**輸出，以及**MyRedmondCount**上第二個輸出的輸出資料行。  
  
6.  在**指令碼**頁面上，按一下**編輯指令碼**並輸入以下指令碼。 然後關閉 指令碼開發環境和**指令碼轉換編輯器**。  
  
7.  建立及設定預期的第一個輸出的目的地元件**AddressID**和**縣 （市)**資料行，例如[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]目的地、 或的範例目的地元件中所示範[與指令碼元件建立目的地](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-destination-with-the-script-component.md)。 然後將轉換的第一個輸出連接**MyAddressOutput**，到目的地元件。 您可以執行下列命令，以建立目的地資料表[!INCLUDE[tsql](../../includes/tsql-md.md)]命令**AdventureWorks**資料庫：  
  
    ```sql
    CREATE TABLE [Person].[Address2]([AddressID] [int] NOT NULL,  
        [City] [nvarchar](30) NOT NULL)  
    ```  
  
8.  為第二個輸出建立及設定另一個目的地元件。 然後將轉換的第二個輸出連接**MySummaryOutput**，到目的地元件。 因為第二個輸出會寫入具有單一值的單一資料列，所以您可以輕鬆地使用一般檔案連接管理員來設定目的地，此管理員會連接到具有單一資料行的新檔案。 在範例中，這個目的地資料行名為**MyRedmondCount**。  
  
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
  
  

