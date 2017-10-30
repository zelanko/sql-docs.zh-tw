---
title: "使用指令碼元件建立同步轉換 |Microsoft 文件"
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
- synchronous outputs [Integration Services]
- transformation components [Integration Services]
- Script component [Integration Services], transformation components
ms.assetid: aa1bee1a-ab06-44d8-9944-4bff03d73016
caps.latest.revision: 64
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 3d4a507c31f77449aba7eb884c39bf68c7c78581
ms.contentlocale: zh-tw
ms.lasthandoff: 09/26/2017

---
# <a name="creating-a-synchronous-transformation-with-the-script-component"></a>使用指令碼元件建立同步轉換
  您在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝的資料流程中使用轉換元件，以修改及分析從來源傳遞到目的地的資料。 具有同步輸出的轉換會處理通過該元件的每個輸入資料列。 具有非同步輸出的轉換會等到它收到所有的輸入資料列後，才完成其處理。 本主題討論同步轉換。 非同步轉換的相關資訊，請參閱[使用指令碼元件建立非同步轉換](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-an-asynchronous-transformation-with-the-script-component.md)。 如需有關同步和非同步元件之間差異的詳細資訊，請參閱[了解同步和非同步轉換](../../integration-services/understanding-synchronous-and-asynchronous-transformations.md)。  
  
 如需指令碼元件的概觀，請參閱[Extending the Data Flow with Script Component](../../integration-services/extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md)。  
  
 指令碼元件以及它為您產生的基礎結構程式碼，可大幅簡化開發自訂資料流程元件的程序。 不過，若要了解指令碼元件如何運作，您可能會發現閱讀上開發自訂資料流程元件的區段中，您必須遵循的步驟[開發自訂資料流程元件](../../integration-services/extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md)，，尤其是[開發具有同步輸出的自訂轉換元件](../../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-transformation-component-with-synchronous-outputs.md)。  
  
## <a name="getting-started-with-a-synchronous-transformation-component"></a>開始使用同步轉換元件  
 當您將指令碼元件加入至 [資料流程] 窗格的[!INCLUDE[ssIS](../../includes/ssis-md.md)]設計工具中，**選取指令碼元件類型**對話方塊會開啟，並提示您選取的來源、 目的地或轉換元件的類型。 在此對話方塊中，選取**轉換**。  
  
## <a name="configuring-a-synchronous-transformation-component-in-metadata-design-mode"></a>在中繼資料設計模式中設定同步轉換元件  
 您選取選項以建立轉換元件之後，您會設定元件利用**指令碼轉換編輯器**。 如需詳細資訊，請參閱[設定指令碼元件指令碼元件編輯器中](../../integration-services/extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md)。  
  
 若要設定指令碼元件的指令碼語言，您將**ScriptLanguage**屬性**指令碼**頁面**指令碼轉換編輯器**。  
  
> [!NOTE]  
>  若要設定預設的指令碼語言指令碼元件，請使用**指令碼語言**選項**一般**頁面**選項** 對話方塊。 如需詳細資訊，請參閱[一般頁面](https://msdn.microsoft.com/library/ms189436(v=sql.110).aspx)。  
  
 資料流程轉換元件有一個輸入，而且支援一或多個輸出。 設定輸入和輸出的元件是其中一個步驟，您必須使用中繼資料設計模式中，在完成**指令碼轉換編輯器**，然後才能在您撰寫自訂指令碼。  
  
### <a name="configuring-input-columns"></a>設定輸入資料行  
 轉換元件有一個輸入。  
  
 在**的輸入資料行**頁面**指令碼轉換編輯器 中，**資料行清單顯示可用的資料行的上游元件輸出從資料流程中的資料。 選取要轉換或通過的資料行。 將任何您要就地轉換的資料行標示成「讀取/寫入」。  
  
 如需有關**的輸入資料行**頁面**指令碼轉換編輯器**，請參閱[指令碼轉換編輯器 &#40; 輸入資料行頁面 &#41;](../../integration-services/data-flow/transformations/script-transformation-editor-input-columns-page.md)。  
  
### <a name="configuring-inputs-outputs-and-output-columns"></a>設定輸入、輸出及輸出資料行  
 轉換元件支援一或多個輸出。  
  
 在**輸入和輸出**頁面**指令碼轉換編輯器**，您可以看到，已建立單一輸出，但是輸出沒有資料行。 在編輯器的此頁面上，您可能會需要或想要設定下列項目。  
  
-   建立一或多個其他輸出，例如含有非預期值的資料列之模擬錯誤輸出。 使用**加入輸出**和**移除輸出**按鈕管理同步轉換元件的輸出。 所有的輸入資料列都會導向至所有可用的輸出，除非您指定想要將每個資料列重新導向至某個輸出或是另一個輸出。 您表示您想要藉由指定非零的整數值的資料列重新導向**ExclusionGroup**輸出上的屬性。 在中輸入特定的整數值**ExclusionGroup**來識別輸出並不重要，但您必須指定群組的輸出，一致地使用相同的整數。  
  
    > [!NOTE]  
    >  您也可以使用非零**ExclusionGroup**具有單一輸出，當您不想要輸出所有資料列的屬性值。 不過，在此情況下，您必須明確呼叫**DirectRowTo\<outputbuffer >**您想要傳送至輸出每個資料列的方法。  
  
-   指派更具描述性的名稱給輸入與輸出。 指令碼元件使用這些名稱來產生具類型的存取子屬性，您將使用這些屬性來參考指令碼中的輸入和輸出。  
  
-   保留資料行的原狀以進行同步轉換。 一般而言，同步轉換不會將資料行加入資料流程。 資料會在緩衝區中就地修改，而緩衝區則會傳遞至資料流程中的下一個元件。 如果是這樣的情況，您不必在轉換的輸出上明確地加入和設定輸出資料行。 輸出會出現在編輯器中，但沒有任何明確定義的資料行。  
  
-   將新資料行加入資料列層級錯誤的模擬錯誤輸出。 多個在相同的輸出通常**ExclusionGroup**擁有相同的輸出資料行。 然而，如果您正在建立模擬的錯誤輸出，可能會想要加入更多的資料行以包含錯誤資訊。 如需如何資料流程引擎的相關資訊，處理錯誤資料列，請參閱[資料流程元件中使用錯誤輸出](../../integration-services/extending-packages-custom-objects/data-flow/using-error-outputs-in-a-data-flow-component.md)。 不過，在指令碼元件中，您必須撰寫自已的程式碼，以適當的錯誤資訊填寫其他資料行。 如需詳細資訊，請參閱[模擬錯誤輸出指令碼元件](../../integration-services/extending-packages-scripting-data-flow-script-component-examples/simulating-an-error-output-for-the-script-component.md)。  
  
 如需有關**輸入和輸出**頁面**指令碼轉換編輯器**，請參閱[指令碼轉換編輯器 &#40; 輸入及輸出頁面 &#41;](../../integration-services/data-flow/transformations/script-transformation-editor-inputs-and-outputs-page.md)。  
  
### <a name="adding-variables"></a>加入變數  
 如果您想要在您的指令碼中使用現有的變數，您可以將其加入**[readonlyvariables]**和**[readwritevariables]**屬性欄位上**指令碼**頁面**指令碼轉換編輯器**。  
  
 當您在屬性欄位中加入多個變數時，請用逗號分隔變數名稱。 您也可以選取多個變數，依序按一下省略符號 (**...**) 旁邊**readonlyvariables**和**readwritevariables**屬性欄位，然後選取 在變數**選取變數**對話方塊。  
  
 如需如何使用指令碼元件中使用變數的一般資訊，請參閱[在指令碼元件中使用變數](../../integration-services/extending-packages-scripting/data-flow-script-component/using-variables-in-the-script-component.md)。  
  
 如需有關**指令碼**頁面**指令碼轉換編輯器**，請參閱[指令碼轉換編輯器 &#40;指令碼頁面 &#41;](../../integration-services/data-flow/transformations/script-transformation-editor-script-page.md).  
  
## <a name="scripting-a-synchronous-transformation-component-in-code-design-mode"></a>在程式碼設計模式中編寫同步轉換元件的指令碼  
 在您設定好元件的中繼資料之後，便可撰寫自訂指令碼。 在**指令碼轉換編輯器**上**指令碼**頁面上，按一下**編輯指令碼**開啟[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications (VSTA) IDE您可以在其中加入自訂指令碼。 您使用的指令碼語言，取決於您選取[!INCLUDE[msCoName](../../includes/msconame-md.md)]Visual Basic 或[!INCLUDE[msCoName](../../includes/msconame-md.md)]Visual C# 做為指令碼語言**ScriptLanguage**屬性**指令碼**頁面。  
  
 適用於所有類型的元件所使用的指令碼元件建立的重要資訊，請參閱[編碼和偵錯指令碼元件](../../integration-services/extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md)。  
  
### <a name="understanding-the-auto-generated-code"></a>了解自動產生的程式碼  
 當您開啟 VSTA IDE 之後您建立, 和設定轉換元件，可編輯**ScriptMain**類別會出現在虛設常式的程式碼編輯器**ProcessInputRow**方法。 **ScriptMain**類別是您將在其中撰寫自訂程式碼和**ProcessInputRow**是最重要的方法中的轉換元件。  
  
 如果您開啟**Project Explorer**視窗在 VSTA 中的，您可以看到，指令碼元件也會產生唯讀**BufferWrapper**和**ComponentWrapper**專案項目。 **ScriptMain**類別繼承自**UserComponent**類別**ComponentWrapper**專案項目。  
  
 在執行階段，資料流程引擎會叫用**ProcessInput**方法中的**UserComponent**類別，它會覆寫<xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ProcessInput%2A>方法<xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent>父類別。 **ProcessInput**方法接著執行迴圈的輸入的緩衝區和呼叫中的資料列**ProcessInputRow**方法一次，每個資料列。  
  
### <a name="writing-your-custom-code"></a>撰寫您的自訂程式碼  
 具有同步輸出的轉換元件是所有資料流程元件中最容易撰寫的。 例如，在本主題稍後所顯示的單一輸出範例是由下列自訂程式碼所組成：  
  
```vb  
Row.City = UCase(Row.City)  
```  
  
```csharp  
Row.City = (Row.City).ToUpper();  
  
```  
  
 若要完成建立自訂同步轉換元件，請使用覆寫**ProcessInputRow**方法轉換輸入緩衝區的每個資料列中的資料。 資料流程引擎會在變滿時將這個緩衝區傳遞到資料流程中的下一個元件。  
  
 根據您的需求，您也可以撰寫指令碼**PreExecute**和**PostExecute**中可用方法**ScriptMain**類別，以執行初步或最終處理。  
  
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
  
 在此範例中，指令碼元件會產生**DirectRowTo\<OutputBufferX >**方法，根據您設定的輸出名稱。 您可以使用類似的程式碼將錯誤資料列導向模擬的錯誤輸出。  
  
## <a name="examples"></a>範例  
 以下範例示範自訂程式碼所需的**ScriptMain**類別來建立同步轉換元件。  
  
> [!NOTE]  
>  這些範例使用**Person.Address**資料表中**AdventureWorks**範例資料庫，並傳遞其第一個和第四個資料行， **intAddressID**和**nvarchar (30) 縣 （市)** ，經過資料流資料行。 在本章節中的來源、轉換和目的地範例使用相同的資料。 每個範例都會記載其他必要條件與假設。  
  
### <a name="single-output-synchronous-transformation-example"></a>單一輸出同步轉換範例  
 此範例示範具有單一輸出的同步轉換元件。 此轉換會通過**AddressID**資料行並轉換**縣 （市)**成大寫的資料行。  
  
 如果您要執行這個範例程式碼，必須依下列方式設定封裝與元件：  
  
1.  將新指令碼元件加入資料流程設計師介面，並將它設定為轉換。  
  
2.  將來源的輸出或另一個轉換的輸出連接到 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師中的新轉換元件。 這個輸出應該會提供來自資料**Person.Address**資料表**AdventureWorks**範例資料庫包含**AddressID**和**縣 （市)**資料行。  
  
3.  開啟**指令碼轉換編輯器**。 在**的輸入資料行**頁面上，選取**AddressID**和**縣 （市)**資料行。 標記**縣 （市)**為讀取/寫入的資料行。  
  
4.  在**輸入和輸出**頁面、 重新命名輸入和輸出，是使用更具描述性的名稱，例如**MyAddressInput**和**MyAddressOutput**。 請注意， **SynchronousInputID**的輸出對應至**識別碼**的輸入。 因此，您不必加入和設定輸出資料行。  
  
5.  在**指令碼**頁面上，按一下**編輯指令碼**並輸入以下指令碼。 然後關閉 指令碼開發環境和**指令碼轉換編輯器**。  
  
6.  建立及設定一個目的地元件，必須要有**AddressID**和**縣 （市)**資料行，例如[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]目的地、 或的範例目的地元件中所示範[與指令碼元件建立目的地](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-destination-with-the-script-component.md)。 然後將轉換的輸出連接到目的地元件。 您可以執行下列命令，以建立目的地資料表[!INCLUDE[tsql](../../includes/tsql-md.md)]命令**AdventureWorks**資料庫：  
  
    ```sql
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
 此範例示範的同步轉換元件具有兩個輸出。 此轉換會通過**AddressID**資料行並轉換**縣 （市)**成大寫的資料行。 如果城市名稱是 Redmond，它會將資料列導向其中一個輸出，並將所有的其他資料列導向另一個輸出。  
  
 如果您要執行這個範例程式碼，必須依下列方式設定封裝與元件：  
  
1.  將新指令碼元件加入資料流程設計師介面，並將它設定為轉換。  
  
2.  將來源的輸出或另一個轉換的輸出連接到 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師中的新轉換元件。 這個輸出應該會提供來自資料**Person.Address**資料表**AdventureWorks**範例資料庫包含最少為**AddressID**和**縣 （市)**資料行。  
  
3.  開啟**指令碼轉換編輯器**。 在**的輸入資料行**頁面上，選取**AddressID**和**縣 （市)**資料行。 標記**縣 （市)**為讀取/寫入的資料行。  
  
4.  在**輸入和輸出**頁面上，建立第二個輸出。 加入新輸出之後，請確定您設定其**SynchronousInputID**至**識別碼**的輸入。 在預設會建立的第一個輸出上已經設定這個屬性。 每個輸出，設定**ExclusionGroup**為相同的非零值，表示您將分割兩個互斥輸出之間的輸入資料列的屬性。 您不必將任何輸出資料行加入輸出。  
  
5.  重新命名輸入與輸出使用更具描述性的名稱，例如**MyAddressInput**， **MyRedmondAddresses**，和**MyOtherAddresses**。  
  
6.  在**指令碼**頁面上，按一下**編輯指令碼**並輸入以下指令碼。 然後關閉 指令碼開發環境和**指令碼轉換編輯器**。  
  
7.  建立及設定預期的兩個目的地元件**AddressID**和**縣 （市)**資料行，例如[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]目的地、 一般檔案目的地，或是的範例目的地元件中所示範[與指令碼元件建立目的地](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-destination-with-the-script-component.md)。 然後將每個轉換輸出連接到其中一個目的地元件。 您可以執行，以建立目的地資料表[!INCLUDE[tsql](../../includes/tsql-md.md)]命令類似於 （使用唯一資料表名稱） 中的下列**AdventureWorks**資料庫：  
  
    ```sql
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
  
## <a name="see-also"></a>另請參閱  
 [了解同步和非同步轉換](~/integration-services/understanding-synchronous-and-asynchronous-transformations.md   
 [使用指令碼元件建立非同步轉換](~/integration-services/extending-packages-scripting-data-flow-script-component-types/creating-an-asynchronous-transformation-with-the-script-component.md   
 [開發具有同步輸出的自訂轉換元件](~/integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-transformation-component-with-synchronous-outputs.md  
  
  



