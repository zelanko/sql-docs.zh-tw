---
title: "資料分析工作 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: control-flow
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.dataprofilingtask.f1
helpviewer_keywords:
- Data Profiling task [Integration Services], about Data Profiling task
- data profiling
- profiling data
ms.assetid: 248ce233-4342-42c5-bf26-f4387ea152cf
caps.latest.revision: 32
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f5acdf3ae4f27685fce7aab56aab423044491ee1
ms.openlocfilehash: cb13596ddd01922f10632ccb3e1b801937c9941a
ms.contentlocale: zh-tw
ms.lasthandoff: 08/03/2017

---
# <a name="data-profiling-task"></a>資料分析工作
  資料分析工作會計算各種設定檔，協助您熟悉資料來源並在資料中識別必須修復的問題。  
  
 您可以使用 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝中的資料分析工作，分析儲存在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的資料並識別資料品質的潛在問題。  
  
> [!NOTE]  
>  本主題只會描述資料分析工作的功能和需求。 如需如何使用資料分析工作的逐步解說，請參閱 [資料分析工作和檢視器](../../integration-services/control-flow/data-profiling-task-and-viewer.md)一節。  
  
## <a name="requirements-and-limitations"></a>需求與限制  
 資料分析工作僅用於儲存在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中的資料。 此工作不適用於協力廠商或以檔案為基礎的資料來源。  
  
 此外，若要執行包含資料分析工作的封裝，您所使用的帳戶必須具備 tempdb 資料庫的讀取/寫入權限，包括 CREATE TABLE 權限。  
  
## <a name="data-profiler-viewer"></a>資料分析工具檢視器  
 使用工作來計算資料分析並將其儲存在檔案中後，您可以使用獨立的「資料設定檔檢視器」來檢閱設定檔輸出。 「資料設定檔檢視器」也支援向下鑽研功能，協助您了解在設定檔輸出中識別的資料品質問題。 如需詳細資訊，請參閱 [資料設定檔檢視器](../../integration-services/control-flow/data-profile-viewer.md)。  
  
> [!IMPORTANT]  
>  輸出檔可能包含您資料庫的相關敏感性資料，以及資料庫所包含的資料。 如需如何讓這個檔案更安全的相關建議，請參閱 [對封裝使用之檔案的存取權](../../integration-services/security/security-overview-integration-services.md#files)。  
>   
>  資料設定檔檢視器所提供的向下鑽研功能會傳送即時查詢給原始資料來源。  
  
## <a name="available-profiles"></a>可用的設定檔  
 資料分析工作可以計算八種不同的資料設定檔。 其中五種設定檔會分析個別的資料行，而剩餘的三種則會分析多個資料行或資料行和資料表之間的關聯性。  
  
 下列五個設定檔會分析個別的資料行。  
  
|分析個別資料行的設定檔|說明|  
|----------------------------------------------|-----------------|  
|資料行長度散發設定檔|報告選取之資料行中所有不同的字串值長度，以及該資料表中每個長度所代表之資料列的百分比。<br /><br /> 這個設定檔可協助您識別資料中的問題，例如無效的值。 例如，您分析了應該是兩個字元之美國州名代碼的資料行，並發現長度大於兩個字元的值。|  
|資料行 Null 比例設定檔|報告選取之資料行中 Null 值的百分比。<br /><br /> 這個設定檔可協助您識別資料中的問題，例如某個資料行中 Null 值的比例過高。 舉例來說，您分析了「郵遞區號」資料行並發現遺漏郵遞區號的百分比過高。|  
|資料行模式設定檔|報告一組規則運算式，其中涵蓋了字串資料行中值的指定百分比。<br /><br /> 這個設定檔可協助您識別資料中的問題，例如無效的字串。 這個設定檔也可以建議未來可用於驗證新值的規則運算式。 例如，[美國郵遞區號] 資料行的模式設定檔可能會產生規則運算式：\d{5}-\d{4}、\d{5} 及 \d{9}。 如果您看見其他規則運算式，表示資料可能包含無效或格式錯誤的值。|  
|資料行統計資料設定檔|報告數值資料行的最小值、最大值、平均和標準差，以及 **datetime** 資料行的最小值和最大值等統計資料。<br /><br /> 這個設定檔可協助您識別資料中的問題，例如無效的日期。 舉例來說，您分析了歷程記錄日期的資料行，並發現屬於未來的最大日期。|  
|資料行值散發設定檔|報告選取之資料行中的所有相異值，以及該資料表中每個值所代表之資料列的百分比。 也可以報告代表超過資料表中指定之資料列百分比的值。<br /><br /> 這個設定檔可協助您識別資料中的問題，例如某個資料行中相異值的數目不正確。 舉例來說，您分析了應該包含美國州名的資料行並發現超過 50 個相異值。|  
  
 下列三個設定檔會分析多個資料行或資料行和資料表之間的關聯性。  
  
|分析多個資料行的設定檔|說明|  
|--------------------------------------------|-----------------|  
|候選索引鍵設定檔|報告資料行或資料行集合是否為選取之資料表的索引鍵或近似索引鍵。<br /><br /> 這個設定檔也可協助您識別資料中的問題，例如潛在索引鍵資料行中重複的值。|  
|功能相依性設定檔|報告某個資料行 (相依資料行) 中的值相依於另一個資料行或資料行集合 (行列式資料行) 中之值的程度。<br /><br /> 這個設定檔也可協助您識別資料中的問題，例如無效的值。 舉例來說，您分析了包含「美國郵遞區號」之資料行與「美國州名」之資料行之間的相依性。 相同的郵遞區號應該永遠具有相同的州名，但是此設定檔卻發現了這個相依性的違規。|  
|值包含設定檔|計算兩個資料行或資料行集合之間值的重疊。 這個設定檔可以判斷資料行或資料行集合是否適合當做選取之資料表之間的外部索引鍵。<br /><br /> 這個設定檔也可協助您識別資料中的問題，例如無效的值。 舉例來說，您分析了 Sales 資料表的 ProductID 資料行，並發現此資料行包含在 Products 資料表之 ProductID 資料行中找不到的值。|  
  
## <a name="prerequisites-for-a-valid-profile"></a>有效設定檔的必要條件  
 除非您選取非空白的資料表和資料行，而且這些資料行包含不適用於設定檔的資料類型，否則設定檔無效。  
  
### <a name="valid-data-types"></a>有效的資料類型  
 有些可用的設定檔僅對某些資料類型有意義。 例如，針對包含數值或 **datetime** 值的資料行計算資料行模式設定檔是沒有意義的。 因此，這樣的設定檔無效。  
  
|設定檔|有效的資料類型*|  
|-------------|------------------------|  
|ColumnStatisticsProfile|數值類型或 **datetime** 類型 ( **datetime** 資料行沒有 **mean** 及 **stddev** ) 的資料行|  
|ColumnNullRatioProfile|所有資料行**|  
|ColumnValueDistributionProfile|**integer** 類型、 **char** 類型和 **datetime** 類型的資料行|  
|ColumnLengthDistributionProfile|**char** 類型的資料行|  
|ColumnPatternProfile|**char** 類型的資料行|  
|CandidateKeyProfile|**integer** 類型、 **char** 類型和 **datetime** 類型的資料行|  
|FunctionalDependencyProfile|**integer** 類型、 **char** 類型和 **datetime** 類型的資料行|  
|InclusionProfile|**integer** 類型、 **char** 類型和 **datetime** 類型的資料行|  
  
 \* 在有效資料類型的上一個資料表中， **integer**、 **char**、 **datetime**及 **numeric** 類型包括下列特定的資料類型：  
  
 整數類型包括 **bit**、 **tinyint**、 **smallint**、 **int**和 **bigint**。  
  
 字元類型包括 **char**、 **nchar**、 **varchar**及 **nvarchar** ，但不包括 **varchar(max)** 和 **nvarchar(max)**。  
  
 日期和時間類型包括 **datetime**、 **smalldatetime**和 **timestamp**。  
  
 數值類型包括 **integer** 類型 ( **bit**除外)、 **money**、 **smallmoney**、 **decimal**、 **float**、 **real**與 **numeric**。  
  
 \*\* **image**、 **text**、 **XML**、 **udt**及 **variant** 類型。  
  
### <a name="valid-tables-and-columns"></a>有效的資料表和資料行  
 如果資料表或資料行為空白，資料分析會採取下列動作：  
  
-   當選取的資料表或檢視為空白時，資料分析工作不會計算任何設定檔。  
  
-   當選取之資料行中的所有值為 Null 時，資料分析工作僅會計算資料行 Null 比例設定檔。 此工作不會計算資料行長度散發設定檔、資料行模式設定檔、資料行統計資料設定檔或資料行值散發設定檔。  
  
## <a name="features-of-the-data-profiling-task"></a>資料分析工作的功能  
 資料分析工作具有下列便利的組態選項：  
  
-   **萬用字元資料行**當您要設定設定檔要求時，此工作會接受 **(\*)** 萬用字元來取代資料行名稱。 這會簡化組態，而且更容易發現不熟悉之資料的特性。 當工作執行時，該工作會分析具有適當資料類型的每個資料行。  
  
-   **[快速分析]** You can select [快速分析] to configure the task quickly. [快速分析] 會使用所有預設的設定檔和預設值，分析資料表或檢視表。  
  
## <a name="custom-logging-messages-available-on-the-data-profililng-task"></a>資料分析工作上所提供的自訂記錄訊息  
 下表列出資料分析工作的自訂記錄項目。 如需詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 記錄](../../integration-services/performance/integration-services-ssis-logging.md)。  
  
|記錄項目|說明|  
|---------------|-----------------|  
|**DataProfilingTaskTrace**|提供有關此工作之狀態的描述性資訊。 訊息包括下列資訊：<br /><br /> 開始處理要求<br /><br /> 查詢開始<br /><br /> 查詢結束<br /><br /> 完成計算要求|  
  
## <a name="output-and-its-schema"></a>輸出及其結構描述  
 資料分析工作會將選取的設定檔輸出到根據 DataProfile.xsd 結構描述結構化的 XML。 您可以指定此 XML 輸出要以檔案或封裝變數儲存。 您可以在 [http://schemas.microsoft.com/sqlserver/2008/DataDebugger/](http://schemas.microsoft.com/sqlserver/2008/DataDebugger/)，線上檢視此結構描述。 您可以從網頁儲存結構描述的本機複本。 然後，您可以在 Microsoft [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 或其他結構描述編輯器、XML 編輯器，或「記事本」之類的文字編輯器中檢視結構描述的本機複本。  
  
 此資料品質資訊的結構描述對於下列事項可能很實用：  
  
-   在組織內部與跨組織交換資料品質資訊。  
  
-   建立搭配資料品質資訊使用的自訂工具。  
  
 在結構描述中，系統會將目標命名空間視為 [http://schemas.microsoft.com/sqlserver/2008/DataDebugger/](http://schemas.microsoft.com/sqlserver/2008/DataDebugger/)。  
  
## <a name="output-in-the-conditional-workflow-of-a-package"></a>封裝的條件式工作流程中的輸出  
 資料分析元件不包含內建功能，無法根據資料分析工作的輸出，在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝的工作流程中實作條件式邏輯。 不過，您可以利用最少量的程式設計，在指令碼工作中輕鬆加入這個邏輯。 此程式碼會根據 XML 輸出執行 XPath 查詢，然後以封裝變數儲存結果。 將指令碼工作連接到後續工作的優先順序條件約束可以使用運算式來判斷工作流程。 例如，指令碼工作會偵測到 Null 值在資料行中的百分比超出特定的臨界值。 此條件為 true 時，您可能想要先中斷封裝並解決問題，然後再繼續。  
  
## <a name="configuration-of-the-data-profiling-task"></a>設定資料分析工作  
 您可以使用 **[資料分析工作編輯器]**來設定資料分析工作。 此編輯器有兩個頁面：  
  
 [一般頁面](../../integration-services/control-flow/data-profiling-task-editor-general-page.md)  
 在 [一般] 頁面上，您可以指定輸出檔案或變數。 您也可以選取 **[快速分析]** ，利用預設值快速設定工作以計算設定檔。 如需詳細資訊，請參閱 [單一資料表快速分析表單 &#40;資料分析工作&#41;](../../integration-services/control-flow/single-table-quick-profile-form-data-profiling-task.md)。  
  
 [設定檔要求頁面](../../integration-services/control-flow/data-profiling-task-editor-profile-requests-page.md)  
 在 [設定檔要求] 頁面上，您可以指定資料來源，然後選取並設定您要計算的資料設定檔。 如需有關您可以設定之各種設定檔的詳細資訊，請參閱下列主題：  
  
-   [候選索引鍵設定檔要求選項 &#40;資料分析工作&#41;](../../integration-services/control-flow/candidate-key-profile-request-options-data-profiling-task.md)  
  
-   [資料行長度散發設定檔要求選項 &#40;資料分析工作&#41;](../../integration-services/control-flow/column-length-distribution-profile-request-options-data-profiling-task.md)  
  
-   [資料行 Null 比例設定檔要求選項 &#40;資料分析工作&#41;](../../integration-services/control-flow/column-null-ratio-profile-request-options-data-profiling-task.md)  
  
-   [資料行模式設定檔要求選項 &#40;資料分析工作&#41;](../../integration-services/control-flow/column-pattern-profile-request-options-data-profiling-task.md)  
  
-   [資料行統計資料設定檔要求選項 &#40;資料分析工作&#41;](../../integration-services/control-flow/column-statistics-profile-request-options-data-profiling-task.md)  
  
-   [資料行值散發設定檔要求選項 &#40;資料分析工作&#41;](../../integration-services/control-flow/column-value-distribution-profile-request-options-data-profiling-task.md)  
  
-   [功能相依性設定檔要求選項 &#40;資料分析工作&#41;](../../integration-services/control-flow/functional-dependency-profile-request-options-data-profiling-task.md)  
  
-   [值包含設定檔要求選項 &#40;資料分析工作&#41;](../../integration-services/control-flow/value-inclusion-profile-request-options-data-profiling-task.md)  
  
  

