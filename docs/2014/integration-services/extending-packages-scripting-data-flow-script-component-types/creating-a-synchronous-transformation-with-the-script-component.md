---
title: 使用指令碼元件建立同步轉換 | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- synchronous outputs [Integration Services]
- transformation components [Integration Services]
- Script component [Integration Services], transformation components
ms.assetid: aa1bee1a-ab06-44d8-9944-4bff03d73016
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 7e2fc735cd4834fcb6e59550604b831b5d8790fb
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/22/2019
ms.locfileid: "58379976"
---
# <a name="creating-a-synchronous-transformation-with-the-script-component"></a>使用指令碼元件建立同步轉換
  您在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝的資料流程中使用轉換元件，以修改及分析從來源傳遞到目的地的資料。 具有同步輸出的轉換會處理通過該元件的每個輸入資料列。 具有非同步輸出的轉換會等到它收到所有的輸入資料列後，才完成其處理。 本主題討論同步轉換。 如需非同步轉換的資訊，請參閱[使用指令碼元件建立非同步轉換](../extending-packages-scripting-data-flow-script-component-types/creating-an-asynchronous-transformation-with-the-script-component.md)。 如需同步與非同步元件之間差異的詳細資訊，請參閱[了解同步和非同步轉換](../understanding-synchronous-and-asynchronous-transformations.md)。  
  
 如需指令碼元件的概觀，請參閱[使用指令碼元件擴充資料流程](../extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md)。  
  
 指令碼元件以及它為您產生的基礎結構程式碼，可大幅簡化開發自訂資料流程元件的程序。 不過，若要了解指令碼元件運作方式，閱讀[開發自訂資料流程元件](../extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md)的一節中有關開發自訂資料流程元件所必須遵循的步驟，尤其是[開發具有同步輸出的自訂轉換元件](../extending-packages-custom-objects-data-flow-types/developing-a-custom-transformation-component-with-synchronous-outputs.md)，可能會非常有幫助。  
  
## <a name="getting-started-with-a-synchronous-transformation-component"></a>開始使用同步轉換元件  
 當您將指令碼元件新增至 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計工具的 [資料流程] 窗格時，就會開啟 [選取指令碼元件類型] 對話方塊，並提示您選取 [來源]、[目的地] 或是 [轉換] 元件類型。 在這個對話方塊中，選取 [轉換]。  
  
## <a name="configuring-a-synchronous-transformation-component-in-metadata-design-mode"></a>在中繼資料設計模式中設定同步轉換元件  
 在您選取可建立轉換元件的選項之後，請使用 [指令碼轉換編輯器] 來設定元件。 如需詳細資訊，請參閱[在指令碼元件編輯器中設定指令碼元件](../extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md)。  
  
 若要設定指令碼元件的指令碼語言，請在 [指令碼轉換編輯器] 的 [指令碼] 頁面上設定 **ScriptLanguage** 屬性。  
  
> [!NOTE]  
>  若要為指令碼元件設定預設的指令碼語言，請使用 [選項] 對話方塊中 [一般] 頁面上的 [指令碼語言] 選項。 如需相關資訊，請參閱 [General Page](../general-page-of-integration-services-designers-options.md)。  
  
 資料流程轉換元件有一個輸入，而且支援一或多個輸出。 設定元件的輸入與輸出是您必須在中繼資料設計模式下完成的其中一個步驟，方法是在撰寫自訂指令碼之前先使用 [指令碼轉換編輯器]。  
  
### <a name="configuring-input-columns"></a>設定輸入資料行  
 轉換元件有一個輸入。  
  
 在 [指令碼轉換編輯器] 的 [輸入資料行] 頁面上，資料行清單會從資料流程中的上游元件輸出顯示可用的資料行。 選取要轉換或通過的資料行。 將任何您要就地轉換的資料行標示成「讀取/寫入」。  
  
 如需 [指令碼轉換編輯器] 的 [輸入資料行] 頁面的詳細資訊，請參閱[指令碼轉換編輯器 &#40;輸入資料行頁面&#41;](../script-transformation-editor-input-columns-page.md)。  
  
### <a name="configuring-inputs-outputs-and-output-columns"></a>設定輸入、輸出及輸出資料行  
 轉換元件支援一或多個輸出。  
  
 在 [指令碼轉換編輯器] 的 [輸入及輸出] 頁面上，您可以看到已建立單一輸出，但是輸出沒有資料行。 在編輯器的此頁面上，您可能會需要或想要設定下列項目。  
  
-   建立一或多個其他輸出，例如含有非預期值的資料列之模擬錯誤輸出。 使用 [新增輸出] 和 [移除輸出] 按鈕管理同步轉換元件的輸出。 所有的輸入資料列都會導向至所有可用的輸出，除非您指定想要將每個資料列重新導向至某個輸出或是另一個輸出。 您為輸出上的 `ExclusionGroup` 屬性指定非零的整數值，以指出想要重新導向資料列。 在 `ExclusionGroup` 中輸入哪一個特定整數值來識別輸出並不重要，但是您必須為指定的輸出群組持續地使用相同的整數。  
  
    > [!NOTE]  
    >  當您不想要輸出所有的資料列時，也可以使用具有單一輸出的非零 `ExclusionGroup` 屬性值。 不過，在此情況下，您必須為要傳送至輸出的每個資料列，明確地呼叫 **DirectRowTo\<outputbuffer>** 方法。  
  
-   指派更具描述性的名稱給輸入與輸出。 指令碼元件使用這些名稱來產生具類型的存取子屬性，您將使用這些屬性來參考指令碼中的輸入和輸出。  
  
-   保留資料行的原狀以進行同步轉換。 一般而言，同步轉換不會將資料行加入資料流程。 資料會在緩衝區中就地修改，而緩衝區則會傳遞至資料流程中的下一個元件。 如果是這樣的情況，您不必在轉換的輸出上明確地加入和設定輸出資料行。 輸出會出現在編輯器中，但沒有任何明確定義的資料行。  
  
-   將新資料行加入資料列層級錯誤的模擬錯誤輸出。 通常在相同 `ExclusionGroup` 中的多個輸出都有相同的一組輸出資料行。 然而，如果您正在建立模擬的錯誤輸出，可能會想要加入更多的資料行以包含錯誤資訊。 如需資料流程引擎如何處理錯誤資料列的資訊，請參閱[使用資料流程元件中的錯誤輸出](../extending-packages-custom-objects/data-flow/using-error-outputs-in-a-data-flow-component.md)。 不過，在指令碼元件中，您必須撰寫自已的程式碼，以適當的錯誤資訊填寫其他資料行。 如需詳細資訊，請參閱[模擬指令碼元件的錯誤輸出](../extending-packages-scripting-data-flow-script-component-examples/simulating-an-error-output-for-the-script-component.md)。  
  
 如需 [指令碼轉換編輯器] 之 [輸入及輸出] 頁面的詳細資訊，請參閱[指令碼轉換編輯器 &#40;輸入及輸出頁面&#41;](../script-transformation-editor-inputs-and-outputs-page.md)。  
  
### <a name="adding-variables"></a>加入變數  
 如果您想要在您的指令碼中使用現有的變數，您可以將其加入`ReadOnlyVariables`並`ReadWriteVariables`屬性欄位上**指令碼**頁面**指令碼轉換編輯器**。  
  
 當您在屬性欄位中加入多個變數時，請用逗號分隔變數名稱。 您也可以選取多個變數，按一下省略符號 (**...**) 按鈕旁`ReadOnlyVariables`並`ReadWriteVariables`屬性欄位，然後選取 [在變數**選取變數**] 對話方塊。  
  
 如需如何利用指令碼元件使用變數的一般資訊，請參閱[在指令碼元件中使用變數](../extending-packages-scripting/data-flow-script-component/using-variables-in-the-script-component.md)。  
  
 如需 [指令碼轉換編輯器] 的 [指令碼] 頁面的詳細資訊，請參閱[指令碼轉換編輯器 &#40;指令碼頁面&#41;](../script-transformation-editor-script-page.md)。  
  
## <a name="scripting-a-synchronous-transformation-component-in-code-design-mode"></a>在程式碼設計模式中編寫同步轉換元件的指令碼  
 在您設定好元件的中繼資料之後，便可撰寫自訂指令碼。 在 [指令碼轉換編輯器] 的 [指令碼] 頁面上，按一下 [編輯指令碼]，開啟 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications (VSTA) IDE 以新增自訂指令碼。 所使用的指令碼語言取決於您選取 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic 還是 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C# 作為 [指令碼] 頁面上 **ScriptLanguage** 屬性的指令碼語言。  
  
 如需使用指令碼元件所建立之各種元件都適用的重要資訊，請參閱[編碼和偵錯指令碼元件](../extending-packages-scripting/data-flow-script-component/using-variables-in-the-script-component.md)。  
  
### <a name="understanding-the-auto-generated-code"></a>了解自動產生的程式碼  
 當您在建立和設定轉換元件之後開啟 VSTA IDE，可編輯的 `ScriptMain` 類別會出現在程式碼編輯器中，並具有 `ProcessInputRow` 方法的 Stub。 `ScriptMain` 類別是您將撰寫自訂程式碼的地方，而 `ProcessInputRow` 則是轉換元件中最重要的方法。  
  
 如果您開啟**Project Explorer**  視窗中的在 VSTA 中，您所見，指令碼元件也會產生唯讀`BufferWrapper`和`ComponentWrapper`專案項目。 `ScriptMain` 類別會繼承 `UserComponent` 專案項目中的 `ComponentWrapper` 類別。  
  
 在執行階段，資料流程引擎會叫用 `ProcessInput` 類別中的 `UserComponent` 方法，它會覆寫 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ProcessInput%2A> 父類別的 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent> 方法。 `ProcessInput` 方法接著會在輸入緩衝區的資料列中執行迴圈，並為每個資料列呼叫一次 `ProcessInputRow` 方法。  
  
### <a name="writing-your-custom-code"></a>撰寫您的自訂程式碼  
 具有同步輸出的轉換元件是所有資料流程元件中最容易撰寫的。 例如，在本主題稍後所顯示的單一輸出範例是由下列自訂程式碼所組成：  
  
```vb  
Row.City = UCase(Row.City)  
```  
  
```csharp  
Row.City = (Row.City).ToUpper();  
  
```  
  
 若要完成建立自訂同步轉換元件，可以使用覆寫的 `ProcessInputRow` 方法，轉換輸入緩衝區之每個資料列中的資料。 資料流程引擎會在變滿時將這個緩衝區傳遞到資料流程中的下一個元件。  
  
 視您的需求而定，您也可能會想要在 `PreExecute` 與 `PostExecute` 方法 (可在 `ScriptMain` 類別中取得) 中撰寫指令碼，以執行初步或是最後的處理。  
  
### <a name="working-with-multiple-outputs"></a>使用多個輸出  
 相較於之前討論的單一輸出狀況，將輸入資料列導向兩個或更多可能的輸出之一，並不需要更多的自訂程式碼。 例如，在本主題稍後所顯示的雙輸出範例是由下列自訂程式碼所組成：  
  
```vb  
Row.City = UCase(Row.City)  
If Row.City = "REDMOND" Then  
    Row.DirectRowToMyRedmondAddresses()  
Else  
    Row.DirectRowToMyOtherAddresses()  
End If  
```  
  
```csharp  
Row.City = (Row.City).ToUpper();  
  
if (Row.City=="REDMOND")  
{  
    Row.DirectRowToMyRedmondAddresses();  
}  
else  
{  
    Row.DirectRowToMyOtherAddresses();  
}  
```  
  
 在這個範例中，根據您所設定的輸出名稱而定，指令碼元件會為您產生 **DirectRowTo\<OutputBufferX>** 方法。 您可以使用類似的程式碼將錯誤資料列導向模擬的錯誤輸出。  
  
## <a name="examples"></a>範例  
 以下範例示範在 `ScriptMain` 類別中所需的自訂程式碼，以建立同步轉換元件。  
  
> [!NOTE]  
>  這些範例會使用**Person.Address**資料表中`AdventureWorks`範例資料庫，並將傳遞其第一個和第四個資料行**intAddressID**和**nvarchar (30) 縣 （市)** 資料行，並透過資料流程。 在本章節中的來源、轉換和目的地範例使用相同的資料。 每個範例都會記載其他必要條件與假設。  
  
### <a name="single-output-synchronous-transformation-example"></a>單一輸出同步轉換範例  
 此範例示範具有單一輸出的同步轉換元件。 此轉換會通過 **AddressID** 資料行，並將 **City** 資料行轉換為大寫字元。  
  
 如果您要執行這個範例程式碼，必須依下列方式設定封裝與元件：  
  
1.  將新指令碼元件加入資料流程設計師介面，並將它設定為轉換。  
  
2.  將來源的輸出或另一個轉換的輸出連接到 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師中的新轉換元件。 此輸出應會提供資料**Person.Address**的資料表`AdventureWorks`範例資料庫，其中包含**AddressID**並**縣 （市)** 資料行。  
  
3.  開啟**指令碼轉換編輯器**。 在 [輸入資料行] 頁面上，選取 [AddressID] 和 [City] 資料行。 將 **City** 資料行標示為讀取/寫入。  
  
4.  在 [輸入及輸出] 頁面上，以更具描述性的名稱重新命名輸入與輸出；例如 **MyAddressInput** 和 **MyAddressOutput**。 請注意，輸出的 `SynchronousInputID` 會對應至輸入的 `ID`。 因此，您不必加入和設定輸出資料行。  
  
5.  在 [指令碼] 頁面上，按一下 [編輯指令碼]，並輸入以下指令碼。 然後關閉指令碼開發環境以及 [指令碼轉換編輯器]。  
  
6.  建立和設定需要 **AddressID** 和 **City** 資料行的目的地元件 (例如 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 目的地)，或是在[使用指令碼元件建立目的地](../extending-packages-scripting-data-flow-script-component-types/creating-a-destination-with-the-script-component.md)中所示範的範例目的地元件。 然後將轉換的輸出連接到目的地元件。 您可以在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 資料庫中執行下列 `AdventureWorks` 命令，以建立目的地資料表：  
  
    ```  
    CREATE TABLE [Person].[Address2]([AddressID] [int] NOT NULL,  
        [City] [nvarchar](30) NOT NULL)  
    ```  
  
7.  執行範例。  
  
```vb  
Public Class ScriptMain  
    Inherits UserComponent  
  
    Public Overrides Sub MyAddressInput_ProcessInputRow(ByVal Row As MyAddressInputBuffer)  
  
        Row.City = UCase(Row.City)  
  
    End Sub  
  
End Class  
```  
  
```csharp  
public class ScriptMain:  
    UserComponent  
  
{  
    public override void MyAddressInput_ProcessInputRow(MyAddressInputBuffer Row)  
    {  
  
        Row.City = (Row.City).ToUpper();  
  
    }  
  
}  
```  
  
### <a name="two-output-synchronous-transformation-example"></a>雙輸出同步轉換範例  
 此範例示範的同步轉換元件具有兩個輸出。 此轉換會通過 **AddressID** 資料行，並將 **City** 資料行轉換為大寫字元。 如果城市名稱是 Redmond，它會將資料列導向其中一個輸出，並將所有的其他資料列導向另一個輸出。  
  
 如果您要執行這個範例程式碼，必須依下列方式設定封裝與元件：  
  
1.  將新指令碼元件加入資料流程設計師介面，並將它設定為轉換。  
  
2.  將來源的輸出或另一個轉換的輸出連接到 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師中的新轉換元件。 此輸出應會提供資料**Person.Address**的資料表`AdventureWorks`範例資料庫，其中包含至少**AddressID**並**縣 （市)** 資料行。  
  
3.  開啟**指令碼轉換編輯器**。 在 [輸入資料行] 頁面上，選取 [AddressID] 和 [City] 資料行。 將 **City** 資料行標示為讀取/寫入。  
  
4.  在 [輸入及輸出] 頁面上，建立第二個輸出。 在加入新輸出之後，請確定將其 `SynchronousInputID` 設定為輸入的 `ID`。 在預設會建立的第一個輸出上已經設定這個屬性。 對於每個輸出，請將 `ExclusionGroup` 屬性設定為相同的非零值，以指出您將在兩個互斥輸出之間分割輸入資料列。 您不必將任何輸出資料行加入輸出。  
  
5.  使用更具描述性的名稱重新命名輸入與輸出，例如 **MyAddressInput**、**MyRedmondAddresses** 和 **MyOtherAddresses**。  
  
6.  在 [指令碼] 頁面上，按一下 [編輯指令碼]，並輸入以下指令碼。 然後關閉指令碼開發環境以及 [指令碼轉換編輯器]。  
  
7.  建立和設定兩個需要 **AddressID** 和 **City** 資料行的目的地元件，例如 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 目的地、一般檔案目的地，或是在[使用指令碼元件建立目的地](../extending-packages-scripting-data-flow-script-component-types/creating-a-destination-with-the-script-component.md)中所示範的範例目的地元件。 然後將每個轉換輸出連接到其中一個目的地元件。 您可以在 `AdventureWorks` 資料庫中執行類似下列程式碼 (具有唯一的資料表名稱) 的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 命令，以建立目的地資料表：  
  
    ```  
    CREATE TABLE [Person].[Address2](  
        [AddressID] [int] NOT NULL,  
        [City] [nvarchar](30) NOT NULL  
    ```  
  
8.  執行範例。  
  
```vb  
Public Class ScriptMain  
    Inherits UserComponent  
  
    Public Overrides Sub MyAddressInput_ProcessInputRow(ByVal Row As MyAddressInputBuffer)  
  
        Row.City = UCase(Row.City)  
  
        If Row.City = "REDMOND" Then  
            Row.DirectRowToMyRedmondAddresses()  
        Else  
            Row.DirectRowToMyOtherAddresses()  
        End If  
  
    End Sub  
  
End Class  
```  
  
```csharp  
public class ScriptMain:  
    UserComponent  
  
public override void MyAddressInput_ProcessInputRow(MyAddressInputBuffer Row)  
    {  
  
        Row.City = (Row.City).ToUpper();  
  
        if (Row.City == "REDMOND")  
        {  
            Row.DirectRowToMyRedmondAddresses();  
        }  
        else  
        {  
            Row.DirectRowToMyOtherAddresses();  
        }  
  
    }  
}  
```  
  
|![](./media/creating-a-synchronous-transformation-with-the-script-component/dts-16.gif)  **保持最新的 Integration Services**<br /> 若要取得 Microsoft 的最新下載、文件、範例和影片以及社群中的精選解決方案，請瀏覽 MSDN 上的 [!INCLUDE[ssISnoversion](../../includes/msconame-md.md)] 頁面：<br /><br /> [瀏覽 MSDN 上的 Integration Services 頁面](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 若要得到這些更新的自動通知，請訂閱該頁面上所提供的 RSS 摘要。  
  
## <a name="see-also"></a>另請參閱  
 [了解同步和非同步轉換](../understanding-synchronous-and-asynchronous-transformations.md)[使用指令碼元件建立非同步轉換](../extending-packages-scripting-data-flow-script-component-types/creating-an-asynchronous-transformation-with-the-script-component.md)[開發具有同步的自訂轉換元件輸出](../extending-packages-custom-objects-data-flow-types/developing-a-custom-transformation-component-with-synchronous-outputs.md)  
  
  
