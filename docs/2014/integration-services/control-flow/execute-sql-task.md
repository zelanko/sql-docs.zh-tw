---
title: 執行 SQL 工作 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.executesqltask.f1
helpviewer_keywords:
- Transact-SQL statements, SSIS
- statements [Integration Services]
- batches [Integration Services]
- Execute SQL task [Integration Services]
ms.assetid: bebb2e8c-0410-43b2-ac2f-6fc80c8f2e9e
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 6be23e1a45f2b2ed0cc055c5032a72ffe2387399
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "62831766"
---
# <a name="execute-sql-task"></a>執行 SQL 工作
  「執行 SQL」工作會執行封裝中的 SQL 陳述式或預存程序。 工作可以包含逐次執行的單一 SQL 陳述式或多重 SQL 陳述式。 您可將執行 SQL 工作用於下列用途：  
  
-   截斷資料表或檢視，為插入資料做準備。  
  
-   建立、改變和卸除資料庫物件，例如資料表和檢視。  
  
-   將資料載入至事實 (Fact) 和維度 (Dimension) 資料表之前，先重建這些資料表。  
  
-   執行預存程序。 如果 SQL 陳述式叫用會從暫存資料表傳回結果的預存程序，請使用 WITH RESULT SETS 選項來定義結果集的中繼資料。  
  
-   將從查詢傳回的資料列集儲存到變數中。  
  
 執行 SQL 工作可搭配「Foreach 迴圈」容器和「For 迴圈」容器，用來執行多個 SQL 陳述式。 這些容器會實作封裝中重複的控制流程，並且可以重複執行「執行 SQL」工作。 例如，若使用「Foreach 迴圈」容器，封裝即可列舉資料夾中的檔案，並重複執行「執行 SQL」工作，以便執行每個檔案中儲存的 SQL 陳述式。  
  
## <a name="connecting-to-a-data-source"></a>連接到資料來源  
 執行 SQL 工作可使用不同類型的連接管理員，以連接到其執行 SQL 陳述式或預存程序的資料來源。 此工作可使用下表中列出的連接類型。  
  
|連線類型|[ODBC 來源編輯器]|  
|---------------------|------------------------|  
|EXCEL|[Excel 連線管理員](../connection-manager/excel-connection-manager.md)|  
|OLE DB|[OLE DB 連線管理員](../connection-manager/ole-db-connection-manager.md)|  
|ODBC|[ODBC 連線管理員](../connection-manager/odbc-connection-manager.md)|  
|ADO|[ADO 連線管理員](../connection-manager/ado-connection-manager.md)|  
|ADO.NET|[ADO.NET 連線管理員](../connection-manager/ado-net-connection-manager.md)|  
|SQLMOBILE|[SQL Server Compact Edition 連線管理員](../connection-manager/sql-server-compact-edition-connection-manager.md)|  
  
## <a name="creating-sql-statements"></a>建立 SQL 陳述式  
 此工作所使用的 SQL 陳述式來源，可以是包含陳述式的工作屬性、包含一個或多個陳述式的檔案連接，或者包含陳述式的變數名稱。 SQL 陳述式必須以來源資料庫管理系統 (DBMS) 的用語撰寫。 如需詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 查詢](../integration-services-ssis-queries.md)。  
  
 如果 SQL 陳述式儲存在檔案中，則工作會使用「檔案」連接管理員連接到該檔案。 如需相關資訊，請參閱 [File Connection Manager](../connection-manager/file-connection-manager.md)。  
  
 在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師中，您可以使用 [執行 SQL 工作編輯器]  對話方塊輸入 SQL 陳述式，或使用圖形化使用者介面 [查詢產生器]  建立 SQL 查詢。 如需詳細資訊，請參閱[執行 SQL 工作編輯器 &#40;一般頁面&#41;](../execute-sql-task-editor-general-page.md) 和[查詢產生器](../query-builder.md)。  
  
> [!NOTE]  
>  「執行 SQL」工作可能無法成功剖析在「執行 SQL」工作外部撰寫的有效 SQL 陳述式。  
  
> [!NOTE]  
>  「執行 SQL」工作會使用 `RecognizeAll` ParseMode 列舉值。 如需詳細資訊，請參閱 [ManagedBatchParser Namespace](https://go.microsoft.com/fwlink/?LinkId=223617)(ManagedBatchParser 命名空間)。  
  
## <a name="sending-multiple-statements-in-a-batch"></a>在批次中傳送多重陳述式  
 如果您在執行 SQL 工作中加入多個陳述式，可將它們組成群組，並在批次中執行。 若要表示批次結束，請使用 GO 命令。 兩個 GO 命令之間的所有 SQL 陳述式，都會在一個批次中傳送至要執行的 OLE DB 提供者。 SQL 命令可包含以 GO 命令分隔的多個批次。  
  
 您可分組到同一個批次中的 SQL 陳述式有其限制。 如需詳細資訊，請參閱 [陳述式的批次](../../relational-databases/native-client-odbc-queries/executing-statements/batches-of-statements.md)。  
  
 如果執行 SQL 工作執行一個批次的 SQL 陳述式，則下列規則會套用至該批次︰  
  
-   只有一個陳述式可傳回結果集，且它必須是批次中的第一個陳述式。  
  
-   如果結果集使用結果繫結，則查詢必須傳回相同數目的資料行。 如果查詢傳回不同數目的資料行，工作便會失敗。 不過，即使工作失敗，它執行的查詢 (例如，DELETE 或 INSERT 查詢) 仍會成功。  
  
-   如果結果繫結使用資料行名稱，則查詢必須傳回名稱與工作所使用之結果集名稱相同的資料行。 如果資料行遺失，工作便會失敗。  
  
-   如果工作使用參數繫結，則批次中所有查詢的參數數目和類型都必須相同。  
  
## <a name="running-parameterized-sql-commands"></a>執行參數化的 SQL 命令  
 SQL 陳述式和預存程序經常使用輸入參數、輸出參數以及傳回碼。 執行 SQL 工作支援 `Input`、`Output` 和 `ReturnValue` 等參數類型。 您可以使用 `Input` 類型當做輸入參數，使用 `Output` 當做輸出參數，並使用 `ReturnValue` 當做傳回碼。  
  
> [!NOTE]  
>  只有在資料提供者支援參數時，您才能在執行 SQL 工作中使用參數。  
  
 如需在「執行 SQL」工作中使用參數和傳回碼的資訊，請參閱 [執行 SQL 工作中的參數和傳回碼](execute-sql-task.md)。  
  
## <a name="specifying-a-result-set-type"></a>指定結果集類型  
 根據 SQL 命令的類型而定，結果集可能會，也可能不會傳回到執行 SQL 工作。 例如，SELECT 陳述式通常會傳回結果集，INSERT 陳述式則不會。 來自 SELECT 陳述式的結果集可包含零個資料列、一個資料列或多個資料列。 預存程序亦可傳回整數值，稱為傳回碼，以表示程序的執行狀態。 在此情況下，結果集是由單一資料列所組成。  
  
 如需在「執行 SQL」工作中從 SQL 命令擷取結果集的資訊，請參閱 [執行 SQL 工作中的結果集](../result-sets-in-the-execute-sql-task.md)。  
  
## <a name="troubleshooting-the-execute-sql-task"></a>疑難排解執行 SQL 工作  
 您可以記錄執行 SQL 工作對外部資料提供者執行的呼叫。 您可以使用這項記錄功能，疑難排解執行 SQL 工作所執行的 SQL 命令。 若要記錄「執行 SQL」工作對外部資料提供者執行的呼叫，請啟用封裝記錄，然後在封裝層級選取 [診斷]**** 事件。 如需詳細資訊，請參閱 [封裝執行的疑難排解工具](../troubleshooting/troubleshooting-tools-for-package-execution.md)。  
  
 有時 SQL 命令或預存程序會傳回多個結果集。 這些結果集不只包括屬於 `SELECT` 查詢結果的資料列集，也包括屬於 `RAISERROR` 或 `PRINT` 陳述式之錯誤結果的單一值。 工作是否忽略發生在第一個結果集之後之結果集中的錯誤，將取決於所使用的連接管理員類型：  
  
-   使用 OLE DB 和 ADO 連接管理員時，工作會忽略發生在第一個結果集之後的結果集。 因此，使用這些連接管理員時，如果錯誤不屬於第一個結果集的一部分，便會忽略 SQL 命令或預存程序所傳回的錯誤。  
  
-   使用 ODBC 和 ADO.NET 連接管理員時，工作不會忽略發生在第一個結果集之後的結果集。 使用這些連接管理員時，如果第一個結果集之外的結果集包含錯誤，工作將會失敗。  
  
### <a name="custom-log-entries"></a>自訂記錄項目  
 下表描述「執行 SQL」工作的自訂記錄項目。 如需詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 記錄](../performance/integration-services-ssis-logging.md)和[自訂訊息以進行記錄](../custom-messages-for-logging.md)。  
  
|記錄項目|描述|  
|---------------|-----------------|  
|`ExecuteSQLExecutingQuery`|提供 SQL 陳述式執行階段的相關資訊。 寫入記錄項目的時機包括在工作取得資料庫連接時、在工作開始準備 SQL 陳述式時，以及在 SQL 陳述式執行完成之後。 準備階段的記錄項目包含工作所使用的 SQL 陳述式。|  
  
## <a name="configuring-the-execute-sql-task"></a>設定執行 SQL 工作  
 您可以利用下列方式設定執行 SQL 工作：  
  
-   指定用來連接到資料庫的連接管理員類型。  
  
-   指定 SQL 陳述式傳回的結果集類型。  
  
-   指定 SQL 陳述式的逾時。  
  
-   指定 SQL 陳述式的來源。  
  
-   指示工作是否要略過 SQL 陳述式的準備階段。  
  
-   如果使用 ADO 連接類型，您必須指出 SQL 陳述式是否為預存程序。 如果是其他連接類型，此屬性為唯讀，且其值固定為 `false`。  
  
 您可以程式設計方式或透過「 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師」設定屬性。  
  
 如需有關可以在「 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師」中設定之屬性的詳細資訊，請按下列其中一個主題：  
  
-   [&#40;一般頁面&#41;執行 SQL 工作編輯器](../execute-sql-task-editor-general-page.md)  
  
-   [[執行 SQL 工作編輯器] &#40;[參數對應] 頁面&#41;](../execute-sql-task-editor-parameter-mapping-page.md)  
  
-   [[執行 SQL 工作編輯器] &#40;[結果集] 頁面&#41;](../execute-sql-task-editor-result-set-page.md)  
  
-   [運算式頁面](../expressions/expressions-page.md)  
  
 如需有關如何在「 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師」中設定這些屬性的詳細資訊，請按下列主題：  
  
-   [設定工作或容器的屬性](../set-the-properties-of-a-task-or-container.md)  
  
## <a name="configuring-the-execute-sql-task-programmatically"></a>以程式設計的方式設定執行 SQL 工作  
 如需有關以程式設計方式設定這些屬性的詳細資訊，請按下列主題：  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.ExecuteSQLTask.ExecuteSQLTask>  
  
## <a name="related-tasks"></a>相關工作  
  
-   [在執行 SQL 工作中將查詢參數對應至變數](../map-query-parameters-to-variables-in-an-execute-sql-task.md)  
  
-   [在執行 SQL 工作中將結果集對應至變數](../map-result-sets-to-variables-in-an-execute-sql-task.md)  
  
## <a name="related-content"></a>相關內容  
  
-   [執行 SQL 工作中的參數和傳回碼](execute-sql-task.md)  
  
-   [執行 SQL 工作中的結果集](../result-sets-in-the-execute-sql-task.md)  
  
-   [Transact-SQL 參考 &#40;Database Engine&#41;](/sql/t-sql/language-reference)  
  
-   mssqltips.com 上的部落格文章： [New Date and Time Functions in SQL Server 2012](https://go.microsoft.com/fwlink/?LinkId=239783)(SQL Server 2012 中的新日期和時間函數)  
  
  
