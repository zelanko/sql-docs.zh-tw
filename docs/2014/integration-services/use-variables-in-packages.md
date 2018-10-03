---
title: 在封裝中使用變數 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- user-defined variables [Integration Services]
- variables [Integration Services], use scenarios
- system variables [Integration Services]
ms.assetid: 7742e92d-46c5-4cc4-b9a3-45b688ddb787
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: e309a50dcc47ff4e05335222f9bac6532658ffdd
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48145598"
---
# <a name="use-variables-in-packages"></a>在封裝中使用變數
  變數是 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 封裝之有用的彈性附加項目，可提供在封裝的物件間和父子封裝之間的通訊。 變數還可用於運算式和指令碼。  
  
## <a name="user-defined-variables-and-system-variables"></a>使用者自訂變數和系統變數  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 提供的系統變數，並支援使用者定義的變數。 建立新封裝時，會將容器或工作加入封裝，或建立事件處理常式， [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 包括容器的系統變數集。 系統變數包含關於封裝、容器、工作或事件處理常式的有用資訊。 例如，在執行階段， **MachineName** 系統變數包含在其上執行封裝的電腦名稱和封裝執行開始時間 **StartTime** 。 系統變數是唯讀的。 如需詳細資訊，請參閱 [系統變數](system-variables.md)。  
  
 您可以建立使用者自訂變數，然後將其用於封裝。 在 [!INCLUDE[ssIS](../includes/ssis-md.md)]中可以多種方式使用使用者自訂變數：在指令碼中、在優先順序條件約束、「For 迴圈」容器、「衍生的資料行」轉換和「條件式分割」轉換所使用的運算式中，以及在更新屬性值的屬性運算式中。  
  
 例如，您可以在「For 迴圈」容器的評估條件中，使用使用者自訂變數。 您還可以將「Foreach 迴圈」容器中的列舉值集合值對應至變數，如果「執行 SQL」工作使用參數化 SQL 陳述式，則可將陳述式的參數對應到變數。 如需詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 變數](integration-services-ssis-variables.md)。  
  
## <a name="variables-usage-scenarios"></a>變數使用方式案例  
 變數在 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 封裝中有許多不同的使用方式。 在您將使用者自訂變數新增至封裝，實作方案所需的彈性和可管理性之前，您可能會覺得封裝開發沒有太多的進展。 視案例而定，也常會使用系統變數。  
  
 **屬性運算式** ：使用變數在設定封裝和封裝物件屬性的屬性運算式中提供值。 例如， `SELECT * FROM @varTableName` 運算式會包含更新「執行 SQL」工作所執行之 SQL 陳述式的 `varTableName` 變數。 `DATEPART("d", GETDATE()) == 1? @[User::varPackageFirst]:@[User::varPackageOther]`" 運算式會在該月的第一天執行 `varPackageFirst` 變數中指定的封裝，並在其他日子執行 `varPackageOther` 變數中指定的封裝，來更新「執行封裝」工作所執行的封裝。 如需詳細資訊，請參閱 [在封裝中使用屬性運算式](expressions/use-property-expressions-in-packages.md)。  
  
 **資料流程運算式** ：使用變數在運算式中提供值，「衍生的資料行」和「條件式分割」轉換會使用這些運算式擴展資料行，或將資料列導向不同的轉換輸出。 例如， `@varSalutation + LastName`運算式會串連 `VarSalutation` 變數和 `LastName` 資料行中的值。 `Income < @HighIncome` 運算式會將 `Income` 資料行中、值小於 `HighIncome` 變數中的值的資料列導向輸出。 如需詳細資訊，請參閱[衍生的資料行轉換](data-flow/transformations/derived-column-transformation.md)、[條件式分割轉換](data-flow/transformations/conditional-split-transformation.md) 和 [Integration Services &#40;SSIS&#41; 運算式](expressions/integration-services-ssis-expressions.md)。  
  
 **優先順序條件約束運算式**：提供要在優先順序條件約中使用的值，決定受條件約束的可執行檔是否執行。 這些運算式可以和執行結果 (成功、失敗、完成) 一起使用，或取代執行結果。 例如，如果 `@varMax > @varMin` 運算式評估為 `true`，可執行檔就會執行。 如需詳細資訊，請參閱 [將運算式加入優先順序條件約束](control-flow/precedence-constraints.md)。  
  
 **參數和傳回碼** ：提供值給輸入參數，或儲存輸出參數和傳回碼的值。 您可以將變數對應到參數和傳回值來完成這個動作。 例如，如果您將 `varProductId` 變數設為 23 並執行 `SELECT * from Production.Product WHERE ProductID = ?`SQL 陳述式，查詢就會擷取 `ProductID` 為 23 的產品。 如需詳細資訊，請參閱 [執行 SQL 工作](control-flow/execute-sql-task.md) 和 [執行 SQL 工作中的參數和傳回碼](../../2014/integration-services/parameters-and-return-codes-in-the-execute-sql-task.md)。  
  
 **For 迴圈運算式** ：提供要在「For 迴圈」的初始化、評估和指派運算式中使用的值。 例如，如果 `varCount` 變數為 2 且 `varMaxCount` 為 10，初始化運算式為 `@varCount`，評估運算式為  `@varCount < @varMaxCount`且指派運算式為 `@varCount =@varCount +1`，則迴圈就會重複 8 次。 如需詳細資訊，請參閱 [For 迴圈容器](control-flow/for-loop-container.md)。  
  
 **父封裝變數組態** ：將值從父封裝傳遞到子封裝。 子封裝可以使用父封裝變數組態存取父封裝中的變數。 例如，如果子封裝必須使用和父封裝相同的日期，子封裝就可以定義父封裝變數組態，指定由父封裝中之 GETDATE 函數設定的變數。 如需詳細資訊，請參閱 [執行封裝工作](control-flow/execute-package-task.md) 和 [封裝組態](../../2014/integration-services/package-configurations.md)。  
  
 **指令碼工作和指令碼元件** ：提供唯讀和讀取/寫入變數的清單到「指令碼」工作或「指令碼」元件、更新指令碼中的讀取/寫入變數，然後在指令碼內或指令碼外使用更新的值。 例如，在程式碼 `numberOfCars = CType(Dts.Variables("NumberOfCars").Value, Integer)`中，指令碼變數 `numberOfCars` 會由變數 `NumberOfCars`中的值更新。 如需詳細資訊，請參閱 [在指令碼工作中使用變數](control-flow/script-task.md)。  
  
## <a name="configurations-and-variables"></a>組態和變數  
 若要動態地更新變數，您可以建立變數的組態，使用封裝部署組態，然後在部署封裝時更新組態檔中的變數值。 在執行階段，封裝會使用更新的變數值。 如需詳細資訊，請參閱 [建立封裝組態](../../2014/integration-services/create-package-configurations.md)。  
  
### <a name="to-add-modify-and-delete-user-defined-variables"></a>若要加入、修改和刪除使用者自訂變數  
  
-   [新增、刪除、變更套件中使用者定義變數的範圍](../../2014/integration-services/add-delete-change-scope-of-user-defined-variable-in-a-package.md)  
  
-   [設定使用者定義變數的屬性](../../2014/integration-services/set-the-properties-of-a-user-defined-variable.md)  
  
  
