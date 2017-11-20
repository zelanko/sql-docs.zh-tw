---
title: "在指令碼元件編輯器中設定指令碼元件 |Microsoft 文件"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: extending-packages-scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
dev_langs:
- VB
helpviewer_keywords:
- SSIS Script component
- Script Component Editor
- SSIS Script component, configuring
- Script component [Integration Services], configuring
ms.assetid: 586dd799-f383-4d6d-b1a1-f09233d14f0a
caps.latest.revision: 46
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 8488fcc7d402430f66b9b9018b31956a5a1d8383
ms.contentlocale: zh-tw
ms.lasthandoff: 08/03/2017

---
# <a name="configuring-the-script-component-in-the-script-component-editor"></a>在指令碼元件編輯器中設定指令碼元件
  您在指令碼元件中撰寫自訂程式碼之前，您必須選取您想要建立的資料流程元件的類型 — 來源、 轉換或目的地，然後設定元件的中繼資料和屬性中的**指令碼轉換編輯器**。  
  
## <a name="selecting-the-type-of-component-to-create"></a>選取要建立的元件類型  
 當您將指令碼元件加入至 [資料流程] 窗格的[!INCLUDE[ssIS](../../../includes/ssis-md.md)]設計工具中，**選取指令碼元件類型** 對話方塊隨即出現。 您可以將元件預先設定為來源、轉換或目的地。 做出初步選擇之後，您可以繼續設定中的元件**指令碼轉換編輯器**。  
  
 若要設定指令碼元件的預設指令碼語言，使用**指令碼語言**選項**一般**頁面**選項** 對話方塊。 如需相關資訊，請參閱 [General Page](https://msdn.microsoft.com/library/ms189436(v=sql.110).aspx)。  
  
## <a name="understanding-the-two-design-time-modes"></a>了解兩個設計階段模式  
 在 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 設計師中，指令碼元件有中繼資料設計與程式碼設計兩種模式。  
  
 當您開啟**指令碼轉換編輯器**，元件會進入中繼資料設計模式。 在此模式中，您可以選取輸入資料行，以及加入或設定輸出與輸出資料行，但是無法撰寫程式碼。 在您已設定好元件的中繼資料之後，便可切換到程式碼設計模式以撰寫指令碼。  
  
 當您切換至程式碼設計模式，即可**編輯指令碼**，指令碼元件會鎖定中繼資料，以防止其他變更，並會自動從輸入和輸出的中繼資料產生基底程式碼。 在完成自動產生的程式碼之後，將可以輸入自訂程式碼。 您的程式碼使用自動產生的基底類別以處理輸入資料列、存取緩衝區和緩衝區中的資料行，以及從封裝擷取連接管理員與變數，全部都做為強式類型的物件。  
  
 在程式碼設計模式中輸入自訂程式碼之後，便可切換回中繼資料設計模式。 這並不會刪除您已輸入的任何程式碼，然而，對中繼資料的後續變更會造成重新產生基底類別。 之後，您的元件可能會無法驗證，因為自訂程式碼所參考的物件可能不再存在或是可能已修改過。 在此情況下，您必須手動修正程式碼，才能針對重新產生的基底類別成功地編譯程式碼。  
  
## <a name="configuring-the-component-in-metadata-design-mode"></a>在中繼資料設計模式中設定元件  
 在中繼資料設計模式中，您可以選取輸入資料行，以及加入和設定輸出與輸出資料行，但是無法撰寫程式碼。 在您已設定好元件的中繼資料之後，便可切換到程式碼設計模式以撰寫指令碼。  
  
 您必須在自訂編輯器中設定的屬性，端視指令碼元件的使用而定。 指令碼元件可以設定為來源、轉換或目的地。 視元件的使用方式而定，可支援輸入、輸出或兩者。 您將撰寫的自訂程式碼會負責處理輸入和輸出資料列與資料行。  
  
### <a name="inputs-columns-page-of-the-script-transformation-editor"></a>指令碼轉換編輯器的輸入資料行頁面  
 **的輸入資料行**頁面**指令碼轉換編輯器**會顯示針對轉換和目的地，但不是會為來源。 在本頁，您選取要提供給自訂指令碼使用的輸入資料行，並指定這些資料行的唯讀或讀寫存取權限。  
  
 在將會根據此中繼資料產生的程式碼專案中，BufferWrapper 專案項目包含每個輸入的類別，而且這個類別包含每個選取的輸入資料行之具類型的存取子屬性。 例如，如果您選擇的整數**CustomerID**資料行和一個字串**CustomerName**從名為輸入的資料行**CustomerInput**，BufferWrapper 專案項目會包含**CustomerInput**衍生自類別<xref:Microsoft.SqlServer.Dts.Pipeline.ScriptBuffer>，和**CustomerInput**類別會公開 （expose) 名為整數屬性**CustomerID**和名為字串屬性**CustomerName**。 這個慣例使得撰寫具有類型檢查的程式碼變得可能，如下所示：  
  
```vb  
Dim currentCustomerID as Integer = CustomerInput.CustomerID  
Dim currentCustomerName as String = CustomerInput.CustomerName  
```  
  
 如需如何設定特定類型的資料流程元件的輸入資料行的詳細資訊，請參閱底下的適當範例[開發特定類型的指令碼元件](../../../integration-services/extending-packages-scripting-data-flow-script-component-types/developing-specific-types-of-script-components.md)。  
  
### <a name="inputs-and-outputs-page-of-the-script-transformation-editor"></a>指令碼轉換編輯器的輸入及輸出頁面  
 **輸入和輸出**頁面**指令碼轉換編輯器**顯示為來源、 轉換和目的地。 在本頁，您可以加入、移除和設定要在自訂指令碼中使用的輸入、輸出和輸出資料行，但具有下列限制：  
  
-   當做為來源使用時，指令碼元件沒有輸入並且支援多個輸出。  
  
-   當做為轉換使用時，指令碼元件可支援一個輸入和多個輸出。  
  
-   當做為目的地使用時，指令碼元件支援一個輸入並且沒有輸出。  
  
 在將會根據此中繼資料產生的程式碼專案中，BufferWrapper 專案項目包含每個輸入與輸出的類別。 例如，如果您建立名為輸出**CustomerOutput**，BufferWrapper 專案項目會包含**CustomerOutput**類別衍生自<xref:Microsoft.SqlServer.Dts.Pipeline.ScriptBuffer>，和**CustomerOutput**類別會包含每個輸出資料行建立的具型別的存取子屬性。  
  
 您可以設定輸出資料行上只**輸入和輸出**頁面。 您可以選取轉換和目的地的輸入資料行上**輸入資料行**頁面。 在 BufferWrapper 專案項目中為您建立的具類型之存取子屬性對於輸出資料行而言將是唯寫的。 輸入資料行的存取子屬性將會是唯讀或讀取/寫入根據您選取每個資料行的使用類型**輸入資料行**頁面。  
  
 如需有關設定特定的資料類型的輸入和輸出的資料流程元件查看之下的適當範例[開發特定類型的指令碼元件](../../../integration-services/extending-packages-scripting-data-flow-script-component-types/developing-specific-types-of-script-components.md)。  
  
> [!NOTE]  
>  雖然您無法在指令碼元件中將輸出直接設定為錯誤輸出，以自動處理錯誤資料列，不過可以建立其他輸出與使用指令碼，適時地將資料列導向此輸出，以重新產生錯誤輸出的功能。 如需詳細資訊，請參閱[模擬錯誤輸出指令碼元件](../../../integration-services/extending-packages-scripting-data-flow-script-component-examples/simulating-an-error-output-for-the-script-component.md)。  
  
#### <a name="exclusiongroup-and-synchronousinputid-properties-of-outputs"></a>輸出的 ExclusionGroup 與 SynchronousInputID 屬性  
 **ExclusionGroup**屬性在具有同步輸出，您的程式碼執行篩選或分支的位置，並將共用相同的非零輸出之一的每個資料列導向轉換中才有非零值**ExclusionGroup**值。 例如，轉換可以將資料列導向至預設輸出或是錯誤輸出。 當您建立此案例中的其他輸出時，請確定設定的值**SynchronousInputID**屬性為整數，以符合**識別碼**元件的輸入。  
  
 **SynchronousInputID**屬性在具有同步輸出的轉換中才有非零值。 如果此屬性的值是零，即表示輸出是非同步的。 同步輸出，其中資料列會傳遞給選取的輸出或輸出而不加入任何新資料列，這個屬性應該包含**識別碼**元件的輸入。  
  
> [!NOTE]  
>  當**指令碼轉換編輯器**建立第一個輸出，編輯器設定**SynchronousInputID**要輸出的屬性**識別碼**元件的輸入。 不過，當編輯器建立後續的輸出時，編輯器設定**SynchronousInputID**為零的那些輸出的屬性。  
>   
>  如果您要建立具有同步輸出，每個輸出必須將其**SynchronousInputID**屬性設定為**識別碼**元件的輸入。 因此，每個輸出編輯器建立之後的第一個輸出必須有其**SynchronousInputID**值從零變更**識別碼**元件的輸入。  
>   
>  如果您具有非同步輸出建立元件，每個輸出必須將其**SynchronousInputID**屬性設定為零。 因此，第一個輸出必須有其**SynchronousInputID**值從變更**識別碼**元件的輸入為零。  
  
 如需將兩個同步輸出的其中一個資料列導向指令碼元件中的範例，請參閱[使用指令碼元件建立同步轉換](../../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-synchronous-transformation-with-the-script-component.md)。  
  
### <a name="object-names-in-generated-script"></a>產生的指令碼中的物件名稱  
 指令碼元件會剖析輸入與輸出的名稱，並剖析在輸入與輸出中的資料行名稱，而且會根據這些名稱在 BufferWrapper 專案項目中產生類別和屬性。 如果找到的名稱包含不屬於 Unicode 類別的字元**UppercaseLetter**， **LowercaseLetter**， **TitlecaseLetter**， **ModifierLetter**， **OtherLetter**，或**DecimalDigitLetter**，產生的名稱中卸除無效的字元。 例如，空格會予以捨棄，因此兩個輸入資料行具有名稱**FirstName**和 [**名字**] 會轉譯為具有資料行名稱**FirstName**，預期的結果。 為了避免這個情況，指令碼元件所使用的輸入與輸出的名稱和輸入與輸出資料行的名稱，應該只包含本節中所列的 Unicode 類別裡的字元。  
  
### <a name="script-page-of-the-script-transformation-editor"></a>指令碼轉換編輯器的指令碼頁面  
 在**指令碼**頁面**指令碼工作編輯器**，您指派唯一的名稱和描述指令碼工作。 您也可以指派下列屬性的值。  
  
> [!NOTE]  
>  在 [!INCLUDE[ssISversion10](../../../includes/ssisversion10-md.md)] 和更新的版本中，所有指令碼都是先行編譯。 在舊版中，您指定藉由設定指令碼是否已經先行編譯**Precompile**工作的屬性。  
  
#### <a name="validateexternalmetadata-property"></a>ValidateExternalMetadata 屬性  
 布林值的**ValidateExternalMetadata**屬性指定元件是否應該執行驗證外部資料來源，在設計階段，或是否它延後到執行階段才驗證。 根據預設，這個屬性的值是**True**; 也就是在設計階段和執行階段會進行驗證的外部中繼資料。 您可能想要設定這個屬性的值**False**當外部資料來源不是可在設計階段： 例如，當封裝下載來源或建立目的地只能在執行階段。  
  
#### <a name="readonlyvariables-and-readwritevariables-properties"></a>ReadOnlyVariables 與 ReadWriteVariables 屬性  
 您可以輸入現有變數的逗號分隔清單做為這些屬性的值，使得變數可在指令碼元件程式碼中以唯讀或讀取/寫入的方式來存取。 在程式碼中，變數是透過自動產生的基底類別之 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ReadOnlyVariables%2A> 與 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ReadWriteVariables%2A> 屬性來存取。 如需詳細資訊，請參閱[在指令碼元件中使用變數](../../../integration-services/extending-packages-scripting/data-flow-script-component/using-variables-in-the-script-component.md)。  
  
> [!NOTE]  
>  變數名稱會區分大小寫。  
  
#### <a name="scriptlanguage"></a>ScriptLanguage  
 您可以選擇使用 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic 或 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual C# 做為指令碼元件的程式設計語言。  
  
#### <a name="edit-script-button"></a>編輯指令碼按鈕  
 **編輯指令碼**按鈕會開啟[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] Tools for Applications (VSTA) IDE，您可以在其中撰寫自訂指令碼。 如需詳細資訊，請參閱[編碼和偵錯指令碼元件](../../../integration-services/extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md)。  
  
### <a name="connection-managers-page-of-the-script-transformation-editor"></a>指令碼轉換編輯器的連接管理員頁面  
 在**連接管理員**頁面**指令碼轉換編輯器**，可加入和移除您想要使用自訂指令碼中的連接管理員。 一般而言，您需要在建立來源或是目的地元件時，參考連接管理員。  
  
 在程式碼會產生專案中，會根據此中繼資料， **ComponentWrapper**專案項目包含**連線**具有每個選取的連接管理員的類型存取子屬性的集合類別。 每個具類型的存取子屬性都有做為連接管理員的相同名稱，並且會傳回連接管理員參考做為 <xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.IDTSConnectionManager100> 的執行個體。 比方說，如果您加入連接管理員，名為`MyADONETConnection`上**連接管理員**頁面的 [編輯器] 中，您可以取得連接管理員的參考指令碼中使用下列程式碼：  
  
```vb  
Dim myADONETConnectionManager As IDTSConnectionManager100 = _  
    Me.Connections.MyADONETConnection  
```  
  
 如需詳細資訊，請參閱[連接到指令碼元件中的資料來源](../../../integration-services/extending-packages-scripting/data-flow-script-component/connecting-to-data-sources-in-the-script-component.md)。  
  
## <a name="see-also"></a>另請參閱  
 [編碼和偵錯指令碼元件](../../../integration-services/extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md)  
  
  

