---
title: "執行 SQL 工作 |Microsoft 文件"
ms.custom:
- ssisdev020617
ms.date: 03/13/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.executesqltask.f1
- sql13.dts.designer.executesqltask.general.f1
- sql13.dts.designer.executesqltask.parametermapping.f1
- sql13.dts.designer.executesqltask.resultset.f1
helpviewer_keywords:
- Transact-SQL statements, SSIS
- statements [Integration Services]
- batches [Integration Services]
- Execute SQL task [Integration Services]
ms.assetid: bebb2e8c-0410-43b2-ac2f-6fc80c8f2e9e
caps.latest.revision: 115
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: c6e8206cfceb0fe643fc537fa4e343731e7c21cb
ms.contentlocale: zh-tw
ms.lasthandoff: 08/03/2017

---
# <a name="execute-sql-task"></a>執行 SQL 工作
  「執行 SQL」工作會執行封裝中的 SQL 陳述式或預存程序。 工作可以包含逐次執行的單一 SQL 陳述式或多重 SQL 陳述式。 您可將執行 SQL 工作用於下列用途：  
  
-   截斷資料表或檢視，為插入資料做準備。  
  
-   建立、改變和卸除資料庫物件，例如資料表和檢視。  
  
-   將資料載入至事實 (Fact) 和維度 (Dimension) 資料表之前，先重建這些資料表。  
  
-   執行預存程序。 如果 SQL 陳述式叫用會從暫存資料表傳回結果的預存程序，請使用 WITH RESULT SETS 選項來定義結果集的中繼資料。  
  
-   將從查詢傳回的資料列集儲存到變數中。  
  
 執行 SQL 工作可搭配「Foreach 迴圈」容器和「For 迴圈」容器，用來執行多個 SQL 陳述式。 這些容器會實作封裝中重複的控制流程，並且可以重複執行「執行 SQL」工作。 例如，若使用「Foreach 迴圈」容器，封裝即可列舉資料夾中的檔案，並重複執行「執行 SQL」工作，以便執行每個檔案中儲存的 SQL 陳述式。  
  
## <a name="connect-to-a-data-source"></a>連接到資料來源  
 執行 SQL 工作可使用不同類型的連接管理員，以連接到其執行 SQL 陳述式或預存程序的資料來源。 此工作可使用下表中列出的連接類型。  
  
|連接類型|[ODBC 目的地編輯器]|  
|---------------------|------------------------|  
|EXCEL|[Excel 連接管理員](../../integration-services/connection-manager/excel-connection-manager.md)|  
|OLE DB|[OLE DB 連接管理員](../../integration-services/connection-manager/ole-db-connection-manager.md)|  
|ODBC|[ODBC 連接管理員](../../integration-services/connection-manager/odbc-connection-manager.md)|  
|ADO|[ADO 連接管理員](../../integration-services/connection-manager/ado-connection-manager.md)|  
|ADO.NET|[ADO.NET 連接管理員](../../integration-services/connection-manager/ado-net-connection-manager.md)|  
|SQLMOBILE|[SQL Server Compact Edition 連接管理員](../../integration-services/connection-manager/sql-server-compact-edition-connection-manager.md)|  
  
## <a name="create-sql-statements"></a>建立 SQL 陳述式  
 此工作所使用的 SQL 陳述式來源，可以是包含陳述式的工作屬性、包含一個或多個陳述式的檔案連接，或者包含陳述式的變數名稱。 SQL 陳述式必須以來源資料庫管理系統 (DBMS) 的用語撰寫。 如需詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 查詢](../../integration-services/integration-services-ssis-queries.md)。  
  
 如果 SQL 陳述式儲存在檔案中，則工作會使用「檔案」連接管理員連接到該檔案。 如需相關資訊，請參閱 [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md)。  
  
 在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師中，您可以使用 [執行 SQL 工作編輯器] 對話方塊輸入 SQL 陳述式，或使用圖形化使用者介面 [查詢產生器] 建立 SQL 查詢。 
  
> [!NOTE]  
>  「執行 SQL」工作可能無法成功剖析在「執行 SQL」工作外部撰寫的有效 SQL 陳述式。  
  
> [!NOTE]  
>  「執行 SQL」工作會使用 **RecognizeAll** ParseMode 列舉值。 如需詳細資訊，請參閱 [ManagedBatchParser Namespace](http://go.microsoft.com/fwlink/?LinkId=223617)(ManagedBatchParser 命名空間)。  
  
## <a name="send-multiple-statements-in-a-batch"></a>批次中傳送多個陳述式  
 如果您在執行 SQL 工作中加入多個陳述式，可將它們組成群組，並在批次中執行。 若要表示批次結束，請使用 GO 命令。 兩個 GO 命令之間的所有 SQL 陳述式，都會在一個批次中傳送至要執行的 OLE DB 提供者。 SQL 命令可包含以 GO 命令分隔的多個批次。  
  
 您可分組到同一個批次中的 SQL 陳述式有其限制。 如需詳細資訊，請參閱 [陳述式的批次](../../relational-databases/native-client-odbc-queries/executing-statements/batches-of-statements.md)。  
  
 如果執行 SQL 工作執行一個批次的 SQL 陳述式，則下列規則會套用至該批次︰  
  
-   只有一個陳述式可傳回結果集，且它必須是批次中的第一個陳述式。  
  
-   如果結果集使用結果繫結，則查詢必須傳回相同數目的資料行。 如果查詢傳回不同數目的資料行，工作便會失敗。 不過，即使工作失敗，它執行的查詢 (例如，DELETE 或 INSERT 查詢) 仍會成功。  
  
-   如果結果繫結使用資料行名稱，則查詢必須傳回名稱與工作所使用之結果集名稱相同的資料行。 如果資料行遺失，工作便會失敗。  
  
-   如果工作使用參數繫結，則批次中所有查詢的參數數目和類型都必須相同。  
  
## <a name="run-parameterized-sql-commands"></a>執行參數化的 SQL 命令  
 SQL 陳述式和預存程序經常使用輸入參數、輸出參數以及傳回碼。 「執行 SQL」工作支援 **Input**、 **Output**和 **ReturnValue** 參數類型。 您可以使用 **Input** 類型當做輸入參數，使用 **Output** 當做輸出參數，並使用 **ReturnValue** 當做傳回碼。  
  
> [!NOTE]  
>  只有在資料提供者支援參數時，您才能在執行 SQL 工作中使用參數。  
  
## <a name="specify-a-result-set-type"></a>指定結果集類型  
 根據 SQL 命令的類型而定，結果集可能會，也可能不會傳回到執行 SQL 工作。 例如，SELECT 陳述式通常會傳回結果集，INSERT 陳述式則不會。 來自 SELECT 陳述式的結果集可包含零個資料列、一個資料列或多個資料列。 預存程序亦可傳回整數值，稱為傳回碼，以表示程序的執行狀態。 在此情況下，結果集是由單一資料列所組成。  
  
## <a name="configure-the-execute-sql-task"></a>設定 「 執行 SQL 」 工作  
 您可以利用下列方式設定執行 SQL 工作：  
  
-   指定用來連接到資料庫的連接管理員類型。  
  
-   指定 SQL 陳述式傳回的結果集類型。  
  
-   指定 SQL 陳述式的逾時。  
  
-   指定 SQL 陳述式的來源。  
  
-   指示工作是否要略過 SQL 陳述式的準備階段。  
  
-   如果使用 ADO 連接類型，您必須指出 SQL 陳述式是否為預存程序。 如果是其他連接類型，此屬性為唯讀，且其值一律為 **false**。  
  
 您可以程式設計方式或透過「 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師」設定屬性。  

## <a name="general-page---execute-sql-task-editor"></a>-[一般] 頁面執行 SQL 工作編輯器
 使用 [執行 SQL 工作編輯器] 對話方塊的 [一般] 頁面，即可設定「執行 SQL」工作和提供該工作執行的 SQL 陳述式。  

若要深入了解 Transact-SQL 查詢語言，請參閱 [Transact-SQL 參考 &#40;資料庫引擎&#41;](../../t-sql/transact-sql-reference-database-engine.md)。  
  
### <a name="static-options"></a>靜態選項  
 **名稱**  
 提供唯一的名稱給工作流程中的執行 SQL 工作。 提供的名稱將顯示在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師內。  
  
 **描述**  
 描述執行 SQL 工作。 最佳作法是以其用途描述工作，使封裝可以自我記錄並易於維護。  
  
 **逾時**  
 指定工作在逾時之前執行的秒數上限。 值為 0 指出無限的時間。 預設值是 0。  
  
> [!NOTE]  
>  如果預存程序藉由提供大於 [逾時] 指定的秒數之連接時間與交易完成時間，使預存程序模擬睡眠功能，就不會發生逾時。 不過，執行查詢的預存程序一律會受到 [逾時] 所指定的時間限制。  
  
 **CodePage**  
 指定翻譯變數中的 Unicode 值時要使用的字碼頁。 預設值是本機電腦的字碼頁。  
  
> [!NOTE]  
>  當「執行 SQL」工作使用 ADO 或 ODBC 連線管理員時， **CodePage** 屬性就無法使用。 如果您的方案需要使用字碼頁，請使用 OLE DB 或 ADO.NET 連接管理員搭配執行 SQL 工作。  
  
 **TypeConversionMode**  
 將此屬性設為 **Allowed** 時，「執行 SQL」工作會嘗試將輸出參數和查詢結果轉換為指派結果之變數的資料類型。 這適用於 [單一資料列] 結果集類型。  
  
 **結果集**  
 指定 SQL 陳述式開始執行的預期結果類型。 在 [單一資料列]、[完整結果集]、[XML] 或 [無] 之間選擇。  
  
 **ConnectionType**  
 選擇用來連接到資料來源的連接管理員類型。 可用的連接類型包括 **OLE DB**、 **ODBC**、 **ADO**、 **ADO.NET** 和 **SQLMOBILE**。  
  
 **相關主題** [OLE DB 連線管理員](../../integration-services/connection-manager/ole-db-connection-manager.md)、 [ODBC 連線管理員](../../integration-services/connection-manager/odbc-connection-manager.md)、 [ADO 連線管理員](../../integration-services/connection-manager/ado-connection-manager.md)、 [ADO.NET 連線管理員](../../integration-services/connection-manager/ado-net-connection-manager.md)、 [SQL Server Compact Edition 連線管理員](../../integration-services/connection-manager/sql-server-compact-edition-connection-manager.md)  
  
 **連接**  
 從已定義的連接管理員清單中選擇連接。 若要建立新的連接，請選取\<**新增連接...**>.  
  
 **[Sqlsourcetype]**  
 選取工作執行之 SQL 陳述式的來源類型。  
  
 而根據執行 SQL 工作所使用的連接管理員類型，您必須在參數化 SQL 陳述式中使用特定的參數標記。    
  
 這個屬性具有下表中所列的選項。  
  
|Value|說明|  
|-----------|-----------------|  
|**直接輸入**|將來源設定為 Transact-SQL 陳述式。 選取此值會顯示動態選項 [SQLStatement]。|  
|**檔案連接**|選取包含 Transact-SQL 陳述式的檔案。 選取此選項會顯示動態選項 [FileConnection]。|  
|**變數**|將來源設定為定義 Transact-SQL 陳述式的變數。 選取此值會顯示動態選項 [SourceVariable]。|  
  
 **QueryIsStoredProcedure**  
 指出要執行之指定的 SQL 陳述式是否為預存程序。 只有工作使用 ADO 連接管理員時，此屬性才會是讀取/寫入。 否則此屬性是唯讀的，且其值為 **false**。  
  
 **BypassPrepare**  
 指出 SQL 陳述式是否已備妥。  **true** 會略過準備； **false** 會備妥再執行 SQL 陳述式。 只有搭配支援準備的 OLE DB 連接，才能使用此選項。  
  
 **相關主題**  [備妥的執行](../../relational-databases/native-client-odbc-queries/executing-statements/prepared-execution.md)  
  
 **瀏覽**  
 使用 [開啟] 對話方塊，以尋找包含 SQL 陳述式的檔案。 選取要將檔案內容以 SQL 陳述式複製到 **SQLStatement** 屬性的檔案。  
  
 **建立查詢**  
 使用 [查詢產生器] 對話方塊建立 SQL 陳述式，它是用來建立查詢的圖形化工具。 當 [SQLSourceType] 選項設定為 [直接輸入] 時，才能使用此選項。  
  
 **剖析查詢**  
 驗證 SQL 陳述式的語法。  
  
### <a name="sqlsourcetype-dynamic-options"></a>SQLSourceType 動態選項  
  
#### <a name="sqlsourcetype--direct-input"></a>SQLSourceType = 直接輸入  
 **例如：**  
 在選項方塊中輸入要執行的 SQL 陳述式，或按一下瀏覽按鈕 (…) 在 [輸入 SQL 查詢] 對話方塊中輸入 SQL 陳述式，或按一下 [建立查詢] 使用 [查詢產生器] 對話方塊來撰寫陳述式。  
  
 **相關主題**︰[查詢產生器](http://msdn.microsoft.com/library/780752c9-6e3c-4f44-aaff-4f4d5e5a45c5)  
  
#### <a name="sqlsourcetype--file-connection"></a>SQLSourceType = 檔案連接  
 **FileConnection**  
 選取現有的檔案連接管理員，或按一下\<**新增連接...**> 以建立新的連接管理員。  
  
 **相關主題：** [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md)、 [File Connection Manager Editor](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
#### <a name="sqlsourcetype--variable"></a>SQLSourceType = 變數  
 **SourceVariable**  
 選取現有的變數，或按一下\<**新增變數...**> 若要建立新的變數。  
  
 **相關主題**：[Integration Services &#40;SSIS&#41; 變數](../../integration-services/integration-services-ssis-variables.md)、[加入變數](http://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)  
 
## <a name="parameter-mapping-page---execute-sql-task-editor"></a>參數對應頁面-執行 SQL 工作編輯器
使用 [執行 SQL 工作編輯器] 對話方塊的 [參數對應] 頁面，即可將變數對應到 SQL 陳述式中的參數。  
  
### <a name="options"></a>選項  
 **變數名稱**  
 按一下 [加入參數對應之後**新增**，從清單中選取系統或使用者定義的變數，或按一下\<**新增變數...**> 若要加入新的變數使用**加入變數**] 對話方塊。  
  
 **相關主題：**[Integration Services &#40;SSIS&#41; 變數](../../integration-services/integration-services-ssis-variables.md)  
  
 **方向**  
 選取參數的方向。 將每個變數對應到輸入參數、輸出參數或傳回碼。  
  
 **資料型別**  
 選取參數的資料類型。 在工作所使用之連接管理員中選取的提供者，各有其專用的可用資料類型清單。  
  
 **參數名稱**  
 提供參數名稱。  
  
 您必須根據工作所使用的連接管理員類型，來使用數字或參數名稱。 有些連接管理員類型需要參數名稱的第一個字元是 @ 符號、 特定名稱@Param1，或做為參數名稱的資料行名稱。  
  
 **參數的大小**  
 提供具有可變長度之參數的大小，例如字串和二進位欄位。  
  
 此設計可確保提供者能為可變長度的參數值配置足夠的空間。  
  
 **新增**  
 按一下即可加入參數對應。  
  
 **移除**  
 在清單中選取參數對應，然後按一下 [移除]。  
 
## <a name="result-set-page---execute-sql-task-editor"></a>結果集頁面-執行 SQL 工作編輯器
使用 [執行 SQL 工作編輯器] 對話方塊的 [結果集] 頁面，即可將 SQL 陳述式的結果對應至新的或現有的變數。 如果 [一般] 頁面上的 [結果集] 已設定為 [無]，就會停用此對話方塊中的選項。  
  
### <a name="options"></a>選項  
 **結果名稱**  
 按一下 [加入] 加入結果集對應集之後，請為結果提供名稱。 您必須根據結果集類型來使用特定的結果名稱。  
  
 如果結果集類型是「 **單一資料列**」，則您可以使用查詢所傳回之資料行的名稱，或查詢所傳回之資料行的資料行清單中，代表資料行位置的數字。  
  
 如果結果集類型為 **完整結果集** 或 **XML**，則必須使用 0 作為結果集名稱。  
 
  
 **變數名稱**  
 將選取的變數或按一下 [設定為變數的結果對應\<**新增變數...**> 若要加入新的變數使用**加入變數**] 對話方塊。  
  
 **加入**  
 按一下即可新增結果集對應。  
  
 **移除**  
 選取清單中的結果集對應，然後按一下 [移除]。  
 
## <a name="parameters-in-the-execute-sql-task"></a>中的參數執行 SQL 工作
SQL 陳述式和預存程序經常使用 **輸入** 參數、 **輸出** 參數以及傳回碼。 在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 中，「執行 SQL」工作支援 **Input**、**Output** 和 **ReturnValue** 參數類型。 您可針對輸入參數使用 **Input** 類型、針對輸出參數使用 **Output** ，且針對傳回碼使用 **ReturnValue** 。  
  
> [!NOTE]  
>  只有在資料提供者支援參數時，您才能在執行 SQL 工作中使用參數。  
  
 SQL 命令中的參數 (包括查詢和預存程序) 都會對應到在執行 SQL 工作範圍內、父容器內或封裝範圍內建立的使用者自訂變數。 變數值可於設計階段設定，或於執行階段動態擴展。 您也可以將參數對應到系統變數。 如需詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 變數](../../integration-services/integration-services-ssis-variables.md)和[系統變數](../../integration-services/system-variables.md)。  
  
 不過，在執行 SQL 工作中使用參數和傳回碼比只是知道工作支援的參數類型，以及如何對應這些參數還要複雜。 若要在執行 SQL 工作中成功使用參數和傳回碼，需要有其他使用需求與指導方針。 本主題的其餘部分包含這些使用需求和指導方針：  
  
-   [使用參數名稱和標記](#Parameter_names_and_markers)  
  
-   [搭配日期和時間資料類型使用參數](#Date_and_time_data_types)  
  
-   [在 WHERE 子句中使用參數](#WHERE_clauses)  
  
-   [搭配預存程序使用參數](#Stored_procedures)  
  
-   [取得傳回碼的值](#Return_codes)    
  
###  <a name="Parameter_names_and_markers"></a>參數名稱和標記  
 依據執行 SQL 工作使用的連接類型，SQL 命令的語法會使用不同的參數標記。 例如，[!INCLUDE[vstecado](../../includes/vstecado-md.md)]連接管理員類型要求 SQL 命令必須使用格式的參數標記 **@varParameter** ，而 OLE DB 連接類型需要使用問號 （？） 參數標記。  
  
 在變數與參數的對應中，可以用來當做參數名稱的名稱也會隨著連線管理員的類型而異。 例如，[!INCLUDE[vstecado](../../includes/vstecado-md.md)] 連線管理員類型使用具有 @ 前置詞的使用者自訂名稱，而 OLE DB 連線管理員類型則要求您必須使用以 0 為基底的序數數值做為參數名稱。  
  
 下表摘要說明執行 SQL 工作可以使用之連線管理員類型的 SQL 命令需求。  
  
|連接類型|參數標記|參數名稱|範例 SQL 命令|  
|---------------------|----------------------|--------------------|-------------------------|  
|ADO|?|Param1, Param2, …|SELECT FirstName, LastName, Title FROM Person.Contact WHERE ContactID = ?|  
|[!INCLUDE[vstecado](../../includes/vstecado-md.md)]|@\<參數名稱 >|@\<參數名稱 >|選取從 Person.Contact 標題的 FirstName、 LastName 其中 ContactID =@parmContactID|  
|ODBC|?|1, 2, 3, …|SELECT FirstName, LastName, Title FROM Person.Contact WHERE ContactID = ?|  
|EXCEL 和 OLE DB|?|0, 1, 2, 3, …|SELECT FirstName, LastName, Title FROM Person.Contact WHERE ContactID = ?|  
  
#### <a name="use-parameters-with-adonet-and-ado-connection-managers"></a>搭配 ADO.NET 和 ADO 連接管理員使用參數  
 [!INCLUDE[vstecado](../../includes/vstecado-md.md)]和 ADO 連接管理員有使用參數的 SQL 命令的特定需求：  
  
-   [!INCLUDE[vstecado](../../includes/vstecado-md.md)]連接管理員要求 SQL 命令必須使用參數名稱做為參數標記。 這表示變數可以直接對應到參數。 例如， `@varName` 變數會對應到名為 `@parName` 的參數，並提供值給 `@parName`參數。  
  
-   ADO 連接管理員要求 SQL 命令必須使用問號 (?) 做為參數標記。 不過，您可以使用整數值之外的任何使用者自訂名稱做為參數名稱。  
  
 若要提供值給參數，變數會對應到參數名稱。 接著，執行 SQL 工作會在參數清單中使用參數名稱的序數值，將值從變數載入參數中。  
  
#### <a name="use-parameters-with-excel-odbc-and-ole-db-connection-managers"></a>使用 EXCEL、 ODBC 和 OLE DB 連接管理員中的參數  
 EXCEL、ODBC 和 OLE DB 連接管理員要求 SQL 命令必須使用問號 (?) 做為參數標記，並以 0 或 1 為基底的數值作為參數名稱。 如果執行 SQL 工作使用 ODBC 連接管理員，對應到查詢中第一個參數的參數名稱會被命名為 1，否則，該參數會被命名為 0。 對於後續的參數，參數名稱的數值表示 SQL 命令中，參數名稱所對應的參數。 例如，參數名稱 3 對應至第 3 個參數，這個參數在 SQL 命令中是由第 3 個問號 (?) 來代表。  
  
 為了將值提供給參數，變數會對應到參數名稱，而執行 SQL 工作則會使用參數名稱的序數值，將值從變數載入參數中。  
  
 依據連接管理員使用的提供者而定，部分 OLE DB 資料類型可能不受支援。 例如，Excel 驅動程式只能辨識有限的一組資料類型。 如需具有 Excel 驅動程式之 Jet 提供者行為的詳細資訊，請參閱 [Excel 來源](../../integration-services/data-flow/excel-source.md)。  
  
#### <a name="use-parameters-with-ole-db-connection-managers"></a>搭配 OLE DB 連接管理員使用參數  
 「執行 SQL」工作使用 OLE DB 連線管理員時，即可使用工作的 BypassPrepare 屬性。 如果「執行 SQL」工作搭配參數使用 SQL 陳述式，您應該將這個屬性設為 [true]。  
  
 您在使用 OLE DB 連接管理員時無法使用參數化的子查詢，因為執行 SQL 工作無法透過 OLE DB 提供者衍生參數資訊。 不過，您可以使用運算式，將參數值串連到查詢字串，並設定工作的 SqlStatementSource 屬性。  
  
###  <a name="Date_and_time_data_types"></a>使用日期和時間資料型別參數  
  
#### <a name="use-date-and-time-parameters-with-adonet-and-ado-connection-managers"></a>搭配 ADO.NET 和 ADO 連接管理員使用日期和時間參數  
 讀取 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 類型的資料，即 **time** 和 **datetimeoffset** 時，使用 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 或 ADO 連線管理員的「執行 SQL」工作有下列額外需求：  
  
-   若是 **time** 資料，[!INCLUDE[vstecado](../../includes/vstecado-md.md)] 連線管理員要求此資料必須儲存在參數類型為 **Input** 或 **Output**，且資料類型為 **string** 的參數中。  
  
-   若是 **datetimeoffset** 資料，[!INCLUDE[vstecado](../../includes/vstecado-md.md)] 連線管理員要求此資料必須儲存在下列其中一個參數中：  
  
    -   參數類型為 **Input** ，且資料類型為 **string**的參數。  
  
    -   參數類型為 **Output** 或 **ReturnValue**，且資料類型為 **datetimeoffset**、 **string**或 **datetime2**的參數。 如果您選取資料類型為 **string** 或 **datetime2** 的參數，[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 會將資料轉換為字串或 datetime2。  
  
-   ADO 連線管理員要求 **time** 或 **datetimeoffset** 資料必須儲存在參數類型為 **Input** 或 **Output**，且資料類型為 **adVarWchar** 的參數中。  
  
 如需 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型以及如何將其對應到 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 資料類型的詳細資訊，請參閱[資料類型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md) 和 [Integration Services 資料類型](../../integration-services/data-flow/integration-services-data-types.md)。  
  
#### <a name="use-date-and-time-parameters-with-ole-db-connection-managers"></a>搭配 OLE DB 連接管理員使用日期和時間參數  
 使用 OLE DB 連線管理員時，「執行 SQL」工作對於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型，即 **date**、**time**、**datetime**、**datetime2** 和 **datetimeoffset** 的資料具有特定的儲存需求。 您必須以下列其中一種參數類型儲存此資料：  
  
-   NVARCHAR 資料類型的輸入參數。  
  
-   具有適當資料類型的輸出參數，如下表所列示。  
  
    |**Output** 參數類型|日期資料類型|  
    |-------------------------------|--------------------|  
    |DBDATE|**date**|  
    |DBTIME2|**time**|  
    |DBTIMESTAMP|**datetime**、 **datetime2**|  
    |DBTIMESTAMPOFFSET|**datetimeoffset**|  
  
 如果資料沒有以適當的輸入或輸出參數儲存，則封裝會失敗。  
  
#### <a name="use-date-and-time-parameters-with-odbc-connection-managers"></a>搭配 ODBC 連接管理員使用日期和時間參數  
 使用 ODBC 連線管理員時，「執行 SQL」工作對於具有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型之一，即 **date**、**time**、**datetime**、**datetime2** 或 **datetimeoffset** 的資料具有特定的儲存需求。 您必須以下列其中一種參數類型儲存此資料：  
  
-   SQL_WVARCHAR 資料類型的 **input** 參數。  
  
-   具有適當資料類型的 **output** 參數，如下表所列示。  
  
    |**Output** 參數類型|日期資料類型|  
    |-------------------------------|--------------------|  
    |SQL_DATE|**date**|  
    |SQL_SS_TIME2|**time**|  
    |SQL_TYPE_TIMESTAMP<br /><br /> -或-<br /><br /> SQL_TIMESTAMP|**datetime**、 **datetime2**|  
    |SQL_SS_TIMESTAMPOFFSET|**datetimeoffset**|  
  
 如果資料沒有以適當的輸入或輸出參數儲存，則封裝會失敗。  
  
###  <a name="WHERE_clauses"></a>在 WHERE 子句中使用參數  
 SELECT、INSERT、UPDATE 和 DELETE 命令經常包含 WHERE 子句，以指定篩選條件，用以定義來源資料表中每個資料列必須符合才能做為 SQL 命令的條件。 參數會在 WHERE 子句中提供篩選值。  
  
 您可以使用參數標記，動態提供參數值。 SQL 陳述式中可以使用的參數標記和參數名稱的規則，需視「執行 SQL」所使用的連接管理員類型而定。  
  
 下表依照連接管理員類型列出 SELECT 命令的範例。 INSERT、UPDATE 和 DELETE 陳述式與這些範例類似。 這些範例使用 SELECT，從 [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)] 的 **Product** 資料表傳回 **ProductID** 大於及小於兩個參數所指定之值的產品。  
  
|連接類型|SELECT 語法|  
|---------------------|-------------------|  
|EXCEL、ODBC 和 OLEDB|`SELECT* FROM Production.Product WHERE ProductId > ? AND ProductID < ?`|  
|ADO|`SELECT* FROM Production.Product WHERE ProductId > ? AND ProductID < ?`|  
|[!INCLUDE[vstecado](../../includes/vstecado-md.md)]|`SELECT* FROM Production.Product WHERE ProductId > @parmMinProductID AND ProductID < @parmMaxProductID`|  
  
 這些範例必須使用具有下列名稱的參數：  
  
-   EXCEL 和 OLED DB 連接管理員使用參數名稱 0 和 1。 ODBC 連接類型則使用 1 和 2。  
  
-   ADO 連接類型可以使用任何兩個參數名稱，例如 Param1 和 Param2，但這些名稱必須對應它們在參數清單中的序數位置。  
  
-   [!INCLUDE[vstecado](../../includes/vstecado-md.md)]連接類型使用參數名稱@parmMinProductID和@parmMaxProductID。  
  
###  <a name="Stored_procedures"></a>預存程序使用參數  
 執行預存程序的 SQL 命令亦可使用參數對應。 如何使用參數標記和參數名稱的規則，需視「執行 SQL」所使用的連接管理員類型而定，這一點與參數化查詢的規則相同。  
  
 下表依照連接管理員類型列出 EXEC 命令的範例。 這些範例會執行 [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)] 中的 **uspGetBillOfMaterials** 預存程序。 預存程序會使用 `@StartProductID` 和 `@CheckDate` **輸入** 參數。  
  
|連接類型|EXEC 語法|  
|---------------------|-----------------|  
|EXCEL 和 OLEDB|`EXEC uspGetBillOfMaterials ?, ?`|  
|ODBC|`{call uspGetBillOfMaterials(?, ?)}`<br /><br /> 如需 ODBC CALL 語法的詳細資訊，請參閱 MSDN Library 之《ODBC 程式設計人員參考》中的主題 [程序參數](http://go.microsoft.com/fwlink/?LinkId=89462)。|  
|ADO|如果設為 IsQueryStoredProcedure **False**，`EXEC uspGetBillOfMaterials ?, ?`<br /><br /> 如果設為 IsQueryStoredProcedure **True**，`uspGetBillOfMaterials`|  
|[!INCLUDE[vstecado](../../includes/vstecado-md.md)]|如果設為 IsQueryStoredProcedure **False**，`EXEC uspGetBillOfMaterials @StartProductID, @CheckDate`<br /><br /> 如果設為 IsQueryStoredProcedure **True**，`uspGetBillOfMaterials`|  
  
 若要使用輸出參數，此語法要求您必須在每個參數標記後面加上 OUTPUT 關鍵字。 例如，下列輸出參數語法是正確的：`EXEC myStoredProcedure ? OUTPUT`。  
  
 如需搭配 Transact-SQL 預存程序使用輸入和輸出參數的詳細資訊，請參閱 [EXECUTE &#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md)。  
 
### <a name="map-query-parameters-to-variables"></a>將查詢參數對應至變數
本章節描述如何在執行 SQL 工作中使用參數化的 SQL 陳述式，以及建立 SQL 陳述式中的變數和參數之間的對應。  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，開啟您要使用的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝。  
  
2.  在 [方案總管] 中，按兩下封裝將其開啟。  
  
3.  按一下 **[控制流程]** 索引標籤。  
  
4.  如果封裝尚未包含執行 SQL 工作，則會加入一個執行 SQL 工作至封裝的控制流程。 如需詳細資訊，請參閱 [在控制流程中加入或刪除工作或容器](../../integration-services/control-flow/add-or-delete-a-task-or-a-container-in-a-control-flow.md)。  
  
5.  按兩下執行 SQL 工作。  
  
6.  以下列方式的其中之一提供參數化 SQL 命令：  
  
    -   使用直接輸入，並在 SQLStatement 屬性中輸入 SQL 命令。  
  
    -   使用直接輸入，按一下 [建立查詢]，然後使用「查詢產生器」提供的圖形工具來建立 SQL 命令。  
  
    -   使用檔案連接，然後參考包含 SQL 命令的檔案。  
  
    -   使用變數，然後參考包含 SQL 命令的變數。  
  
     您在參數化 SQL 陳述式中使用的參數標記，需視「執行 SQL」工作所使用的連接類型而定。  
  
    |連接類型|參數標記|  
    |---------------------|----------------------|  
    |ADO|?|  
    |ADO.NET 和 SQLMOBILE|@\<參數名稱 >|  
    |ODBC|?|  
    |EXCEL 和 OLE DB|?|  
  
     下表依照連接管理員類型列出 SELECT 命令的範例。 參數會在 WHERE 子句中提供篩選值。 這些範例使用 SELECT，從 **中的** Product [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)] 資料表傳回 **ProductID** 大於及小於兩個參數所指定之值的產品。  
  
    |連接類型|SELECT 語法|  
    |---------------------|-------------------|  
    |EXCEL、ODBC 和 OLEDB|`SELECT* FROM Production.Product WHERE ProductId > ? AND ProductID < ?`|  
    |ADO|`SELECT* FROM Production.Product WHERE ProductId > ? AND ProductID < ?`|  
    |[!INCLUDE[vstecado](../../includes/vstecado-md.md)]|`SELECT* FROM Production.Product WHERE ProductId > @parmMinProductID AND ProductID < @parmMaxProductID`|  
   
7.  按一下 [參數對應]。  
  
8.  若要加入參數對應，請按一下 [加入]。  
  
9. 在 [參數名稱] 方塊中提供名稱。  
  
     您所使用的參數名稱需視「執行 SQL」工作所使用的連接類型而定。  
  
    |連接類型|參數名稱|  
    |---------------------|--------------------|  
    |ADO|Param1, Param2, …|  
    |ADO.NET 和 SQLMOBILE|@\<參數名稱 >|  
    |ODBC|1, 2, 3, …|  
    |EXCEL 和 OLE DB|0, 1, 2, 3, …|  
  
10. 從 [變數名稱] 清單中，選取一個變數。 如需詳細資訊，請參閱[加入、刪除、變更封裝中使用者定義變數的範圍](http://msdn.microsoft.com/library/cbf40c7f-3c8a-48cd-aefa-8b37faf8b40e)。  
  
11. 在 [方向] 清單中，指定參數是輸入、輸出還是傳回值。  
  
12. 在 [資料類型] 清單中，設定參數的資料類型。  
  
    > [!IMPORTANT]  
    >  參數的資料類型必須與變數的資料類型相容。  
  
13. 針對 SQL 陳述式中的每個參數，重複步驟 8 到 11。  
  
    > [!IMPORTANT]  
    >  參數對應的順序必須與參數在 SQL 陳述式中出現的順序相同。  
  
14. 按一下 **[確定]**。  

##  <a name="Return_codes"></a>取得傳回碼的值  
 預存程序可以傳回稱為傳回碼的整數值，以指出程序的執行狀態。 若要在「執行 SQL」工作中實作傳回碼，請使用 **ReturnValue** 類型的參數。  
  
 下表依據連接類型列出實作傳回碼的部分 EXEC 命令範例。 所有的範例都使用 **Input** 參數。 所有參數類型 (**Input**、 **Output**和 **ReturnValue**) 之使用參數標記和參數名稱的規則都相同。  
  
 部分語法不支援參數常值。 在這種情況下，您必須使用變數來提供參數值。  
  
|連接類型|EXEC 語法|  
|---------------------|-----------------|  
|EXCEL 和 OLEDB|`EXEC ? = myStoredProcedure 1`|  
|ODBC|`{? = call myStoredProcedure(1)}`<br /><br /> 如需 ODBC CALL 語法的詳細資訊，請參閱 MSDN Library 之《ODBC 程式設計人員參考》中的主題 [程序參數](http://go.microsoft.com/fwlink/?LinkId=89462)。|  
|ADO|如果設為 IsQueryStoreProcedure **False**，`EXEC ? = myStoredProcedure 1`<br /><br /> 如果設為 IsQueryStoreProcedure **True**，`myStoredProcedure`|  
|[!INCLUDE[vstecado](../../includes/vstecado-md.md)]|將 IsQueryStoreProcedure 設為 [True]。<br /><br /> `myStoredProcedure`|  
  
 在上表顯示的語法中，「執行 SQL」工作使用 [直接輸入] 來源類型執行預存程序。 「執行 SQL」工作也可以使用 [檔案連接] 來源類型執行預存程序。 不論「執行 SQL」工作是使用 [直接輸入] 或 [檔案連接] 來源類型，都請使用 **ReturnValue** 類型的參數來實作傳回碼。
  
 如需搭配 Transact-SQL 預存程序使用傳回碼的詳細資訊，請參閱 [RETURN &#40;Transact-SQL&#41;](../../t-sql/language-elements/return-transact-sql.md)。  
  
## <a name="result-sets-in-the-execute-sql-task"></a>執行 SQL 工作中的結果集
 在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝中，結果集是否會傳回到執行 SQL 工作，端視工作所使用的 SQL 命令類型而定。 例如，SELECT 陳述式通常會傳回結果集，INSERT 陳述式則不會。  
  
 結果集所包含的內容也會隨著 SQL 命令而有所不同。 例如，來自 SELECT 陳述式的結果集可包含零個資料列、一個資料列或多個資料列。 但是，SELECT 陳述式中傳回計數或總和的結果集只包含單一資料列。  
  
 在執行 SQL 工作中使用結果集比只是知道 SQL 命令是否傳回結果集，以及結果集所包含的內容還要複雜。 若要在執行 SQL 工作中成功使用結果集，需要有其他使用需求與指導方針。 本主題的其餘部分包含這些使用需求和指導方針：  
  
-   [指定結果集類型](#Result_set_type)  
  
-   [以結果集填入變數](#Populate_variable_with_result_set)  
  
###  <a name="Result_set_type"></a>指定結果集類型  
 執行 SQL 工作支援下列類型的結果集︰  
  
-   **無** ：結果集是在查詢未傳回任何結果時使用。 例如，此結果集用於加入、變更和刪除資料表中記錄的查詢。  
  
-   **單一資料列** ：結果集是在查詢只傳回一個資料列時使用。 例如，此結果集用於傳回計數或總和的 SELECT 陳述式。  
  
-   **完整結果集** ：結果集是在查詢傳回多個資料列時使用。 例如，此結果集用於擷取資料表中所有資料列的 SELECT 陳述式。  
  
-   **XML** ：結果集是在查詢傳回 XML 格式的結果集時使用。 例如，此結果集用於包含 FOR XML 子句的 SELECT 陳述式。  
  
 如果執行 SQL 工作使用 **[完整結果集]** 結果集，且查詢傳回多個資料列集，則工作只會傳回第一個資料列集。 如果此資料列集產生錯誤，則工作會報告該錯誤。 如果其他資料列集產生錯誤，則工作不會報告它們。  
  
###  <a name="Populate_variable_with_result_set"></a>填入具有結果集的變數  
 如果查詢傳回的結果集類型為單一資料列、資料列集或 XML，則您可將結果集繫結至使用者自訂的變數。  
  
 如果結果集類型為 **Single row**，則可以藉由使用資料行名稱做為結果集名稱將傳回結果中的資料行繫結至變數，或者可以使用資料行清單中資料行的序數位置做為結果集名稱。 例如，查詢 `SELECT Color FROM Production.Product WHERE ProductID = ?` 的結果集名稱可以為 **Color** 或 **0**。 如果查詢傳回多個資料行，並且您要存取所有資料行中的值，則您必須將每個資料行繫結至不同的變數。 如果您透過使用數字做為結果集名稱將資料行對應至變數，則該數字會反映資料行在查詢的資料行清單中所顯示的順序。 例如，在查詢 `SELECT Color, ListPrice, FROM Production.Product WHERE ProductID = ?`中，您將 0 用於 **Color** 資料行，將 1 用於 **ListPrice** 資料行。 使用資料行名稱做為結果集名稱的功能取決於將該工作設定為使用的提供者。 並非所有的提供者可以使用資料行名稱做為結果集名稱。  
  
 部分傳回單一值的查詢可能不包含資料行名稱。 例如， `SELECT COUNT (*) FROM Production.Product` 陳述式不會傳回任何資料行名稱。 您可以使用序數位置 0 做為結果名稱來存取傳回的結果。 若要存取傳回結果資料行名稱，此查詢必須包含 AS\<別名名稱 > 子句，以提供資料行名稱。 `SELECT COUNT (*)AS CountOfProduct FROM Production.Product`陳述式會提供 **CountOfProduct** 資料行。 接著您可以使用 **CountOfProduct** 資料行名稱或序數位置 0 來存取傳回結果資料行。  
  
 如果結果集類型為 **完整結果集** 或 **XML**，則必須使用 0 作為結果集名稱。  
  
 當您將變數對應至結果集類型為 **Single row** 的結果集時，此變數須具有與結果集包含的資料行之資料類型相容的資料類型。 例如，包含資料類型為 **String** 之資料行的結果集不能對應至數值資料類型的變數。 將 **[TypeConversionMode]** 屬性設為 **Allowed**時，「執行 SQL」工作會嘗試將輸出參數和查詢結果轉換為指派結果之變數的資料類型。  
  
 XML 結果集只可對應至資料類型為 **String** 或 **Object** 的變數。 如果變數有 **String** 資料類型，則執行 SQL 工作會傳回字串，且 XML 來源可使用 XML 資料。 如果變數具有 **Object** 資料類型，則執行 SQL 工作會傳回「文件物件模組」(DOM) 物件。  
  
 **[完整結果集]** 必須對應至資料類型為 **Object** 的變數。 傳回結果為資料列集物件。 您可以使用 Foreach 迴圈容器，將儲存在 Object 變數中的資料表資料列值，擷取到封裝變數中，然後使用指令碼工作，將儲存在封裝變數中的資料寫入檔案。 如需如何使用 Foreach 迴圈容器和指令碼工作執行此作業的示範，請參閱 msftisprodsamples.codeplex.com 上的 CodePlex 範例 [執行 SQL 參數及結果集](http://go.microsoft.com/fwlink/?LinkId=157863)(英文)。  
  
 下表列出可對應至結果集之變數的資料類型。  
  
|結果集類型|變數的資料類型|物件類型|  
|---------------------|---------------------------|--------------------|  
|單一資料列|與結果集之類型資料行相容的任何類型。|不適用|  
|完整結果集|**物件**|如果工作使用原生連接管理員 (包括 ADO、OLE DB、Excel 與 ODBC 連接管理員)，則傳回的物件是 ADO **Recordset**。<br /><br /> 如果工作使用 Managed 連線管理員 (例如 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 連線管理員)，傳回的物件便會是 **System.Data.DataSet**。<br /><br /> 您可以使用指令碼工作來存取 **System.Data.DataSet** 物件，如下列範例所示。<br /><br /> `Dim dt As Data.DataTable`<br /><br /> `Dim ds As Data.DataSet = CType(Dts.Variables("Recordset").Value, DataSet) dt = ds.Tables(0)`|  
|XML|**字串**|**字串**|  
|XML|**物件**|如果工作使用原生連接管理員 (包括 ADO、OLE DB、Excel 與 ODBC 連接管理員)，則傳回的物件是 **MSXML6.IXMLDOMDocument**。<br /><br /> 如果工作使用 Managed 連線管理員 (例如 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 連線管理員)，傳回的物件便會是 **System.Xml.XmlDocument**。|  
  
 變數可在執行 SQL 工作或封裝範圍內定義。 如果變數包含封裝範圍，則結果集可用於該封裝內的其他工作和容器，並可用於「執行封裝」或「執行 DTS 2000 封裝」工作所執行的任何封裝。  
  
 將變數對應到 **單一資料列** 結果集時，如果符合下列條件，SQL 陳述式傳回的非字串值就會轉換為字串：  
  
-   **TypeConversionMode** 屬性設為 True。 您可以在 [屬性] 視窗中設定屬性值，也可以使用 **[執行 SQL 工作編輯器]**。  
  
-   轉換不會導致資料截斷。  
  
## <a name="map-result-sets-to-variables-in-an-execute-sql-task"></a>在執行 SQL 工作中將結果集對應至變數
本章節描述如何在執行 SQL 工作中建立結果集與變數之間的對應。 將結果集對應至變數後，封裝中的其他元素便可使用該結果集。 例如，指令碼工作中的指令碼可以讀取變數，然後使用結果集中的值，或是 XML 來源可以使用儲存在變數中的結果集。 如果結果集由父封裝產生，則可以藉由將結果集對應至父封裝中的變數，然後在子封裝中建立用來儲存父變數值的父封裝變數組態，以便讓「執行封裝」工作所呼叫的子封裝可以使用結果集。  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，開啟包含所需封裝的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 專案。  
  
2.  在方案總管中，按兩下封裝將其開啟。  
  
3.  按一下 **[控制流程]** 索引標籤。  
  
4.  如果封裝尚未包含執行 SQL 工作，則會加入一個執行 SQL 工作至封裝的控制流程。 如需詳細資訊，請參閱 [在控制流程中加入或刪除工作或容器](../../integration-services/control-flow/add-or-delete-a-task-or-a-container-in-a-control-flow.md)。  
  
5.  按兩下執行 SQL 工作。  
  
6.  在 [執行 SQL 工作編輯器] 對話方塊的 [一般] 頁面上，選取 [單一資料列]、[完整結果集] 或 [XML] 結果集類型。  

7.  按一下 [結果集]。  
  
8.  若要加入結果集對應，請按一下 [加入]。  
  
9. 從 [變數名稱] 清單中，選取變數或新建變數。 如需詳細資訊，請參閱[加入、刪除、變更封裝中使用者定義變數的範圍](http://msdn.microsoft.com/library/cbf40c7f-3c8a-48cd-aefa-8b37faf8b40e)。  
  
10. 在 [結果名稱] 清單中，選擇性地修改結果集的名稱。  
  
     一般而言，您可以使用資料行名稱做為結果集名稱，也可以資料行清單中資料行的序數位置做為結果集。 使用資料行名稱做為結果集名稱的功能取決於將該工作設定為使用的提供者。 並非所有的提供者可以使用資料行名稱做為結果集名稱。  
  
11. 按一下 **[確定]**。  

## <a name="troubleshoot-the-execute-sql-task"></a>疑難排解執行 SQL 工作  
 您可以記錄執行 SQL 工作對外部資料提供者執行的呼叫。 您可以使用這項記錄功能，疑難排解執行 SQL 工作所執行的 SQL 命令。 若要記錄「執行 SQL」工作對外部資料提供者執行的呼叫，請啟用封裝記錄，然後在封裝層級選取 [診斷] 事件。 如需詳細資訊，請參閱[封裝執行的疑難排解工具](../../integration-services/troubleshooting/troubleshooting-tools-for-package-execution.md)。  
  
 有時 SQL 命令或預存程序會傳回多個結果集。 這些結果集不只包括屬於 **SELECT** 查詢結果的資料列集，也包括屬於 **RAISERROR** 或 **PRINT** 陳述式之錯誤結果的單一值。 工作是否忽略發生在第一個結果集之後之結果集中的錯誤，將取決於所使用的連接管理員類型：  
  
-   使用 OLE DB 和 ADO 連接管理員時，工作會忽略發生在第一個結果集之後的結果集。 因此，使用這些連接管理員時，如果錯誤不屬於第一個結果集的一部分，便會忽略 SQL 命令或預存程序所傳回的錯誤。  
  
-   使用 ODBC 和 ADO.NET 連接管理員時，工作不會忽略發生在第一個結果集之後的結果集。 使用這些連接管理員時，如果第一個結果集之外的結果集包含錯誤，工作將會失敗。  
  
### <a name="custom-log-entries"></a>自訂記錄項目  
 下表描述「執行 SQL」工作的自訂記錄項目。 如需詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 記錄](../../integration-services/performance/integration-services-ssis-logging.md)。  
  
|記錄項目|說明|  
|---------------|-----------------|  
|**ExecuteSQLExecutingQuery**|提供 SQL 陳述式執行階段的相關資訊。 寫入記錄項目的時機包括在工作取得資料庫連接時、在工作開始準備 SQL 陳述式時，以及在 SQL 陳述式執行完成之後。 準備階段的記錄項目包含工作所使用的 SQL 陳述式。|  


