---
title: 執行 SQL 工作中的參數和傳回碼 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- return codes [Integration Services]
- parameters [Integration Services]
- parameterized SQL statements [Integration Services]
- Execute SQL task [Integration Services]
ms.assetid: a3ca65e8-65cf-4272-9a81-765a706b8663
author: chugugrace
ms.author: chugu
ms.openlocfilehash: cdc32e103642e086e81f6499bf56e5fbb71c3bd1
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/26/2020
ms.locfileid: "85423555"
---
# <a name="parameters-and-return-codes-in-the-execute-sql-task"></a>執行 SQL 工作中的參數和傳回碼
  SQL 陳述式和預存程序經常使用 `input` 參數、`output` 參數以及傳回碼。 在 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 中，執行 SQL 工作支援 `Input`、`Output` 和 `ReturnValue` 等參數類型。 您可以使用 `Input` 類型當做輸入參數，使用 `Output` 當做輸出參數，並使用 `ReturnValue` 當做傳回碼。  
  
> [!NOTE]  
>  只有在資料提供者支援參數時，您才能在執行 SQL 工作中使用參數。  
  
 SQL 命令中的參數 (包括查詢和預存程序) 都會對應到在執行 SQL 工作範圍內、父容器內或封裝範圍內建立的使用者自訂變數。 變數值可於設計階段設定，或於執行階段動態擴展。 您也可以將參數對應到系統變數。 如需詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 變數](integration-services-ssis-variables.md)和[系統變數](system-variables.md)。  
  
 不過，在執行 SQL 工作中使用參數和傳回碼比只是知道工作支援的參數類型，以及如何對應這些參數還要複雜。 若要在執行 SQL 工作中成功使用參數和傳回碼，需要有其他使用需求與指導方針。 本主題的其餘部分包含這些使用需求和指導方針：  
  
-   [使用參數名稱和標記](#Parameter_names_and_markers)  
  
-   [搭配日期和時間資料類型使用參數](#Date_and_time_data_types)  
  
-   [在 WHERE 子句中使用參數](#WHERE_clauses)  
  
-   [搭配預存程序使用參數](#Stored_procedures)  
  
-   [取得傳回碼的值](#Return_codes)  
  
-   [在執行 SQL 工作編輯器中設定參數和傳回碼](#Configure_parameters_and_return_codes)  
  
##  <a name="using-parameter-names-and-markers"></a><a name="Parameter_names_and_markers"></a>使用參數名稱和標記  
 依據執行 SQL 工作使用的連接類型，SQL 命令的語法會使用不同的參數標記。 例如， [!INCLUDE[vstecado](../includes/vstecado-md.md)] 連線管理員類型要求 SQL 命令使用格式為** \@ varParameter**的參數標記，而 OLE DB 連線類型需要問號（？）參數標記。  
  
 在變數與參數的對應中，可以用來當做參數名稱的名稱也會隨著連線管理員的類型而異。 例如，[!INCLUDE[vstecado](../includes/vstecado-md.md)] 連線管理員類型使用具有 \@ 前置詞的使用者定義名稱，而 OLE DB 連線管理員類型則要求您使用以 0 為基底的序數數值作為參數名稱。  
  
 下表摘要說明執行 SQL 工作可以使用之連線管理員類型的 SQL 命令需求。  
  
|連線類型|參數標記|參數名稱|範例 SQL 命令|  
|---------------------|----------------------|--------------------|-------------------------|  
|ADO|?|Param1, Param2, ...|SELECT FirstName, LastName, Title FROM Person.Contact WHERE ContactID = ?|  
|[!INCLUDE[vstecado](../includes/vstecado-md.md)]|\@\<parameter name>|\@\<parameter name>|SELECT FirstName, LastName, Title FROM Person.Contact WHERE ContactID = \@parmContactID|  
|ODBC|?|1, 2, 3, ...|SELECT FirstName, LastName, Title FROM Person.Contact WHERE ContactID = ?|  
|EXCEL 和 OLE DB|?|0, 1, 2, 3, ...|SELECT FirstName, LastName, Title FROM Person.Contact WHERE ContactID = ?|  
  
### <a name="using-parameters-with-adonet-and-ado-connection-managers"></a>搭配 ADO.NET 和 ADO 連線管理員使用參數  
 [!INCLUDE[vstecado](../includes/vstecado-md.md)] 和 ADO 連線管理員對於使用參數的 SQL 命令，擁有特定的需求：  
  
-   [!INCLUDE[vstecado](../includes/vstecado-md.md)] 連線管理員要求 SQL 命令必須使用參數名稱作為參數標記。 這表示變數可以直接對應到參數。 例如， `@varName` 變數會對應到名為 `@parName` 的參數，並提供值給 `@parName`參數。  
  
-   ADO 連接管理員要求 SQL 命令必須使用問號 (?) 做為參數標記。 不過，您可以使用整數值之外的任何使用者自訂名稱做為參數名稱。  
  
 若要提供值給參數，變數會對應到參數名稱。 接著，執行 SQL 工作會在參數清單中使用參數名稱的序數值，將值從變數載入參數中。  
  
### <a name="using-parameters-with-excel-odbc-and-ole-db-connection-managers"></a>搭配 EXCEL、ODBC 和 OLE DB 連接管理員使用參數  
 EXCEL、ODBC 和 OLE DB 連接管理員要求 SQL 命令必須使用問號 (?) 做為參數標記，並以 0 或 1 為基底的數值作為參數名稱。 如果執行 SQL 工作使用 ODBC 連接管理員，對應到查詢中第一個參數的參數名稱會被命名為 1，否則，該參數會被命名為 0。 對於後續的參數，參數名稱的數值表示 SQL 命令中，參數名稱所對應的參數。 例如，參數名稱 3 對應至第 3 個參數，這個參數在 SQL 命令中是由第 3 個問號 (?) 來代表。  
  
 為了將值提供給參數，變數會對應到參數名稱，而執行 SQL 工作則會使用參數名稱的序數值，將值從變數載入參數中。  
  
 依據連接管理員使用的提供者而定，部分 OLE DB 資料類型可能不受支援。 例如，Excel 驅動程式只能辨識有限的一組資料類型。 如需具有 Excel 驅動程式之 Jet 提供者行為的詳細資訊，請參閱 [Excel 來源](data-flow/excel-source.md)。  
  
#### <a name="using-parameters-with-ole-db-connection-managers"></a>搭配 OLE DB 連接管理員使用參數  
 「執行 SQL」工作使用 OLE DB 連線管理員時，即可使用工作的 BypassPrepare 屬性。 如果執行 SQL 工作搭配參數使用 SQL 陳述式，您應該將這個屬性設為 `true`。  
  
 您在使用 OLE DB 連接管理員時無法使用參數化的子查詢，因為執行 SQL 工作無法透過 OLE DB 提供者衍生參數資訊。 不過，您可以使用運算式，將參數值串連到查詢字串，並設定工作的 SqlStatementSource 屬性。  
  
##  <a name="using-parameters-with-date-and-time-data-types"></a><a name="Date_and_time_data_types"></a>搭配日期和時間資料類型使用參數  
  
### <a name="using-date-and-time-parameters-with-adonet-and-ado-connection-managers"></a>搭配 ADO.NET 和 ADO 連接管理員使用日期和時間參數  
 讀取 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 類型、`time` 和 `datetimeoffset` 的資料時，使用 [!INCLUDE[vstecado](../includes/vstecado-md.md)] 或 ADO 連接管理員的執行 SQL 工作具有下列額外需求：  
  
-   若是 `time` 資料， [!INCLUDE[vstecado](../includes/vstecado-md.md)] 連接管理員要求此資料必須儲存在參數類型為 `Input` 或 `Output` ，且其資料類型為的參數中 `string` 。  
  
-   若是 `datetimeoffset` 資料，[!INCLUDE[vstecado](../includes/vstecado-md.md)] 連接管理員要求此資料必須以下列其中一個參數儲存：  
  
    -   參數類型為 `Input`，且資料類型為 `string` 的參數。  
  
    -   參數類型為 `Output` 或 `ReturnValue`，且資料類型為 `datetimeoffset`、`string` 或 `datetime2` 的參數。 如果您選取資料類型為 `string` 或 `datetime2` 的參數，[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 會將資料轉換為字串或 datetime2。  
  
-   ADO 連接管理員要求 `time` 或 `datetimeoffset` 資料必須以參數類型為 `Input` 或 `Output`，且資料類型為 `adVarWchar` 的參數儲存。  
  
 如需 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 資料類型以及如何將其對應到 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 資料類型的詳細資訊，請參閱[資料類型 &#40;Transact-SQL&#41;](/sql/t-sql/data-types/data-types-transact-sql) 和 [Integration Services 資料類型](data-flow/integration-services-data-types.md)。  
  
### <a name="using-date-and-time-parameters-with-ole-db-connection-managers"></a>搭配 OLE DB 連接管理員使用日期和時間參數  
 使用 OLE DB 連接管理員時，執行 SQL 工作對於 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 資料類型、`date`、`time`、`datetime`、`datetime2` 和 `datetimeoffset` 的資料具有特定的儲存需求。 您必須以下列其中一種參數類型儲存此資料：  
  
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
 使用 ODBC 連接管理員時，執行 SQL 工作對於具有其中一種 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 資料類型、`date`、`time`、`datetime`、`datetime2` 和 `datetimeoffset` 的資料具有特定的儲存需求。 您必須以下列其中一種參數類型儲存此資料：  
  
-   SQL_WVARCHAR 資料類型的 `input` 參數。  
  
-   具有適當資料類型的 `output` 參數，如下表所列示。  
  
    |`Output` 參數類型|日期資料類型|  
    |-------------------------------|--------------------|  
    |SQL_DATE|`date`|  
    |SQL_SS_TIME2|`time`|  
    |SQL_TYPE_TIMESTAMP<br /><br /> -或-<br /><br /> SQL_TIMESTAMP|`datetime`, `datetime2`|  
    |SQL_SS_TIMESTAMPOFFSET|`datetimeoffset`|  
  
 如果資料沒有以適當的輸入或輸出參數儲存，則封裝會失敗。  
  
##  <a name="using-parameters-in-where-clauses"></a><a name="WHERE_clauses"></a>在 WHERE 子句中使用參數  
 SELECT、INSERT、UPDATE 和 DELETE 命令經常包含 WHERE 子句，以指定篩選條件，用以定義來源資料表中每個資料列必須符合才能做為 SQL 命令的條件。 參數會在 WHERE 子句中提供篩選值。  
  
 您可以使用參數標記，動態提供參數值。 SQL 陳述式中可以使用的參數標記和參數名稱的規則，需視「執行 SQL」所使用的連接管理員類型而定。  
  
 下表依照連接管理員類型列出 SELECT 命令的範例。 INSERT、UPDATE 和 DELETE 陳述式與這些範例類似。 這些範例使用 SELECT，從 **中的** Product [!INCLUDE[ssSampleDBUserInputNonLocal](../includes/sssampledbuserinputnonlocal-md.md)] 資料表傳回 **ProductID** 大於及小於兩個參數所指定之值的產品。  
  
|連線類型|SELECT 語法|  
|---------------------|-------------------|  
|EXCEL、ODBC 和 OLEDB|`SELECT* FROM Production.Product WHERE ProductId > ? AND ProductID < ?`|  
|ADO|`SELECT* FROM Production.Product WHERE ProductId > ? AND ProductID < ?`|  
|[!INCLUDE[vstecado](../includes/vstecado-md.md)]|`SELECT* FROM Production.Product WHERE ProductId > @parmMinProductID AND ProductID < @parmMaxProductID`|  
  
 這些範例必須使用具有下列名稱的參數：  
  
-   EXCEL 和 OLED DB 連接管理員使用參數名稱 0 和 1。 ODBC 連接類型則使用 1 和 2。  
  
-   ADO 連接類型可以使用任何兩個參數名稱，例如 Param1 和 Param2，但這些名稱必須對應它們在參數清單中的序數位置。  
  
-   [!INCLUDE[vstecado](../includes/vstecado-md.md)] 連接類型使用參數名稱 \@parmMinProductID 和 \@parmMaxProductID。  
  
##  <a name="using-parameters-with-stored-procedures"></a><a name="Stored_procedures"></a>搭配預存程式使用參數  
 執行預存程序的 SQL 命令亦可使用參數對應。 如何使用參數標記和參數名稱的規則，需視「執行 SQL」所使用的連接管理員類型而定，這一點與參數化查詢的規則相同。  
  
 下表依照連接管理員類型列出 EXEC 命令的範例。 這些範例會執行 **中的** uspGetBillOfMaterials [!INCLUDE[ssSampleDBUserInputNonLocal](../includes/sssampledbuserinputnonlocal-md.md)]預存程序。 預存程式會使用 `@StartProductID` 和 `@CheckDate` `input` 參數。  
  
|連線類型|EXEC 語法|  
|---------------------|-----------------|  
|EXCEL 和 OLEDB|`EXEC uspGetBillOfMaterials ?, ?`|  
|ODBC|`{call uspGetBillOfMaterials(?, ?)}`<br /><br /> 如需 ODBC CALL 語法的詳細資訊，請參閱 MSDN Library 之《ODBC 程式設計人員參考》中的主題 [程序參數](https://go.microsoft.com/fwlink/?LinkId=89462)。|  
|ADO|如果 Isquerystoredprocedure 設設定為 `False` ，`EXEC uspGetBillOfMaterials ?, ?`<br /><br /> 如果 Isquerystoredprocedure 設設定為 `True` ，`uspGetBillOfMaterials`|  
|[!INCLUDE[vstecado](../includes/vstecado-md.md)]|如果 Isquerystoredprocedure 設設定為 `False` ，`EXEC uspGetBillOfMaterials @StartProductID, @CheckDate`<br /><br /> 如果 Isquerystoredprocedure 設設定為 `True` ，`uspGetBillOfMaterials`|  
  
 若要使用輸出參數，此語法要求您必須在每個參數標記後面加上 OUTPUT 關鍵字。 例如，下列輸出參數語法是正確的： `EXEC myStoredProcedure ? OUTPUT`。  
  
 如需搭配 Transact-SQL 預存程序使用輸入和輸出參數的詳細資訊，請參閱 [EXECUTE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/execute-transact-sql)。  
  
##  <a name="getting-values-of-return-codes"></a><a name="Return_codes"></a>取得傳回碼的值  
 預存程序可以傳回稱為傳回碼的整數值，以指出程序的執行狀態。 若要在執行 SQL 工作中實作傳回碼，請使用 `ReturnValue` 類型的參數。  
  
 下表依據連接類型列出實作傳回碼的部分 EXEC 命令範例。 所有的範例都使用 `input` 參數。 所有參數類型（、和）的使用參數標記和參數名稱的規則都相同 `Input` `Output` `ReturnValue` 。  
  
 部分語法不支援參數常值。 在這種情況下，您必須使用變數來提供參數值。  
  
|連線類型|EXEC 語法|  
|---------------------|-----------------|  
|EXCEL 和 OLEDB|`EXEC ? = myStoredProcedure 1`|  
|ODBC|`{? = call myStoredProcedure(1)}`<br /><br /> 如需 ODBC CALL 語法的詳細資訊，請參閱 MSDN Library 之《ODBC 程式設計人員參考》中的主題 [程序參數](https://go.microsoft.com/fwlink/?LinkId=89462)。|  
|ADO|如果 Isquerystoreprocedure 設設定為 `False` ，`EXEC ? = myStoredProcedure 1`<br /><br /> 如果 Isquerystoreprocedure 設設定為 `True` ，`myStoredProcedure`|  
|[!INCLUDE[vstecado](../includes/vstecado-md.md)]|Set Isquerystoreprocedure 設設定為 `True` 。<br /><br /> `myStoredProcedure`|  
  
 在上表顯示的語法中，「執行 SQL」工作使用 [直接輸入]**** 來源類型執行預存程序。 「執行 SQL」工作也可以使用 [檔案連接]**** 來源類型執行預存程序。 不論「執行 SQL」工作是使用 [**直接輸入**] 或 [檔案**連接**] 來源類型，都請使用類型的參數 `ReturnValue` 來執行傳回碼。 如需如何設定「執行 SQL」工作所執行之 SQL 陳述式來源類型的詳細資訊，請參閱[執行 SQL 工作編輯器 &#40;一般頁面&#41;](general-page-of-integration-services-designers-options.md)。  
  
 如需搭配 Transact-SQL 預存程序使用傳回碼的詳細資訊，請參閱 [RETURN &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/return-transact-sql)。  
  
##  <a name="configuring-parameters-and-return-codes-in-the-execute-sql-task"></a><a name="Configure_parameters_and_return_codes"></a>在執行 SQL 工作中設定參數和傳回碼  
 如需可以在 [ [!INCLUDE[ssIS](../includes/ssis-md.md)] 設計師] 中設定之參數和傳回碼屬性的詳細資訊，請按一下下列主題：  
  
-   [[執行 SQL 工作編輯器] &#40;[參數對應] 頁面&#41;](../../2014/integration-services/execute-sql-task-editor-parameter-mapping-page.md)  
  
 如需有關如何在「 [!INCLUDE[ssIS](../includes/ssis-md.md)] 設計師」中設定這些屬性的詳細資訊，請按下列主題：  
  
-   [設定工作或容器的屬性](../../2014/integration-services/set-the-properties-of-a-task-or-container.md)  
  
## <a name="related-tasks"></a>相關工作  
 [設定工作或容器的屬性](../../2014/integration-services/set-the-properties-of-a-task-or-container.md)  
  
## <a name="related-content"></a>相關內容  
  
-   位於 blogs.msdn.com 的部落格項目： [Stored procedures with output parameters](https://go.microsoft.com/fwlink/?LinkId=157786)(使用輸出參數的預存程序)  
  
-   位於 msftisprodsamples.codeplex.com 的 CodePlex 範例： [執行 SQL 參數和結果集](https://go.microsoft.com/fwlink/?LinkId=157863)  
  
## <a name="see-also"></a>另請參閱  
 [執行 SQL 工作](control-flow/execute-sql-task.md)   
 [執行 SQL 工作中的結果集](../../2014/integration-services/result-sets-in-the-execute-sql-task.md)  
  
  
