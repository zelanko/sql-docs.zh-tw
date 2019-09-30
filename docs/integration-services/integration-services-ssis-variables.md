---
title: Integration Services (SSIS) 變數 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- variables [Integration Services], passing between packages
- user-defined variables [Integration Services]
- scope [Integration Services]
- system variables [Integration Services]
- variables [Integration Services]
- variables [Integration Services], about variables
- values [Integration Services]
ms.assetid: c1e81ad6-628b-46d4-9b09-d2866517b6ca
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 973e5e1449205d5e72abfa03068db3c8c3e98f87
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/26/2019
ms.locfileid: "71296156"
---
# <a name="integration-services-ssis-variables"></a>Integration Services (SSIS) 變數

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  變數會儲存 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 封裝及其容器、工作和事件處理常式在執行階段可使用的值。 「指令碼」工作和「指令碼」元件中的指令碼也可以使用變數。 將工作和容器排序成工作流程的優先順序條件約束，可在其條件約束定義含有運算式時使用變數。  
  
 您可將 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 封裝中的變數用於下列用途：  
  
-   在執行階段更新封裝元素的屬性。 例如，您可以動態設定「Foreach 迴圈」容器允許的並行可執行檔數目。  
  
-   包含記憶體中的查閱資料表。 例如，封裝可執行用以載入一個具有資料值之變數的「執行 SQL」工作。  
  
-   載入具有資料值的變數，然後將其用於指定 WHERE 子句中的搜尋條件。 例如，「指令碼」工作中的指令碼可以更新 Transact-SQL 陳述式在「執行 SQL」工作中所使用的變數值。  
  
-   載入一個值為整數的變數，然後將該值用於控制封裝控制流程中的迴圈。 例如，您可以使用「For 迴圈」容器之評估運算式中的變數來控制反覆運算。  
  
-   在執行階段擴展 Transact-SQL 陳述式的參數值。 例如，封裝可執行「執行 SQL」工作，然後使用變數動態設定 Transact-SQL 陳述式中的參數。  
  
-   建立包含變數值的運算式。 例如，「衍生的資料行」轉換可使用變數值乘以資料行值而取得的結果來擴展資料行。  
  
## <a name="system-and-user-defined-variables"></a>系統及使用者定義變數  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 支援兩種類型的變數：使用者自訂變數和系統變數。 使用者自訂變數由封裝開發人員定義，而系統變數則由 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]定義。 您可以根據封裝需要建立許多使用者自訂變數，但無法建立其他系統變數。  
  
 所有的變數 (系統變數和使用者定義變數) 都可在「執行 SQL」工作用來將變數對應至 SQL 陳述式之參數的參數繫結中使用。 如需詳細資訊，請參閱 [執行 SQL 工作](../integration-services/control-flow/execute-sql-task.md) 和 [執行 SQL 工作中的參數和傳回碼](https://msdn.microsoft.com/library/a3ca65e8-65cf-4272-9a81-765a706b8663)。  
  
> [!NOTE]  
>  使用者自訂變數和系統變數的名稱會區分大小寫。  
  
 您可以為下列所有 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 容器類型建立使用者自訂變數：封裝、Foreach 迴圈容器、For 迴圈容器、時序容器、工作和事件處理常式。 使用者自訂變數是容器 Variables 集合的成員。  
  
 如果您使用 [!INCLUDE[ssIS](../includes/ssis-md.md)] 設計師建立封裝，則可以在 [!INCLUDE[ssIS](../includes/ssis-md.md)] 設計師之封裝總管  索引標籤上的 [變數]  資料夾中，查看 Variables 集合的成員。 資料夾會列出使用者自訂變數和系統變數。  
  
 您可以利用下列方式設定使用者自訂變數：  
  
-   提供變數的名稱和描述。  
  
-   指定變數的命名空間。  
  
-   指示其值變更時變數是否會引發事件。  
  
-   指示變數是唯讀還是可讀寫。  
  
-   使用運算式的評估結果，以設定變數值。  
  
-   建立封裝或封裝物件 (例如工作) 範圍內的變數。  
  
-   指定變數的值和資料類型。  
  
 系統變數上唯一可設定的選項是指定其變更值時，它們是否會引發事件。  
  
 針對不同的容器類型可使用一組不同的系統變數。 如需封裝及其元素所使用之系統變數的詳細資訊，請參閱 [系統變數](../integration-services/system-variables.md)。  
  
 如需變數之實際使用狀況的詳細資訊，請參閱 [在封裝中使用變數](https://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787)。  
  
## <a name="properties-of-variables"></a>變數屬性  
 您可以透過在 [變數]  視窗或 [屬性]  視窗中設定下列屬性來設定使用者定義變數。 但某些屬性只能在 [屬性] 視窗中設定。  
  
> [!NOTE]  
>  系統變數上唯一可設定的選項是指定其變更值時，它們是否會引發事件。  
  
 **說明**    
 指定變數的描述。  
  
 **EvaluateAsExpression**    
 當屬性設為 **True**時，會使用提供的運算式設定變數值。  
  
 **運算式**    
 指定指派給變數的運算式。  
  
 **名稱**    
 指定變數名稱。  
  
 **命名空間**  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 提供兩個命名空間： **User** 和 **System**。 依預設，自訂變數屬於 **User** 命名空間，而系統變數則屬於 **System** 命名空間。 您可以為使用者定義變數建立其他命名空間，並變更 **User** 命名空間的名稱，但是您無法變更 **System** 命名空間的名稱，也無法將變數加入 **System** 命名空間或將系統變數指派給其他命名空間。  
  
**RaiseChangedEvent**  
 當此屬性設為 [True]  時，**OnVariableValueChanged** 事件會在變數變更值時產生。  
  
 **ReadOnly**  
 當此屬性設為 [False]  ，表示變數可讀取\寫入。  
  
**範圍。**    
 > [!NOTE]  
>  您只能透過按一下 [變數]  視窗中的 [移動變數]  來變更此屬性設定。  
  
 變數建立於封裝範圍之內，或封裝中的容器、工作或事件處理常式範圍之內。 因為封裝容器位於容器階層的最上層，所以具有封裝範圍的變數在功能上與全域變數相同，且可以由封裝內的所有容器使用。 同樣地，在容器 (例如「For 迴圈」容器) 範圍中定義的變數可由「For 迴圈」容器內的所有工作或容器使用。  
  
 如果封裝使用「執行封裝」工作來執行其他封裝，則在呼叫封裝或「執行封裝」工作範圍中定義的變數可用於所呼叫的封裝，方法是使用「父封裝變數」組態類型。 如需相關資訊，請參閱 [Package Configurations](../integration-services/packages/package-configurations.md)。  
  
**IncludeInDebugDump**  
 指出偵錯傾印檔案中是否要包含變數值。  
  
 如果是使用者定義的變數和系統變數， **InclueInDebugDump** 選項的預設值是 **true**。  
  
 但是，如果是使用者定義的變數，系統會在符合以下條件時將 **IncludeInDebugDump** 選項重設為 **false** ：  
  
-   如果 **EvaluateAsExpression** 變數屬性設為 **true**，則系統會將 **IncludeInDebugDump** 選項重設為 **false**。  
  
     若要將運算式的文字當作變數值併入傾印檔案中，請將 **IncludeInDebugDump** 選項設為 **true**。  
  
-   如果變數資料類型變更為字串，系統會將 **IncludeInDebugDump** 選項重設為 **false**。  
  
 當系統將 **IncludeInDebugDump** 選項重設為 **false**時，這可能會覆寫使用者所選取的值。  
  
**Value**    
使用者自訂變數值可以是常值或是運算式。 變數的值不可為 null。 變數的預設值如下：

| 資料類型 | 預設值 |
|---|---|
| 布林 | False |
| 數字和二進位資料類型 | 0 (零) |
| 字元和字串資料類型 | (空字串) |
| Object | System.Object |
| | |

變數具有設定變數值和該值之資料類型的選項。 兩個屬性必須相容：例如，同時使用字串值和整數資料類型是無效的。  
  
 如果變數設定為做為運算式評估，則必須提供運算式。 在執行階段會評估運算式，且會將變數值設定為評估結果。 例如，如果變數使用運算式 `DATEPART("month", GETDATE())` ，則變數的值將為目前日期所在之月份數。 運算式必須是使用 [!INCLUDE[ssIS](../includes/ssis-md.md)] 運算式文法語法的有效運算式。 當運算式搭配變數使用時，運算式可以使用運算式文法提供的常值、運算子和函數，但是運算式無法參考封裝中資料流程的資料行。 運算式的最大長度為 4000 個字元。 如需詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 運算式](../integration-services/expressions/integration-services-ssis-expressions.md)為止。  
  
**ValueType**    
 > [!NOTE]  
>  此屬性值會顯示在 [變數]  視窗中的 [資料類型]  資料行中。  
  
 指定變數值的資料類型。  

## <a name="scenarios-for-using-variables"></a>使用變數的案例  
 變數在 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 封裝中有許多不同的使用方式。 在您將使用者自訂變數新增至封裝，實作方案所需的彈性和可管理性之前，您可能會覺得封裝開發沒有太多的進展。 視案例而定，也常會使用系統變數。  
  
 **屬性運算式** ：使用變數在設定封裝和封裝物件屬性的屬性運算式中提供值。 例如， `SELECT * FROM @varTableName` 運算式會包含更新「執行 SQL」工作所執行之 SQL 陳述式的 `varTableName` 變數。 `DATEPART("d", GETDATE()) == 1? @[User::varPackageFirst]:@[User::varPackageOther]`" 運算式會在該月的第一天執行 `varPackageFirst` 變數中指定的封裝，並在其他日子執行 `varPackageOther` 變數中指定的封裝，來更新「執行封裝」工作所執行的封裝。 如需詳細資訊，請參閱 [在封裝中使用屬性運算式](../integration-services/expressions/use-property-expressions-in-packages.md)。  
  
 **資料流程運算式** ：使用變數在運算式中提供值，「衍生的資料行」和「條件式分割」轉換會使用這些運算式擴展資料行，或將資料列導向不同的轉換輸出。 例如， `@varSalutation + LastName`運算式會串連 `VarSalutation` 變數和 `LastName` 資料行中的值。 `Income < @HighIncome` 運算式會將 `Income` 資料行中、值小於 `HighIncome` 變數中的值的資料列導向輸出。 如需詳細資訊，請參閱[衍生的資料行轉換](../integration-services/data-flow/transformations/derived-column-transformation.md)、[條件式分割轉換](../integration-services/data-flow/transformations/conditional-split-transformation.md) 和 [Integration Services &#40;SSIS&#41; 運算式](../integration-services/expressions/integration-services-ssis-expressions.md)。  
  
 **優先順序條件約束運算式**：提供要在優先順序條件約中使用的值，決定受條件約束的可執行檔是否執行。 這些運算式可以和執行結果 (成功、失敗、完成) 一起使用，或取代執行結果。 例如，如果 `@varMax > @varMin`運算式評估為 **true**，可執行檔就會執行。 如需詳細資訊，請參閱[將運算式加入優先順序條件約束](https://msdn.microsoft.com/library/5574d89a-a68e-4b84-80ea-da93305e5ca1)。  
  
 **參數和傳回碼** ：提供值給輸入參數，或儲存輸出參數和傳回碼的值。 您可以將變數對應到參數和傳回值來完成這個動作。 例如，如果您將 `varProductId` 變數設為 23 並執行 `SELECT * from Production.Product WHERE ProductID = ?`SQL 陳述式，查詢就會擷取 `ProductID` 為 23 的產品。 如需詳細資訊，請參閱 [執行 SQL 工作](../integration-services/control-flow/execute-sql-task.md) 和 [執行 SQL 工作中的參數和傳回碼](https://msdn.microsoft.com/library/a3ca65e8-65cf-4272-9a81-765a706b8663)。  
  
 **For 迴圈運算式** ：提供要在「For 迴圈」的初始化、評估和指派運算式中使用的值。 例如，如果 `varCount` 變數為 2 且 `varMaxCount` 為 10，初始化運算式為 `@varCount`，評估運算式為  `@varCount < @varMaxCount`且指派運算式為 `@varCount =@varCount +1`，則迴圈就會重複 8 次。 如需詳細資訊，請參閱 [For 迴圈容器](../integration-services/control-flow/for-loop-container.md)為止。  
  
 **父封裝變數組態** ：將值從父封裝傳遞到子封裝。 子封裝可以使用父封裝變數組態存取父封裝中的變數。 例如，如果子封裝必須使用和父封裝相同的日期，子封裝就可以定義父封裝變數組態，指定由父封裝中之 GETDATE 函數設定的變數。 如需詳細資訊，請參閱 [執行封裝工作](../integration-services/control-flow/execute-package-task.md) 和 [封裝組態](../integration-services/packages/package-configurations.md)。  
  
 **指令碼工作和指令碼元件** ：提供唯讀和讀取/寫入變數的清單到「指令碼」工作或「指令碼」元件、更新指令碼中的讀取/寫入變數，然後在指令碼內或指令碼外使用更新的值。 例如，在程式碼 `numberOfCars = CType(Dts.Variables("NumberOfCars").Value, Integer)`中，指令碼變數 `numberOfCars` 會由變數 `NumberOfCars`中的值更新。 如需詳細資訊，請參閱 [在指令碼工作中使用變數](../integration-services/extending-packages-scripting/task/using-variables-in-the-script-task.md)。  

## <a name="add-a-variable"></a>加入變數  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，開啟您要使用的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 封裝。  
  
2.  在 [方案總管] 中，按兩下封裝將其開啟。  
  
3.  在 [[!INCLUDE[ssIS](../includes/ssis-md.md)] 設計師] 中，若要定義變數的範圍，請執行下列其中之一：  
  
    -   若要將範圍設為封裝，按一下 [控制流程]  索引標籤之設計介面上的任意位置。  
  
    -   若要將範圍設為事件處理常式，在 [事件處理常式]  索引標籤的設計介面上，選取可執行檔和事件處理常式。  
  
    -   若要將範圍設為工作或容器，在 [控制流程]  索引標籤或 [事件處理常式]  索引標籤的設計介面上，按一下工作或容器。  
  
4.  在 [SSIS]  功能表上，按一下 [變數]  。 您可以將 View.Variables 命令對應到您在 [選項]  對話方塊的 [鍵盤]  頁面中所選擇的組合鍵，以選擇性地顯示 [變數]  視窗。  
  
5.  在 [變數]  視窗中，按一下**加入變數**圖示。 新變數便會加入清單。  
  
6.  選擇性地按一下**方格選項**圖示，在 [變數方格選項]  對話方塊中選取要顯示的其他資料行，然後按一下 [確定]  。  
  
7.  選擇性地設定變數屬性。 如需詳細資訊，請參閱 [設定使用者定義變數的屬性](https://msdn.microsoft.com/library/f98ddbec-f668-4dba-a768-44ac3ae0536f)。  
  
8.  若要儲存已更新的封裝，請在 **[檔案]** 功能表上，按一下 **[儲存選取項目]** 。  

### <a name="add-variable-dialog-box"></a>加入變數對話方塊
使用 [加入變數]  對話方塊，即可指定新變數的屬性。  
  
#### <a name="options"></a>選項。  
 **容器**  
 選取清單中的容器。 容器會定義變數的範圍。 容器可以是封裝或是封裝中的可執行檔。  
  
 **名稱**  
 鍵入變數名稱。  
  
 **Namespace**  
 指定變數的命名空間。 依預設，使用者定義變數是在 **User** 命名空間中。  
  
 **值類型**  
 選取資料類型。  
  
 **ReplTest1**  
 鍵入值。 此值必須與 [值類型]  選項中所指定的資料類型相容。  
  
 **唯讀**  
 選取即可使變數成為唯讀的。  
   
## <a name="delete-a-variable"></a>刪除變數  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，開啟包含所需封裝的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案。  
  
2.  在 [方案總管] 中，以滑鼠右鍵按一下封裝將其開啟。  
  
3.  在 **[SSIS]** 功能表上，按一下 **變數**。 您可以將 View.Variables 命令對應到您在 [選項]  對話方塊的 [鍵盤]  頁面中所選擇的組合鍵，以選擇性地顯示 [變數]  視窗。  
  
4.  選取要刪除的變數，然後按一下 [刪除變數]  。  
  
     若您在 [變數] 視窗中沒看到變數，請按一下 [方格選項]  ，然後選取 [顯示所有範圍的變數]  。  
  
5.  如果 [確認刪除變數]  對話方塊開啟，按一下 [是]  確認。  
  
6.  若要儲存已更新的封裝，請在 **[檔案]** 功能表上，按一下 **[儲存選取項目]** 。  
  
## <a name="change-the-scope-of-a-variable"></a>變更變數的範圍  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，開啟包含所需封裝的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案。  
  
2.  在 [方案總管] 中，以滑鼠右鍵按一下封裝將其開啟。  
  
3.  在 **[SSIS]** 功能表上，按一下 **變數**。 您可以將 View.Variables 命令對應到您在 [選項]  對話方塊的 [鍵盤]  頁面中所選擇的組合鍵，以選擇性地顯示 [變數]  視窗。  
  
4.  選取變數，然後按一下 [移動變數]  。  
  
     若您在 [變數] 視窗中沒看到變數，請按一下 [方格選項]  ，然後選取 [顯示所有範圍的變數]  。  
  
5.  在 [選取新的範圍]  對話方塊中，選取封裝或容器、工作或是封裝中的事件處理常式，以變更變數範圍。  
  
6.  若要儲存已更新的封裝，請在 **[檔案]** 功能表上，按一下 **[儲存選取項目]** 。  

## <a name="set-the-properties-of-a-user-defined-variable"></a>設定使用者定義變數的屬性
 若要在 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]中設定使用者定義變數的屬性，您可以使用下列其中一項功能：  
  
-   [變數] 視窗。  
  
-   [屬性] 視窗。 [屬性]  視窗會列出屬性，以供您設定 [變數]  視窗中無法使用的變數：Description、EvaluateAsExpression、Expression、ReadOnly、ValueType 和 IncludeInDebugDump。  
  
> [!NOTE]  
>  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 也提供一組無法更新屬性的系統變數，但屬性 RaiseChangedEvent 除外。  
  
### <a name="set-expressions-on-variables"></a>設定變數上的運算式  
  
 當您使用 [屬性]  視窗設定使用者定義變數的運算式時：  
  
-   變數的值可以由 Value 或 Expression 屬性設定。 依預設，EvaluateAsExpression 屬性會設為 **False** ，變數的值會由 Value 屬性設定。 若要使用運算式設定該值，您必須先將 EvaluateAsExpression 設為 **True**，然後在 Expression 屬性中提供運算式。 Value 屬性會自動設為運算式的評估結果。  
  
-   ValueType 屬性包含 Value 屬性中之值的資料類型。 運算式設定 Value 之後，ValueType 就會自動更新為與運算式之評估結果相容的資料類型。 例如，如果 Value 包含 0 且 ValueType 屬性包含 **Int32**，然後您將 Expression 設為 GETDATE()，Value 就會包含目前的日期和時間，且 ValueType 會設為 **DateTime**。  
  
-   透過變數的 [屬性]  視窗，可以存取 [運算式產生器]  對話方塊。 您可使用此工具建立、驗證和評估運算式。 如需詳細資訊，請參閱[運算式產生器](../integration-services/expressions/expression-builder.md)和 [Integration Services &#40;SSIS&#41; 運算式](../integration-services/expressions/integration-services-ssis-expressions.md)。  
  
 當您使用 [變數]  視窗設定使用者定義變數的運算式時：  
  
-   若要使用運算式設定變數值，請先確認變數資料類型是否與運算式的評估結果相容，然後才在 [變數]  視窗的 [運算式]  資料行中提供運算式。 [屬性]  視窗中的 EvaluateAsExpression 屬性會自動設為 **True**。  
  
-   當您將運算式指派給變數時，會在變數旁邊顯示特殊圖示標記。 此特殊圖示標記也會顯示在已經設定運算式的連接管理員及工作旁邊。  
  
-   透過變數的 [變數]  視窗，可以存取 [運算式產生器]  對話方塊。 您可使用此工具建立、驗證和評估運算式。 如需詳細資訊，請參閱[運算式產生器](../integration-services/expressions/expression-builder.md)和 [Integration Services &#40;SSIS&#41; 運算式](../integration-services/expressions/integration-services-ssis-expressions.md)。  
  
 如果您在 [變數]  和 [屬性]  視窗中將運算式指派給變數，且 **EvaluateAsExpression** 設為 **True**，就無法變更變數資料類型。  
  
### <a name="set-the-namespace-and-name-properties"></a>設定命名空間和名稱屬性
  
 **Name** 和 **Namespace** 屬性的值必須以 Unicode Standard 2.0 中定義的字母字元或底線 (_) 為開頭。 後續的字元可以是 Unicode Standard 2.0 中定義的字母或數字，或是底線 (\_)。  
  
### <a name="set-variable-properties-in-the-variables-window"></a>在變數視窗中設定變數屬性   
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，開啟包含所需封裝的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案。  
  
2.  在 [方案總管] 中，以滑鼠右鍵按一下封裝將其開啟。  
  
3.  在 **[SSIS]** 功能表上，按一下 **變數**。  
  
     您可以將 View.Variables 命令對應到您在 [選項]  對話方塊的 [鍵盤]  頁面中所選擇的組合鍵，以選擇性地顯示 [變數]  視窗。  
  
4.  選擇性地在 [變數]  視窗中按一下 [方格選項]  ，然後選取要在 [變數]  視窗中顯示的資料行，並選取要套用到此變數清單的篩選。  
  
5.  選擇清單中的變數，然後更新 [名稱]  、[資料類型]  、[值]  、[命名空間]  、[引發變更事件]  、[描述]  及 [運算式]  資料行中的值。  
  
6.  選擇清單中的變數，然後按一下 [移動變數]  以變更範圍。  
  
7.  若要儲存已更新的封裝，請按一下 [檔案]  功能表上的 [儲存選取項目]  。  
  
### <a name="set-variable-properties-in-the-properties-window"></a>在屬性視窗中設定變數屬性  

1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中，開啟包含所需封裝的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 專案。  
  
2.  在 [方案總管] 中，以滑鼠右鍵按一下封裝將其開啟。  
  
3.  在 [檢視]  功能表上，按一下 [屬性視窗]  。  
  
4.  在 [!INCLUDE[ssIS](../includes/ssis-md.md)] 設計師中，按一下 [封裝總管]  索引標籤，並展開 [封裝] 節點。  
  
5.  若要修改具有封裝範圍的變數，請展開 [變數] 節點；否則，展開 [事件處理常式] 或 [可執行檔] 節點，直到找到包含想要修改之變數的 [變數] 節點為止。  
  
6.  按一下想要修改其屬性的變數。  
  
7.  在 [屬性]  視窗中，更新讀取/寫入變數屬性。 有些使用者自訂變數的屬性為讀取/唯讀。  
  
     如需屬性的詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 變數](../integration-services/integration-services-ssis-variables.md)。  
  
8.  若要儲存已更新的封裝，請按一下 [檔案]  功能表上的 [儲存選取項目]  。  

## <a name="update-a-variable-dynamically-with-configurations"></a>使用設定動態更新變數  
 若要動態地更新變數，您可以建立變數的組態，使用封裝部署組態，然後在部署封裝時更新組態檔中的變數值。 在執行階段，封裝會使用更新的變數值。 如需詳細資訊，請參閱 [建立封裝組態](../integration-services/packages/create-package-configurations.md)。  

## <a name="related-tasks"></a>相關工作  
 [在子封裝中使用變數和參數的值](../integration-services/packages/legacy-package-deployment-ssis.md#child)  
  
 [在資料流程元件中將查詢參數對應至變數](../integration-services/data-flow/map-query-parameters-to-variables-in-a-data-flow-component.md)  
