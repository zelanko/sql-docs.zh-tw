---
title: Integration Services (SSIS) 變數 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
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
caps.latest.revision: 59
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: d7352ff51810a16f2c3e81b5362bad764955f67a
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37283614"
---
# <a name="integration-services-ssis-variables"></a>Integration Services (SSIS) 變數
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
  
 所有的變數 (系統變數和使用者自訂變數) 都可在「執行 SQL」工作用來將變數對應至 SQL 陳述式之參數的參數繫結中使用。 如需詳細資訊，請參閱[執行 SQL 工作](control-flow/execute-sql-task.md)和[執行 SQL 工作中的參數和傳回碼](../../2014/integration-services/parameters-and-return-codes-in-the-execute-sql-task.md)。  
  
> [!NOTE]  
>  使用者自訂變數和系統變數的名稱會區分大小寫。  
  
 您可以為下列所有 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 容器類型建立使用者自訂變數：封裝、Foreach 迴圈容器、For 迴圈容器、時序容器、工作和事件處理常式。 使用者自訂變數是容器 Variables 集合的成員。  
  
 如果您使用 [!INCLUDE[ssIS](../includes/ssis-md.md)] 設計師建立封裝，則可以在 [!INCLUDE[ssIS](../includes/ssis-md.md)] 設計師之封裝總管索引標籤上的 [變數] 資料夾中，查看 Variables 集合的成員。 資料夾會列出使用者自訂變數和系統變數。  
  
 您可以利用下列方式設定使用者自訂變數：  
  
-   提供變數的名稱和描述。  
  
-   指定變數的命名空間。  
  
-   指示其值變更時變數是否會引發事件。  
  
-   指示變數是唯讀還是可讀寫。  
  
-   使用運算式的評估結果，以設定變數值。  
  
-   建立封裝或封裝物件 (例如工作) 範圍內的變數。  
  
-   指定變數的值和資料類型。  
  
 系統變數上唯一可設定的選項是指定其變更值時，它們是否會引發事件。  
  
 針對不同的容器類型可使用一組不同的系統變數。 如需封裝及其元素所使用之系統變數的詳細資訊，請參閱[系統變數](system-variables.md)。  
  
 如需變數之實際使用狀況的詳細資訊，請參閱[在封裝中使用變數](../../2014/integration-services/use-variables-in-packages.md)。  
  
## <a name="variable-properties"></a>變數屬性  
 您可以透過在 [變數] 視窗或 [屬性] 視窗中設定下列屬性來設定使用者定義變數。 但某些屬性只能在 [屬性] 視窗中設定。  
  
> [!NOTE]  
>  系統變數上唯一可設定的選項是指定其變更值時，它們是否會引發事件。  
  
 描述  
 指定變數的描述。  
  
 EvaluateAsExpression  
 當屬性設定為`True`，提供的運算式用來設定變數值。  
  
 運算式  
 指定指派給變數的運算式。  
  
 名稱  
 指定變數名稱。  
  
 命名空間  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 提供兩個命名空間：**User** 和 **System**。 依預設，自訂變數屬於 **User** 命名空間，而系統變數則屬於 **System** 命名空間。 您可以為使用者定義變數建立其他命名空間，並變更 **User** 命名空間的名稱，但是您無法變更 **System** 命名空間的名稱，也無法將變數加入 **System** 命名空間或將系統變數指派給其他命名空間。  
  
 RaiseChangedEvent  
 當此屬性設為 `True` 時，`OnVariableValueChanged` 事件會在變數將值變更時產生。  
  
 ReadOnly  
 當此屬性設為 `False`，表示變數可讀取\寫入。  
  
 範圍。  
 > [!NOTE]  
>  您只能透過按一下 [變數] 視窗中的 [移動變數] 來變更此屬性設定。  
  
 變數建立於封裝範圍之內，或封裝中的容器、工作或事件處理常式範圍之內。 因為封裝容器位於容器階層的最上層，所以具有封裝範圍的變數在功能上與全域變數相同，且可以由封裝內的所有容器使用。 同樣地，在容器 (例如「For 迴圈」容器) 範圍中定義的變數可由「For 迴圈」容器內的所有工作或容器使用。  
  
 如果封裝使用「執行封裝」工作來執行其他封裝，則在呼叫封裝或「執行封裝」工作範圍中定義的變數可用於所呼叫的封裝，方法是使用「父封裝變數」組態類型。 如需相關資訊，請參閱 [Package Configurations](../../2014/integration-services/package-configurations.md)。  
  
 IncludeInDebugDump  
 指出偵錯傾印檔案中是否要包含變數值。  
  
 如需使用者定義的變數和系統變數的預設值**InclueInDebugDump**選項是`true`。  
  
 不過，針對使用者自訂變數，系統會重設**IncludeInDebugDump**選項設定為`false`當符合下列條件：  
  
-   如果**EvaluateAsExpression**變數的屬性設定為`true`，系統會重設**IncludeInDebugDump**選項設定為`false`。  
  
     若要偵錯傾印檔案中包含的變數值運算式的文字，設定**IncludeInDebugDump**選項設定為`true`。  
  
-   如果變數資料類型變更為字串時，系統會重設**IncludeInDebugDump**選項設定為`false`。  
  
 系統會重設**IncludeInDebugDump**選項設定為`false`，這可能會覆寫使用者所選取的值。  
  
 值  
 使用者自訂變數值可以是常值或是運算式。 變數包含設定變數值和該值之資料類型的選項。 兩個屬性必須相容：例如，同時使用字串值和整數資料類型是無效的。  
  
 如果變數設定為做為運算式評估，則必須提供運算式。 在執行階段會評估運算式，且會將變數值設定為評估結果。 例如，如果變數使用運算式 `DATEPART("month", GETDATE())` ，則變數的值將為目前日期所在之月份數。 運算式必須是使用 [!INCLUDE[ssIS](../includes/ssis-md.md)] 運算式文法語法的有效運算式。 當運算式搭配變數使用時，運算式可以使用運算式文法提供的常值、運算子和函數，但是運算式無法參考封裝中資料流程的資料行。 運算式的最大長度為 4000 個字元。 如需詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 運算式](expressions/integration-services-ssis-expressions.md)。  
  
 ValueType  
 > [!NOTE]  
>  此屬性值會顯示在 [變數] 視窗中的 [資料類型] 資料行中。  
  
 指定變數值的資料類型。  
  
## <a name="configuring-variables"></a>設定變數  
 您可以透過 [!INCLUDE[ssIS](../includes/ssis-md.md)] 設計師或以程式設計方式設定屬性。  
  
 如需可以在 [[!INCLUDE[ssIS](../includes/ssis-md.md)] 設計師] 中設定之屬性的詳細資訊，請參閱[變數視窗](../../2014/integration-services/variables-window.md)。  
  
 若要深入了解變數屬性，以及有關以程式設計方式設定這些屬性的詳細資訊，請參閱<xref:Microsoft.SqlServer.Dts.Runtime.Variable>。  
  
## <a name="related-tasks"></a>相關工作  
 [新增、刪除、變更套件中使用者定義變數的範圍](../../2014/integration-services/add-delete-change-scope-of-user-defined-variable-in-a-package.md)  
  
 [設定使用者定義變數的屬性](../../2014/integration-services/set-the-properties-of-a-user-defined-variable.md)  
  
 [在子套件中使用變數和參數的值](../../2014/integration-services/use-the-values-of-variables-and-parameters-in-a-child-package.md)  
  
 [在資料流程元件中將查詢參數對應至變數](data-flow/map-query-parameters-to-variables-in-a-data-flow-component.md)  
  
  
