---
title: 在指令碼元件編輯器中設定指令碼元件 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- SSIS Script component
- Script Component Editor
- SSIS Script component, configuring
- Script component [Integration Services], configuring
ms.assetid: 586dd799-f383-4d6d-b1a1-f09233d14f0a
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 1b2b588c61742d5ab9c57d934b0f4f11230f1ca5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "62894812"
---
# <a name="configuring-the-script-component-in-the-script-component-editor"></a>在指令碼元件編輯器中設定指令碼元件
  在腳本元件中撰寫自訂程式碼之前，您必須先選取要建立的資料流程元件類型-來源、轉換或目的地，然後在 [**腳本轉換編輯器**] 中設定元件的中繼資料和屬性。  
  
## <a name="selecting-the-type-of-component-to-create"></a>選取要建立的元件類型  
 當您將指令碼元件新增至 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 設計工具的 [資料流程] 窗格時，[選取指令碼元件類型]**** 對話方塊便會出現。 您可以將元件預先設定為來源、轉換或目的地。 在做出初步選擇之後，便可繼續在 [指令碼轉換編輯器]**** 中設定元件。  
  
 若要為指令碼元件設定預設的指令碼語言，請使用 [選項]**** 對話方塊的 [一般]**** 頁面上的 [指令碼語言]**** 選項。 如需相關資訊，請參閱 [General Page](../../general-page-of-integration-services-designers-options.md)。  
  
## <a name="understanding-the-two-design-time-modes"></a>了解兩個設計階段模式  
 在 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 設計師中，指令碼元件有中繼資料設計與程式碼設計兩種模式。  
  
 當您開啟 [指令碼轉換編輯器]**** 時，元件會進入中繼資料設計模式。 在此模式中，您可以選取輸入資料行，以及加入或設定輸出與輸出資料行，但是無法撰寫程式碼。 在您已設定好元件的中繼資料之後，便可切換到程式碼設計模式以撰寫指令碼。  
  
 當您按一下 [編輯指令碼]**** 以切換到程式碼設計模式時，指令碼元件會鎖定中繼資料以防止其他變更，接著會從輸入和輸出的中繼資料自動產生基底程式碼。 在完成自動產生的程式碼之後，將可以輸入自訂程式碼。 您的程式碼使用自動產生的基底類別以處理輸入資料列、存取緩衝區和緩衝區中的資料行，以及從封裝擷取連接管理員與變數，全部都做為強式類型的物件。  
  
 在程式碼設計模式中輸入自訂程式碼之後，便可切換回中繼資料設計模式。 這並不會刪除您已輸入的任何程式碼，然而，對中繼資料的後續變更會造成重新產生基底類別。 之後，您的元件可能會無法驗證，因為自訂程式碼所參考的物件可能不再存在或是可能已修改過。 在此情況下，您必須手動修正程式碼，才能針對重新產生的基底類別成功地編譯程式碼。  
  
## <a name="configuring-the-component-in-metadata-design-mode"></a>在中繼資料設計模式中設定元件  
 在中繼資料設計模式中，您可以選取輸入資料行，以及加入和設定輸出與輸出資料行，但是無法撰寫程式碼。 在您已設定好元件的中繼資料之後，便可切換到程式碼設計模式以撰寫指令碼。  
  
 您必須在自訂編輯器中設定的屬性，端視指令碼元件的使用而定。 指令碼元件可以設定為來源、轉換或目的地。 視元件的使用方式而定，可支援輸入、輸出或兩者。 您將撰寫的自訂程式碼會負責處理輸入和輸出資料列與資料行。  
  
### <a name="inputs-columns-page-of-the-script-transformation-editor"></a>指令碼轉換編輯器的輸入資料行頁面  
 會為轉換和目的地，但不會為來源顯示 [指令碼轉換編輯器]**** 的 [輸入資料行]**** 頁面。 在本頁，您選取要提供給自訂指令碼使用的輸入資料行，並指定這些資料行的唯讀或讀寫存取權限。  
  
 在將會根據此中繼資料產生的程式碼專案中，BufferWrapper 專案項目包含每個輸入的類別，而且這個類別包含每個選取的輸入資料行之具類型的存取子屬性。 `CustomerInput`例如，如果您從名為的輸入中選取整數**CustomerID**資料行和字串**CustomerName**資料行，則 BufferWrapper 專案專案會包含`CustomerInput`衍生自<xref:Microsoft.SqlServer.Dts.Pipeline.ScriptBuffer>的類別，而`CustomerInput`類別會公開名為**CustomerID**的整數屬性和名為**CustomerName**的字串屬性。 這個慣例使得撰寫具有類型檢查的程式碼變得可能，如下所示：  
  
```vb  
Dim currentCustomerID as Integer = CustomerInput.CustomerID  
Dim currentCustomerName as String = CustomerInput.CustomerName  
```  
  
 如需如何為特定類型的資料流程元件設定輸入資料行的詳細資訊，請參閱[開發特定類型的指令碼元件](../../extending-packages-scripting-data-flow-script-component-types/developing-specific-types-of-script-components.md)之下的適當範例。  
  
### <a name="inputs-and-outputs-page-of-the-script-transformation-editor"></a>指令碼轉換編輯器的輸入及輸出頁面  
 會為來源、轉換和目的地顯示 [指令碼轉換編輯器]**** 的 [輸入及輸出]**** 頁面。 在本頁，您可以加入、移除和設定要在自訂指令碼中使用的輸入、輸出和輸出資料行，但具有下列限制：  
  
-   當做為來源使用時，指令碼元件沒有輸入並且支援多個輸出。  
  
-   當做為轉換使用時，指令碼元件可支援一個輸入和多個輸出。  
  
-   當做為目的地使用時，指令碼元件支援一個輸入並且沒有輸出。  
  
 在將會根據此中繼資料產生的程式碼專案中，BufferWrapper 專案項目包含每個輸入與輸出的類別。 例如，如果您建立名`CustomerOutput`為的輸出，則 BufferWrapper 專案專案會包含一個`CustomerOutput`衍生自的類別<xref:Microsoft.SqlServer.Dts.Pipeline.ScriptBuffer>，而該`CustomerOutput`類別會包含所建立之每個輸出資料行的具類型存取子屬性。  
  
 您只能在 [輸入及輸出]**** 頁面上設定輸出資料行。 您可以在 [輸入資料行]**** 頁面上，選取轉換和目的地的輸入資料行。 在 BufferWrapper 專案項目中為您建立的具類型之存取子屬性對於輸出資料行而言將是唯寫的。 輸入資料行的存取子屬性將是唯讀或是讀取/寫入，端視您為 [輸入資料行]**** 頁面上的每個資料行所選取的使用類型而定。  
  
 如需為特定類型的資料流程元件設定輸入和輸出的詳細資訊，請參閱[開發特定類型的指令碼元件](../../extending-packages-scripting-data-flow-script-component-types/developing-specific-types-of-script-components.md)之下的適當範例。  
  
> [!NOTE]  
>  雖然您無法在指令碼元件中將輸出直接設定為錯誤輸出，以自動處理錯誤資料列，不過可以建立其他輸出與使用指令碼，適時地將資料列導向此輸出，以重新產生錯誤輸出的功能。 如需詳細資訊，請參閱[模擬指令碼元件的錯誤輸出](../../data-flow/transformations/script-component.md)。  
  
#### <a name="exclusiongroup-and-synchronousinputid-properties-of-outputs"></a>輸出的 ExclusionGroup 與 SynchronousInputID 屬性  
 
  `ExclusionGroup` 屬性只有在具有同步輸出的轉換中才有非零值，在這裡程式碼會執行篩選或分支，並將每個資料列導向具有相同非零 `ExclusionGroup` 值的其中一個輸出。 例如，轉換可以將資料列導向至預設輸出或是錯誤輸出。 當您為此狀況建立其他輸出時，請確定將 `SynchronousInputID` 屬性值設定為整數，以符合元件輸入的 `ID`。  
  
 
  `SynchronousInputID` 屬性只有在具有同步輸出的轉換中才有非零值。 如果此屬性的值是零，即表示輸出是非同步的。 若是同步輸出，亦即將資料列傳遞到選取的輸出或是沒有加入任何新資料列的輸出，則這個屬性應該會包含元件輸入的 `ID`。  
  
> [!NOTE]  
>  當 [**腳本轉換編輯器**] 建立第一個輸出時，編輯器會`SynchronousInputID`將輸出的屬性設定為`ID`元件輸入的。 然而，當編輯器建立後續的輸出時，編輯器會將這些輸出的 `SynchronousInputID` 屬性設定為零。  
>   
>  如果您要建立具有同步輸出的元件，則每個輸出都`SynchronousInputID`必須將其屬性`ID`設定為元件輸入的。 因此，編輯器在第一個輸出之後所建立的每個輸出，都必須將其 `SynchronousInputID` 值從零變更為元件輸入的 `ID`。  
>   
>  如果您以非同步輸出建立元件，每個輸出都必須將其 `SynchronousInputID` 屬性設定為零。 因此，第一個輸出必須將其`SynchronousInputID`值從`ID`元件的輸入變更為零。  
  
 如需將資料列導向指令碼元件中兩個同步輸出的其中一個的範例，請參閱[使用指令碼元件建立同步轉換](../../extending-packages-scripting-data-flow-script-component-types/creating-a-synchronous-transformation-with-the-script-component.md)。  
  
### <a name="object-names-in-generated-script"></a>產生的指令碼中的物件名稱  
 指令碼元件會剖析輸入與輸出的名稱，並剖析在輸入與輸出中的資料行名稱，而且會根據這些名稱在 BufferWrapper 專案項目中產生類別和屬性。 如果找到的名稱包括不屬於 Unicode 類別 (`UppercaseLetter`、`LowercaseLetter`、`TitlecaseLetter`、`ModifierLetter`、`OtherLetter` 或 `DecimalDigitLetter`) 的字元，在產生的名稱中會捨棄無效的字元。 例如，空格會予以捨棄，因此具為名稱為 **FirstName** 和 [**First Name**] 的兩個輸入資料行，都會轉譯為具有 **FirstName** 的資料行名稱，並產生無法預測的結果。 為了避免這個情況，指令碼元件所使用的輸入與輸出的名稱和輸入與輸出資料行的名稱，應該只包含本節中所列的 Unicode 類別裡的字元。  
  
### <a name="script-page-of-the-script-transformation-editor"></a>指令碼轉換編輯器的指令碼頁面  
 在 [指令碼工作編輯器]**** 的 [指令碼]**** 頁面上，為指令碼工作指派一個唯一的名稱與描述。 您也可以指派下列屬性的值。  
  
> [!NOTE]  
>  在 [!INCLUDE[ssISversion10](../../../includes/ssisversion10-md.md)] 和更新的版本中，所有指令碼都是先行編譯。 在舊版中，您可以藉由工作的 `Precompile` 屬性，指定指令碼是否已經先行編譯。  
  
#### <a name="validateexternalmetadata-property"></a>ValidateExternalMetadata 屬性  
 
  `ValidateExternalMetadata` 屬性的布林值可指定元件要在設計階段針對外部資料來源執行驗證，還是將驗證延後到執行階段執行。 依預設，此屬性的值是 `True`，也就是，外部中繼資料是在設計階段與執行階段進行驗證。 當外部資料來源在設計階段無法使用時，您可能會想要將此屬性的值設定為 `False`：例如，當封裝只在執行階段下載來源或建立目的地時。  
  
#### <a name="readonlyvariables-and-readwritevariables-properties"></a>ReadOnlyVariables 與 ReadWriteVariables 屬性  
 您可以輸入現有變數的逗號分隔清單做為這些屬性的值，使得變數可在指令碼元件程式碼中以唯讀或讀取/寫入的方式來存取。 在程式碼中，變數是透過自動產生的基底類別之 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ReadOnlyVariables%2A> 與 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ReadWriteVariables%2A> 屬性來存取。 如需詳細資訊，請參閱[在指令碼元件中使用變數](using-variables-in-the-script-component.md)。  
  
> [!NOTE]  
>  變數名稱會區分大小寫。  
  
#### <a name="scriptlanguage"></a>ScriptLanguage  
 您可以選擇使用 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic 或 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual C# 做為指令碼元件的程式設計語言。  
  
#### <a name="edit-script-button"></a>編輯指令碼按鈕  
 [編輯指令碼]**** 按鈕會開啟 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] Tools for Applications (VSTA) IDE，您可以在此撰寫自訂指令碼。 如需詳細資訊，請參閱[編碼和偵錯指令碼元件](coding-and-debugging-the-script-component.md)。  
  
### <a name="connection-managers-page-of-the-script-transformation-editor"></a>指令碼轉換編輯器的連接管理員頁面  
 在 [指令碼轉換編輯器]**** 的 [連線管理員]**** 頁面上，您可以新增和移除要在自訂指令碼中使用的連線管理員。 一般而言，您需要在建立來源或是目的地元件時，參考連接管理員。  
  
 在將會根據此中繼資料產生的程式碼專案中，`ComponentWrapper` 專案項目包含 `Connections` 集合類別，這個類別對於每個選取的連接管理員，都有具類型的存取子屬性。 每個具類型的存取子屬性都有做為連接管理員的相同名稱，並且會傳回連接管理員參考做為 <xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.IDTSConnectionManager100> 的執行個體。 例如，如果您已在編輯器的 [連線管理員]`MyADONETConnection`** 頁面中新增名為 ** 的連線管理員，就可以使用下列程式碼，取得指令碼中連線管理員的參考：  
  
```vb  
Dim myADONETConnectionManager As IDTSConnectionManager100 = _  
    Me.Connections.MyADONETConnection  
```  
  
 如需詳細資訊，請參閱[在指令碼元件中連線至資料來源](connecting-to-data-sources-in-the-script-component.md)。  
  
![Integration Services 圖示（小型）](../../media/dts-16.gif "Integration Services 圖示 (小)")**與 Integration Services 保持最**新狀態  <br /> 若要取得 Microsoft 的最新下載、文件、範例和影片以及社群中的精選解決方案，請瀏覽 MSDN 上的 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 頁面：<br /><br /> [瀏覽 MSDN 上的 Integration Services 頁面](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 若要得到這些更新的自動通知，請訂閱該頁面上所提供的 RSS 摘要。  
  
## <a name="see-also"></a>另請參閱  
 [指令碼元件的程式碼撰寫和偵錯](coding-and-debugging-the-script-component.md)  
  
  
