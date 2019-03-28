---
title: sp_execute_external_script (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/14/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_execute_external_script_TSQL
- sys.sp_execute_external_script
- sys.sp_execute_external_script_TSQL
- sp_execute_external_script
dev_langs:
- TSQL
helpviewer_keywords:
- sp_execute_external_script
ms.assetid: de4e1fcd-0e1a-4af3-97ee-d1becc7f04df
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions||=azuresqldb-mi-current'
ms.openlocfilehash: f11b09d93510fe1da89abc1a723e7698f1fdd915
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/27/2019
ms.locfileid: "58531040"
---
# <a name="spexecuteexternalscript-transact-sql"></a>sp_execute_external_script (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

執行程序輸入引數提供的指令碼。 執行指令碼[擴充性架構](../../advanced-analytics/concepts/extensibility-framework.md)。 需要至少一個延伸模組的資料庫引擎上，指令碼必須支援的和已註冊的語言，撰寫：[**R**](../../advanced-analytics/concepts/extension-r.md)， [ **Python**](../../advanced-analytics/concepts/extension-python.md)，或[ **Java** （SQL Server 2019 中僅限預覽）](../../advanced-analytics/java/extension-java.md)。 

若要執行**sp_execute_external_script**，您必須先啟用外部指令碼使用陳述式， `sp_configure 'external scripts enabled', 1;`。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  

> [!Note]
> 機器學習 （R 和 Python） 和程式設計延伸模組會安裝 database engine 執行個體的附加元件。 支援特定的延伸模組是根據 SQL Server 版本而異。

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
## <a name="syntax"></a>語法

```
sp_execute_external_script   
    @language = N'language',   
    @script = N'script'  
    [ , @input_data_1 = N'input_data_1' ]   
    [ , @input_data_1_name = N'input_data_1_name' ]  
    [ , @input_data_1_order_by_columns = N'input_data_1_order_by_columns' ]    
    [ , @input_data_1_partition_by_columns = N'input_data_1_partition_by_columns' ]  
    [ , @output_data_1_name = N'output_data_1_name' ]  
    [ , @parallel = 0 | 1 ]  
    [ , @params = N'@parameter_name data_type [ OUT | OUTPUT ] [ ,...n ]' ] 
    [ , @parameter1 = 'value1' [ OUT | OUTPUT ] [ ,...n ] ]
```
::: moniker-end
::: moniker range=">=sql-server-2016 <=sql-server-2017||=sqlallproducts-allversions"
## <a name="syntax-for-2017-and-earlier"></a>2017 及更早版本的語法

```
sp_execute_external_script   
    @language = N'language',   
    @script = N'script'  
    [ , @input_data_1 = N'input_data_1' ]   
    [ , @input_data_1_name = N'input_data_1_name' ]  
    [ , @output_data_1_name = N'output_data_1_name' ]  
    [ , @parallel = 0 | 1 ]  
    [ , @params = N'@parameter_name data_type [ OUT | OUTPUT ] [ ,...n ]' ] 
    [ , @parameter1 = 'value1' [ OUT | OUTPUT ] [ ,...n ] ]
```
::: moniker-end

## <a name="arguments"></a>引數
 **@language** = N'*語言*'  
 表示指令碼語言。 *語言*已**sysname**。  根據您的 SQL Server 的版本，有效值為 R (SQL Server 2016 和更新版本)、 (SQL Server 2017 和更新版本)、 Python 和 Java （SQL Server 2019 預覽）。 
  
 **@script** = N'*指令碼*' 指定為常值或變數輸入的外部語言指令碼。 *指令碼*已**nvarchar （max)**。  

`[ @input_data_1 =  N'input_data_1' ]` 指定的表單中的外部指令碼所使用的輸入的資料[!INCLUDE[tsql](../../includes/tsql-md.md)]查詢。 資料類型*input_data_1*是**nvarchar （max)**。

`[ @input_data_1_name = N'input_data_1_name' ]` 指定用來代表查詢所定義的變數名稱@input_data_1。 在 外部指令碼變數的資料類型會因語言而定。 如果 R 輸入的變數會是資料框架。 在 Python 中，輸入必須是表格式。 *input_data_1_name*已**sysname**。  預設值是*InputDataSet*。  

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
`[ @input_data_1_order_by_columns = N'input_data_1_order_by_columns' ]` 僅適用於 SQL Server 2019，並用來建立每個磁碟分割模型。 指定用來排序結果集資料行的名稱，例如依產品名稱。 在 外部指令碼變數的資料類型會因語言而定。 如果 R 輸入的變數會是資料框架。 在 Python 中，輸入必須是表格式。

`[ @input_data_1_partition_by_columns = N'input_data_1_partition_by_columns' ]` 僅適用於 SQL Server 2019，並用來建立每個磁碟分割模型。 指定用來分割資料，例如地理區域或日期資料行的名稱。 在 外部指令碼變數的資料類型會因語言而定。 如果 R 輸入的變數會是資料框架。 在 Python 中，輸入必須是表格式。 
::: moniker-end

`[ @output_data_1_name =  N'output_data_1_name' ]` 包含要傳回之資料的外部指令碼中指定的變數名稱[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]預存程序呼叫完成時。 在 外部指令碼變數的資料類型會因語言而定。 針對 R，輸出必須是資料框架。 對於 Python，輸出必須是 pandas 資料框架。 *output_data_1_name*已**sysname**。  預設值是*OutputDataSet*。  

`[ @parallel = 0 | 1 ]` 藉由設定啟用平行執行 R 指令碼`@parallel`參數設為 1。 此參數的預設值為 0 (沒有 parallelism)。 如果`@parallel = 1`和輸出串流直接至用戶端電腦，則`WITH RESULT SETS`子句是必要的而且必須指定輸出結構描述。  

 + 針對未使用 RevoScaleR 函式，使用 R 指令碼`@parallel`參數可以是有幫助處理大型資料集，假設指令碼可透過極簡方式平行處理。 例如，當使用 R`predict`函式使用的模型，來產生新預測，請將設定`@parallel = 1`以做為查詢引擎的提示。 如果可以平行處理查詢，資料列會根據散發**MAXDOP**設定。  
  
 + 使用 RevoScaleR 函數的 R 指令碼，平行處理會自動處理，您不應指定`@parallel = 1`要**sp_execute_external_script**呼叫。  
  
`[ @params = N'@parameter_name data_type [ OUT | OUTPUT ] [ ,...n ]' ]` 外部指令碼中使用的輸入的參數宣告的清單。  
  
`[ @parameter1 = 'value1' [ OUT | OUTPUT ] [ ,...n ] ]` 外部指令碼所使用的輸入參數的值清單。  

## <a name="remarks"></a>備註

> [!IMPORTANT]
> 查詢樹狀結構由控制[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，使用者無法執行查詢的任意作業。 

使用**sp_execute_external_script**執行支援的語言撰寫的指令碼。 目前，支援的語言是 SQL Server 2016 R Services，以及 Python 和 R 適用的 SQL Server 2017 Machine Learning 服務的 R。 

根據預設，此預存程序所傳回的結果集是未命名的資料行的輸出。 在指令碼內使用的資料行名稱是本機指令碼環境，並不會反映在輸出的結果集。 若要命名結果集資料行，使用`WITH RESULT SET`子句[ `EXECUTE` ](../../t-sql/language-elements/execute-transact-sql.md)。
  
 除了傳回的結果集，您可以傳回純量值[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用 OUTPUT 參數。 下列範例示範使用輸出參數傳回序列化的 R 模型來做為指令碼的輸入：  
  
您可以控制藉由設定外部資源集區的 外部指令碼所使用的資源。 如需詳細資訊，請參閱 [CREATE EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-resource-pool-transact-sql.md)。 工作負載的相關資訊可以取自 resource governor 目錄檢視、 DMV 和計數器。 如需詳細資訊，請參閱[Resource Governor 目錄檢視&#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/resource-governor-catalog-views-transact-sql.md)， [Resource Governor 相關動態管理檢視&#40;-&#41;](../../relational-databases/system-dynamic-management-views/resource-governor-related-dynamic-management-views-transact-sql.md)，以及[SQL Server 的 External Scripts 物件](../../relational-databases/performance-monitor/sql-server-external-scripts-object.md)。  

### <a name="monitor-script-execution"></a>監視指令碼執行

使用的監視指令碼執行[sys.dm_external_script_requests](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-requests.md)並[sys.dm_external_script_execution_stats](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-execution-stats.md)。 

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
### <a name="parameters-for-partition-modeling"></a>磁碟分割模型的參數

 在 SQL Server 2019，，您也可以在目前在公開預覽，設定兩個額外的參數可讓資料分割的資料，其中資料分割根據一個或多個資料行提供自然地將資料集分成邏輯分割區建立及使用模型僅指令碼執行期間。 年齡、 性別、 地區、 日期或時間，包含重複值的資料行是讓資料分割的資料集的一些範例。
 
 兩個參數**input_data_1_partition_by_columns**並**input_data_1_order_by_columns**，第二個參數用以排序結果集。 將參數傳遞做為輸入`sp_execute_external_script`外部指令碼中執行一次的每個資料分割。 如需詳細資訊和範例，請參閱[教學課程：建立分割區為基礎的模型](https://docs.microsoft.com/sql/advanced-analytics/tutorials/r-tutorial-create-models-per-partition.md)。

 您可以以平行方式執行指令碼，藉由指定`@parallel=1`。 如果輸入的查詢可以平行處理，您應該設定`@parallel=1`做為您的引數的一部分`sp_execute_external_script`。 根據預設，查詢最佳化工具運作`@parallel=1`超過 256 個資料列，但如果您想要明確地處理此資料表上還會使用這個指令碼包含基於示範用途的參數。

 > [!Tip]
> 您可以使用訓練 workoads`@parallel`任何任意的訓練指令碼，甚至是使用非 Microsoft rx 演算法。 通常，只有 RevoScaleR 演算法 （具有 rx 前置詞） 會提供 SQL Server 中的定型案例中的平行處理原則。 但是，與 SQL Server vNext 的新參數，您可以平行處理呼叫函式不是明確地使用這項功能設計的指令碼。
::: moniker-end

### <a name="streaming-execution-for-r-and-python-scripts"></a>如需 R 和 Python 指令碼的資料流執行  

資料流可讓 R 或 Python 指令碼來處理記憶體內可容納更多的資料。 若要控制的串流處理期間傳遞的資料列數目，指定參數的整數值`@r_rowsPerRead`在`@params`集合。  例如，如果您要訓練一個模型來使用非常廣泛的資料，您無法將值調整為讀取較少的資料列，以確保所有資料列都可以傳送資料的一個區塊中。 您也可以使用這個參數，來管理正在讀取和處理一次，以降低伺服器效能問題的資料列數目。 
  
這兩個`@r_rowsPerRead`參數進行串流處理和`@parallel`引數視為提示。 要套用提示，您必須能夠產生 SQL 的查詢計畫，其中包含平行處理。 如果這不可行，就無法啟用平行處理。  
  
> [!NOTE]  
>  只有在 Enterprise Edition 支援資料流和平行處理。 您可以在 Standard Edition 中的查詢中包含參數，而不會引發錯誤，但參數有任何效果和在單一處理序中執行的 R 指令碼。  
  
## <a name="restrictions"></a>限制  


### <a name="data-types"></a>資料類型

使用中，輸入的查詢或參數時，不支援下列資料類型**sp_execute_external_script**程序，並傳回不支援的類型錯誤。  

因應措施， **CAST**資料行或值中的支援型別[!INCLUDE[tsql](../../includes/tsql-md.md)]再將它傳送至外部指令碼。  
  
-   **cursor**  
  
-   **timestamp**  
  
-   **datetime2**， **datetimeoffset**，**時間**  
  
-   **sql_variant**  
  
-   **文字**，**映像**  
  
-   **xml**  
  
-   **hierarchyid**，**幾何**，**地理位置**  
  
-   CLR 使用者定義型別

一般情況下，任何結果集，無法對應至[!INCLUDE[tsql](../../includes/tsql-md.md)]資料型別，會輸出為 NULL。  

### <a name="restrictions-specific-to-r"></a>特定的限制

如果輸入包含**datetime**在 R 中，不符合允許的值範圍的值，值會轉換成**NA**。 這是必要的因為[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]允許較大範圍的值超過支援的 R 語言。

浮點數的值 (例如`+Inf`， `-Inf`， `NaN`) 中不支援[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]即使這兩種語言使用 IEEE 754。 目前的行為只會將值傳送至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]直接; 如此一來中的 SQL 用戶端[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]擲回錯誤。 因此，這些值會轉換成**NULL**。

## <a name="permissions"></a>Permissions

需要**EXECUTE ANY EXTERNAL SCRIPT**資料庫權限。  

## <a name="examples"></a>範例

本章節包含如何使用這個預存程序，來執行 R 或 Python 指令碼使用範例[!INCLUDE[tsql](../../includes/tsql-md.md)]。

### <a name="a-return-an-r-data-set-to-sql-server"></a>A. 返回 SQL Server 中 R 的資料集  

下列範例會建立使用預存程序**sp_execute_external_script**傳回隨附於 R 鳶尾花資料集[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  

```sql
DROP PROC IF EXISTS get_iris_dataset;  
go  
CREATE PROC get_iris_dataset
AS  
BEGIN  
 EXEC   sp_execute_external_script  
       @language = N'R'  
     , @script = N'iris_data <- iris;'
     , @input_data_1 = N''  
     , @output_data_1_name = N'iris_data'
     WITH RESULT SETS (("Sepal.Length" float not null,   
           "Sepal.Width" float not null,  
        "Petal.Length" float not null,   
        "Petal.Width" float not null, "Species" varchar(100)));  
END;
GO
```

### <a name="b-generate-an-r-model-based-on-data-from-sql-server"></a>B. 產生的資料是從 SQL Server 的 R 模型  

下列範例會建立使用預存程序**sp_execute_external_script**產生鳶尾花模型，並傳回模型[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  

> [!NOTE]
>  這個範例需要 e1071 套件的預先安裝。 如需詳細資訊，請參閱 < [SQL Server 上安裝其他 R 套件](../../advanced-analytics/r/install-additional-r-packages-on-sql-server.md)。

```sql
DROP PROC IF EXISTS generate_iris_model;
GO
CREATE PROC generate_iris_model
AS
BEGIN
 EXEC sp_execute_external_script  
      @language = N'R'  
     , @script = N'  
          library(e1071);  
          irismodel <-naiveBayes(iris_data[,1:4], iris_data[,5]);  
          trained_model <- data.frame(payload = as.raw(serialize(irismodel, connection=NULL)));  
'  
     , @input_data_1 = N'select "Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width", "Species" from iris_data'  
     , @input_data_1_name = N'iris_data'  
     , @output_data_1_name = N'trained_model'  
    WITH RESULT SETS ((model varbinary(max)));  
END;
GO
```

若要使用 Python 產生類似的模型，您需要將語言識別項從 `@language=N'R'` 變更為 `@language = N'Python'`，並對 `@script` 引數進行必要的修改。 否則，所有參數都會跟 R 的運作方式相同。

### <a name="c-create-a-python-model-and-generate-scores-from-it"></a>C. 建立 Python 模型，並從中產生分數

這個範例示範如何使用 sp\_execute\_external\_ 指令碼來產生簡單 Python 模型的分數。 

```sql
CREATE PROCEDURE [dbo].[py_generate_customer_scores]
AS
BEGIN

-- Input query to generate the customer data
DECLARE @input_query NVARCHAR(MAX) = N'SELECT customer, orders, items, cost FROM dbo.Sales.Orders'

EXEC sp_execute_external_script @language = N'Python', @script = N'
import pandas as pd
from sklearn.cluster import KMeans

# Get data from input query
customer_data = my_input_data

# Define the model
n_clusters = 4
est = KMeans(n_clusters=n_clusters, random_state=111).fit(customer_data[["orders","items","cost"]])
clusters = est.labels_
customer_data["cluster"] = clusters

OutputDataSet = customer_data
'
, @input_data_1 = @input_query
, @input_data_1_name = N'my_input_data'
WITH RESULT SETS (("CustomerID" int, "Orders" float,"Items" float,"Cost" float,"ClusterResult" float));
END;
GO
```

使用 Python 程式碼中的資料行標題不會輸出到 SQL Server;因此，使用與結果的陳述式來指定要使用的 sql 資料類型與資料行名稱。

若要計分，您也可以使用原生 [PREDICT](../../t-sql/queries/predict-transact-sql.md) 函式，其會避免呼叫 Python 或 R 執行階段，因此一般來說速度更快。

## <a name="see-also"></a>另請參閱

 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Python 程式庫和資料類型](../../advanced-analytics/python/python-libraries-and-data-types.md)  
 [R 程式庫和 R 資料類型](../../advanced-analytics/r/r-libraries-and-data-types.md)  
 [SQL Server R Services](../../advanced-analytics/r/sql-server-r-services.md)   
 [SQL Server Machine Learning 服務的已知的問題](../../advanced-analytics/known-issues-for-sql-server-machine-learning-services.md)   
 [CREATE EXTERNAL LIBRARY &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-library-transact-sql.md)  
 [sp_prepare &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-prepare-transact-sql.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [啟用外部指令碼伺服器設定選項](../../database-engine/configure-windows/external-scripts-enabled-server-configuration-option.md)   
 [SERVERPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/serverproperty-transact-sql.md)   
 [SQL Server 的 External Scripts 物件](../../relational-databases/performance-monitor/sql-server-external-scripts-object.md)  
[sys.dm_external_script_requests](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-requests.md)  
[sys.dm_external_script_execution_stats](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-execution-stats.md) 
