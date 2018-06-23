---
title: 參數和傳回碼在執行 SQL 工作 |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- return codes [Integration Services]
- parameters [Integration Services]
- parameterized SQL statements [Integration Services]
- Execute SQL task [Integration Services]
ms.assetid: a3ca65e8-65cf-4272-9a81-765a706b8663
caps.latest.revision: 28
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 949fefc6beb432eaee882b3a842279a9531f3fbf
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36035734"
---
# <a name="parameters-and-return-codes-in-the-execute-sql-task"></a>執行 SQL 工作中的參數和傳回碼
  SQL 陳述式和預存程序經常使用`input`參數，`output`參數和傳回碼。 在 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 中，執行 SQL 工作支援 `Input`、`Output` 和 `ReturnValue` 等參數類型。 您使用`Input`類型當做輸入參數，`Output`輸出參數和`ReturnValue`的傳回碼。  
  
> [!NOTE]  
>  只有在資料提供者支援參數時，您才能在執行 SQL 工作中使用參數。  
  
 SQL 命令中的參數 (包括查詢和預存程序) 都會對應到在執行 SQL 工作範圍內、父容器內或封裝範圍內建立的使用者自訂變數。 變數值可於設計階段設定，或於執行階段動態擴展。 您也可以將參數對應到系統變數。 如需詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 變數](integration-services-ssis-variables.md)和[系統變數](system-variables.md)。  
  
 不過，在執行 SQL 工作中使用參數和傳回碼比只是知道工作支援的參數類型，以及如何對應這些參數還要複雜。 若要在執行 SQL 工作中成功使用參數和傳回碼，需要有其他使用需求與指導方針。 本主題的其餘部分包含這些使用需求和指導方針：  
  
-   [使用參數名稱和標記](#Parameter_names_and_markers)  
  
-   [搭配日期和時間資料類型使用參數](#Date_and_time_data_types)  
  
-   [在 WHERE 子句中使用參數](#WHERE_clauses)  
  
-   [搭配預存程序使用參數](#Stored_procedures)  
  
-   [取得傳回碼的值](#Return_codes)  
  
-   [設定參數和傳回碼在執行 SQL 工作編輯器](#Configure_parameters_and_return_codes)  
  
##  <a name="Parameter_names_and_markers"></a> 使用參數名稱和標記  
 依據執行 SQL 工作使用的連接類型，SQL 命令的語法會使用不同的參數標記。 例如，[!INCLUDE[vstecado](../includes/vstecado-md.md)] 連線管理員類型要求 SQL 命令必須使用格式為 **@varParameter** 的參數標記，而 OLE DB 連線類型則需要使用問號 (?)。  
  
 在變數與參數的對應中，可以用來當做參數名稱的名稱也會隨著連線管理員的類型而異。 例如，[!INCLUDE[vstecado](../includes/vstecado-md.md)] 連線管理員類型使用具有 @ 前置詞的使用者自訂名稱，而 OLE DB 連線管理員類型則要求您必須使用以 0 為基底的序數數值做為參數名稱。  
  
 下表摘要說明執行 SQL 工作可以使用之連線管理員類型的 SQL 命令需求。  
  
|連接類型|參數標記|參數名稱|範例 SQL 命令|  
|---------------------|----------------------|--------------------|-------------------------|  
|ADO|?|Param1, Param2, …|SELECT FirstName, LastName, Title FROM Person.Contact WHERE ContactID = ?|  
|[!INCLUDE[vstecado](../includes/vstecado-md.md)]|@\<參數名稱>|@\<參數名稱>|SELECT FirstName, LastName, Title FROM Person.Contact WHERE ContactID = @parmContactID|  
|ODBC|?|1, 2, 3, …|SELECT FirstName, LastName, Title FROM Person.Contact WHERE ContactID = ?|  
|EXCEL 和 OLE DB|?|0, 1, 2, 3, …|SELECT FirstName, LastName, Title FROM Person.Contact WHERE ContactID = ?|  
  
### <a name="using-parameters-with-adonet-and-ado-connection-managers"></a>搭配 ADO.NET 和 ADO 連接管理員使用參數  
 [!INCLUDE[vstecado](../includes/vstecado-md.md)] 和 ADO 連線管理員對於使用參數的 SQL 命令，擁有特定的需求：  
  
-   [!INCLUDE[vstecado](../includes/vstecado-md.md)] 連線管理員要求 SQL 命令必須使用參數名稱作為參數標記。 這表示變數可以直接對應到參數。 例如， `@varName` 變數會對應到名為 `@parName` 的參數，並提供值給 `@parName`參數。  
  
-   ADO 連接管理員要求 SQL 命令必須使用問號 (?) 做為參數標記。 不過，您可以使用整數值之外的任何使用者自訂名稱做為參數名稱。  
  
 若要提供值給參數，變數會對應到參數名稱。 接著，執行 SQL 工作會在參數清單中使用參數名稱的序數值，將值從變數載入參數中。  
  
### <a name="using-parameters-with-excel-odbc-and-ole-db-connection-managers"></a>搭配 EXCEL、ODBC 和 OLE DB 連接管理員使用參數  
 EXCEL、ODBC 和 OLE DB 連接管理員要求 SQL 命令必須使用問號 (?) 做為參數標記，並以 0 或 1 為基底的數值作為參數名稱。 如果執行 SQL 工作使用 ODBC 連接管理員，對應到查詢中第一個參數的參數名稱會被命名為 1，否則，該參數會被命名為 0。 對於後續的參數，參數名稱的數值表示 SQL 命令中，參數名稱所對應的參數。 例如，參數名稱 3 對應至第 3 個參數，這個參數在 SQL 命令中是由第 3 個問號 (?) 來代表。  
  
 為了將值提供給參數，變數會對應到參數名稱，而執行 SQL 工作則會使用參數名稱的序數值，將值從變數載入參數中。  
  
 依據連接管理員使用的提供者而定，部分 OLE DB 資料類型可能不受支援。 例如，Excel 驅動程式只能辨識有限的一組資料類型。 如需具有 Excel 驅動程式之 Jet 提供者行為的詳細資訊，請參閱 [Excel 來源](data-flow/excel-source.md)。  
  
#### <a name="using-parameters-with-ole-db-connection-managers"></a>搭配 OLE DB 連接管理員使用參數  
 「執行 SQL」工作使用 OLE DB 連線管理員時，即可使用工作的 BypassPrepare 屬性。 您應該將此屬性設定為`true`如果執行 SQL 工作搭配參數使用 SQL 陳述式。  
  
 您在使用 OLE DB 連接管理員時無法使用參數化的子查詢，因為執行 SQL 工作無法透過 OLE DB 提供者衍生參數資訊。 不過，您可以使用運算式，將參數值串連到查詢字串，並設定工作的 SqlStatementSource 屬性。  
  
##  <a name="Date_and_time_data_types"></a> 搭配日期和時間資料類型使用參數  
  
### <a name="using-date-and-time-parameters-with-adonet-and-ado-connection-managers"></a>搭配 ADO.NET 和 ADO 連接管理員使用日期和時間參數  
 當讀取資料的[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]型別，`time`和`datetimeoffset`，使用 「 執行 SQL 」 工作[!INCLUDE[vstecado](../includes/vstecado-md.md)]或 ADO 連接管理員具有下列額外需求：  
  
-   如`time`資料，[!INCLUDE[vstecado](../includes/vstecado-md.md)]連接管理員要求此資料儲存在參數的參數型別`Input`或`Output`，且資料類型為`string`。  
  
-   如`datetimeoffset`資料，[!INCLUDE[vstecado](../includes/vstecado-md.md)]連接管理員要求此資料儲存在下列參數的其中一個：  
  
    -   參數類型為 `Input`，且資料類型為 `string` 的參數。  
  
    -   參數的參數型別`Output`或`ReturnValue`，且資料類型為`datetimeoffset`， `string`，或`datetime2`。 如果您選取的參數，其資料類型為`string`或`datetime2`，[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]將資料轉換成字串或 datetime2。  
  
-   ADO 連接管理員要求 `time` 或 `datetimeoffset` 資料必須以參數類型為 `Input` 或 `Output`，且資料類型為 `adVarWchar` 的參數儲存。  
  
 如需 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 資料類型以及如何將其對應到 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 資料類型的詳細資訊，請參閱[資料類型 &#40;Transact-SQL&#41;](/sql/t-sql/data-types/data-types-transact-sql) 和 [Integration Services 資料類型](data-flow/integration-services-data-types.md)。  
  
### <a name="using-date-and-time-parameters-with-ole-db-connection-managers"></a>搭配 OLE DB 連接管理員使用日期和時間參數  
 「 執行 SQL 」 工作使用 OLE DB 連接管理員時，具有特定的儲存需求的資料，[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]資料型別， `date`， `time`， `datetime`， `datetime2`，和`datetimeoffset`。 您必須以下列其中一種參數類型儲存此資料：  
  
-   NVARCHAR 資料類型的輸入參數。  
  
-   具有適當資料類型的輸出參數，如下表所列示。  
  
    |`Output` 參數類型|日期資料類型|  
    |-------------------------------|--------------------|  
    |DBDATE|`date`|  
    |DBTIME2|`time`|  
    |DBTIMESTAMP|`datetime`, `datetime2`|  
    |DBTIMESTAMPOFFSET|`datetimeoffset`|  
  
 如果資料沒有以適當的輸入或輸出參數儲存，則封裝會失敗。  
  
### <a name="using-date-and-time-parameters-with-odbc-connection-managers"></a>搭配 ODBC 連接管理員使用日期和時間參數  
 「 執行 SQL 」 工作使用 ODBC 連接管理員時，具有特定的儲存需求使用其中一個資料[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]資料型別， `date`， `time`， `datetime`， `datetime2`，或`datetimeoffset`。 您必須以下列其中一種參數類型儲存此資料：  
  
-   SQL_WVARCHAR 資料類型的 `input` 參數。  
  
-   `output`與適當的資料類型，如下表中所列的參數。  
  
    |`Output` 參數類型|日期資料類型|  
    |-------------------------------|--------------------|  
    |SQL_DATE|`date`|  
    |SQL_SS_TIME2|`time`|  
    |SQL_TYPE_TIMESTAMP<br /><br /> -或-<br /><br /> SQL_TIMESTAMP|`datetime`, `datetime2`|  
    |SQL_SS_TIMESTAMPOFFSET|`datetimeoffset`|  
  
 如果資料沒有以適當的輸入或輸出參數儲存，則封裝會失敗。  
  
##  <a name="WHERE_clauses"></a> 使用參數在 WHERE 子句  
 SELECT、INSERT、UPDATE 和 DELETE 命令經常包含 WHERE 子句，以指定篩選條件，用以定義來源資料表中每個資料列必須符合才能做為 SQL 命令的條件。 參數會在 WHERE 子句中提供篩選值。  
  
 您可以使用參數標記，動態提供參數值。 SQL 陳述式中可以使用的參數標記和參數名稱的規則，需視「執行 SQL」所使用的連接管理員類型而定。  
  
 下表依照連接管理員類型列出 SELECT 命令的範例。 INSERT、UPDATE 和 DELETE 陳述式與這些範例類似。 這些範例使用 SELECT，從 [!INCLUDE[ssSampleDBUserInputNonLocal](../includes/sssampledbuserinputnonlocal-md.md)] 的 **Product** 資料表傳回 **ProductID** 大於及小於兩個參數所指定之值的產品。  
  
|連接類型|SELECT 語法|  
|---------------------|-------------------|  
|EXCEL、ODBC 和 OLEDB|`SELECT* FROM Production.Product WHERE ProductId > ? AND ProductID < ?`|  
|ADO|`SELECT* FROM Production.Product WHERE ProductId > ? AND ProductID < ?`|  
|[!INCLUDE[vstecado](../includes/vstecado-md.md)]|`SELECT* FROM Production.Product WHERE ProductId > @parmMinProductID AND ProductID < @parmMaxProductID`|  
  
 這些範例必須使用具有下列名稱的參數：  
  
-   EXCEL 和 OLED DB 連接管理員使用參數名稱 0 和 1。 ODBC 連接類型則使用 1 和 2。  
  
-   ADO 連接類型可以使用任何兩個參數名稱，例如 Param1 和 Param2，但這些名稱必須對應它們在參數清單中的序數位置。  
  
-   [!INCLUDE[vstecado](../includes/vstecado-md.md)] 連線類型使用參數名稱 @parmMinProductID 和 @parmMaxProductID。  
  
##  <a name="Stored_procedures"></a> 搭配預存程序使用參數  
 執行預存程序的 SQL 命令亦可使用參數對應。 如何使用參數標記和參數名稱的規則，需視「執行 SQL」所使用的連接管理員類型而定，這一點與參數化查詢的規則相同。  
  
 下表依照連接管理員類型列出 EXEC 命令的範例。 這些範例會執行 [!INCLUDE[ssSampleDBUserInputNonLocal](../includes/sssampledbuserinputnonlocal-md.md)] 中的 **uspGetBillOfMaterials** 預存程序。 預存程序會使用`@StartProductID`和`@CheckDate``input`參數。  
  
|連接類型|EXEC 語法|  
|---------------------|-----------------|  
|EXCEL 和 OLEDB|`EXEC uspGetBillOfMaterials ?, ?`|  
|ODBC|`{call uspGetBillOfMaterials(?, ?)}`<br /><br /> 如需 ODBC CALL 語法的詳細資訊，請參閱 MSDN Library 之《ODBC 程式設計人員參考》中的主題 [程序參數](http://go.microsoft.com/fwlink/?LinkId=89462)。|  
|ADO|如果設為 IsQueryStoredProcedure `False`， `EXEC uspGetBillOfMaterials ?, ?`<br /><br /> 如果設為 IsQueryStoredProcedure `True`， `uspGetBillOfMaterials`|  
|[!INCLUDE[vstecado](../includes/vstecado-md.md)]|如果設為 IsQueryStoredProcedure `False`， `EXEC uspGetBillOfMaterials @StartProductID, @CheckDate`<br /><br /> 如果設為 IsQueryStoredProcedure `True`， `uspGetBillOfMaterials`|  
  
 若要使用輸出參數，此語法要求您必須在每個參數標記後面加上 OUTPUT 關鍵字。 例如，下列輸出參數語法是正確的：`EXEC myStoredProcedure ? OUTPUT`。  
  
 如需搭配 Transact-SQL 預存程序使用輸入和輸出參數的詳細資訊，請參閱 [EXECUTE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/execute-transact-sql)。  
  
##  <a name="Return_codes"></a> 取得傳回碼的值  
 預存程序可以傳回稱為傳回碼的整數值，以指出程序的執行狀態。 若要執行 SQL 工作中實作傳回碼，您可以使用參數`ReturnValue`型別。  
  
 下表依據連接類型列出實作傳回碼的部分 EXEC 命令範例。 所有的範例都使用 `input` 參數。 如何使用參數標記和參數名稱的規則也適用於所有參數類型 —`Input`， `Output`，和`ReturnValue`。  
  
 部分語法不支援參數常值。 在這種情況下，您必須使用變數來提供參數值。  
  
|連接類型|EXEC 語法|  
|---------------------|-----------------|  
|EXCEL 和 OLEDB|`EXEC ? = myStoredProcedure 1`|  
|ODBC|`{? = call myStoredProcedure(1)}`<br /><br /> 如需 ODBC CALL 語法的詳細資訊，請參閱 MSDN Library 之《ODBC 程式設計人員參考》中的主題 [程序參數](http://go.microsoft.com/fwlink/?LinkId=89462)。|  
|ADO|如果設為 IsQueryStoreProcedure `False`， `EXEC ? = myStoredProcedure 1`<br /><br /> 如果設為 IsQueryStoreProcedure `True`， `myStoredProcedure`|  
|[!INCLUDE[vstecado](../includes/vstecado-md.md)]|設定 IsQueryStoreProcedure 設`True`。<br /><br /> `myStoredProcedure`|  
  
 在上表顯示的語法中，「執行 SQL」工作使用 [直接輸入] 來源類型執行預存程序。 「執行 SQL」工作也可以使用 [檔案連接] 來源類型執行預存程序。 不論 「 執行 SQL 」 工作使用**直接輸入**或**檔案連接**來源類型，請使用參數的`ReturnValue`實作傳回碼的型別。 如需如何設定「執行 SQL」工作所執行之 SQL 陳述式來源類型的詳細資訊，請參閱[執行 SQL 工作編輯器 &#40;一般頁面&#41;](general-page-of-integration-services-designers-options.md)。  
  
 如需搭配 Transact-SQL 預存程序使用傳回碼的詳細資訊，請參閱 [RETURN &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/return-transact-sql)。  
  
##  <a name="Configure_parameters_and_return_codes"></a> 設定參數和傳回碼，在執行 SQL 工作  
 如需可以在 [[!INCLUDE[ssIS](../includes/ssis-md.md)] 設計師] 中設定之參數和傳回碼屬性的詳細資訊，請按一下下列主題：  
  
-   [執行 SQL 工作編輯器&#40;參數對應頁面&#41;](../../2014/integration-services/execute-sql-task-editor-parameter-mapping-page.md)  
  
 如需有關如何在「 [!INCLUDE[ssIS](../includes/ssis-md.md)] 設計師」中設定這些屬性的詳細資訊，請按下列主題：  
  
-   [設定工作或容器的屬性](../../2014/integration-services/set-the-properties-of-a-task-or-container.md)  
  
## <a name="related-tasks"></a>相關工作  
 [設定工作或容器的屬性](../../2014/integration-services/set-the-properties-of-a-task-or-container.md)  
  
## <a name="related-content"></a>相關內容  
  
-   位於 blogs.msdn.com 的部落格項目： [Stored procedures with output parameters](http://go.microsoft.com/fwlink/?LinkId=157786)(使用輸出參數的預存程序)  
  
-   位於 msftisprodsamples.codeplex.com 的 CodePlex 範例： [執行 SQL 參數和結果集](http://go.microsoft.com/fwlink/?LinkId=157863)  
  
## <a name="see-also"></a>另請參閱  
 [執行 SQL 工作](control-flow/execute-sql-task.md)   
 [中的結果集執行 SQL 工作](../../2014/integration-services/result-sets-in-the-execute-sql-task.md)  
  
  
