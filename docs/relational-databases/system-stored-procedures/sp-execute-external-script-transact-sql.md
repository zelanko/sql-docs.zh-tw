---
title: sp_execute_external_script (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 07/14/2018
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
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
caps.latest.revision: 34
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions||=azuresqldb-mi-current'
ms.openlocfilehash: 5e866f5a9856fe1308bc5233432e053b18d207f7
ms.sourcegitcommit: e4e9f02b5c14f3bb66e19dec98f38c012275b92c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/28/2018
ms.locfileid: "43118316"
---
# <a name="spexecuteexternalscript-transact-sql"></a>sp_execute_external_script & Amp;#40;transact-SQL&AMP;#41;

[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  執行與位於外部位置引數提供的指令碼。 必須在支援的和已註冊的語言 （R 或 Python） 中撰寫指令碼。 若要執行**sp_execute_external_script**，您必須先啟用外部指令碼使用陳述式， `sp_configure 'external scripts enabled', 1;`。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法

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

## <a name="arguments"></a>引數
 \@語言 = N'*語言*'  
 表示指令碼語言。 *語言*已**sysname**。  

 有效值`Python`或`R`。 
  
 \@指令碼 = N'*指令碼*'  
 指定為常值或變數輸入的外部語言指令碼。 *指令碼*已**nvarchar （max)**。  
  
 [ \@input_data_1_name = N'*input_data_1_name*']  
 指定用來代表查詢所定義的變數名稱\@input_data_1。 在 外部指令碼變數的資料類型會因語言而定。 如果 R 輸入的變數會是資料框架。 在 Python 中，輸入必須是表格式。 *input_data_1_name*已**sysname**。  
  
 預設值是`InputDataSet`。  
  
 [ \@input_data_1 = N'*input_data_1*']  
 指定的表單中的外部指令碼所使用的輸入的資料[!INCLUDE[tsql](../../includes/tsql-md.md)]查詢。 資料類型*input_data_1*是**nvarchar （max)**。
  
 [ \@output_data_1_name = N'*output_data_1_name*']  
 包含要傳回之資料的外部指令碼中指定的變數名稱[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]預存程序呼叫完成時。 在 外部指令碼變數的資料類型會因語言而定。 針對 R，輸出必須是資料框架。 對於 Python，輸出必須是 pandas 資料框架。 *output_data_1_name*已**sysname**。  
  
 預設值為"OutputDataSet 」。  
  
 [\@平行 = 0 | 1]

 藉由設定啟用平行執行 R 指令碼`@parallel`參數設為 1。 此參數的預設值為 0 (沒有 parallelism)。  
  
 針對未使用 RevoScaleR 函式，使用 R 指令碼`@parallel`參數可以是有幫助處理大型資料集，假設指令碼可透過極簡方式平行處理。 例如，當使用 R`predict`函式使用的模型，來產生新預測，請將設定`@parallel = 1`以做為查詢引擎的提示。 如果可以平行處理查詢，資料列會根據散發**MAXDOP**設定。  
  
 如果`@parallel = 1`和輸出串流直接至用戶端電腦，則`WITH RESULTS SETS`子句是必要的而且必須指定輸出結構描述。  
  
 使用 RevoScaleR 函數的 R 指令碼，平行處理會自動處理，您不應指定`@parallel = 1`要**sp_execute_external_script**呼叫。  
  
 [ \@params = N'*\@parameter_name data_type* [OUT |輸出] [，......n]']  
 外部指令碼中使用的輸入的參數宣告的清單。  
  
 [ \@parameter1 = '*value1*' [OUT |輸出] [，......n]]  

 外部指令碼所使用的輸入參數的值清單。  

## <a name="remarks"></a>備註

使用**sp_execute_external_script**執行支援的語言撰寫的指令碼。 目前，支援的語言是 SQL Server 2016 和 Python 的 R 和 R 的 SQL Server 2017。 

> [!IMPORTANT]
> 查詢樹狀結構由控制[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，使用者無法執行查詢的任意作業。 

根據預設，此預存程序所傳回的結果集是未命名的資料行的輸出。 在指令碼內使用的資料行名稱是本機指令碼環境，並不會反映在輸出的結果集。 若要命名結果集資料行，使用`WITH RESULTS SET`子句[ `EXECUTE` ](../../t-sql/language-elements/execute-transact-sql.md)。
  
 除了傳回的結果集，您可以傳回純量值[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用 OUTPUT 參數。 下列範例示範使用輸出參數傳回序列化的 R 模型來做為指令碼的輸入：  

在  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]與一起安裝的伺服器元件所組成[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，和一組工作站工具和資料科學家連接至的高效能環境的連線程式庫[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 您必須安裝的機器學習服務期間，元件[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]以啟用外部指令碼執行安裝程式。 如需詳細資訊，請參閱 <<c0> [ 設定 SQL Server Machine Learning 服務](../../advanced-analytics/r/set-up-sql-server-r-services-in-database.md)。  
  
您可以控制藉由設定外部資源集區的 外部指令碼所使用的資源。 如需詳細資訊，請參閱 [CREATE EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-resource-pool-transact-sql.md)。 工作負載的相關資訊可以取自 resource governor 目錄檢視、 DMV 和計數器。 如需詳細資訊，請參閱[Resource Governor 目錄檢視&#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/resource-governor-catalog-views-transact-sql.md)， [Resource Governor 相關動態管理檢視&#40;-&#41;](../../relational-databases/system-dynamic-management-views/resource-governor-related-dynamic-management-views-transact-sql.md)，以及[SQL Server 的 External Scripts 物件](../../relational-databases/performance-monitor/sql-server-external-scripts-object.md)。  

使用的監視指令碼執行[sys.dm_external_script_requests](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-requests.md)並[sys.dm_external_script_execution_stats](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-execution-stats.md)。 

## <a name="streaming-execution-for-r-and-python-scripts"></a>如需 R 和 Python 指令碼的資料流執行  

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

由於系統不會將 Python 程式碼中使用的資料行標題輸出至 SQL Server，因此請使用 WITH RESULTS 陳述式指定要讓 SQL 使用的資料行名稱與資料類型。

若要計分，您也可以使用原生 [PREDICT](../../t-sql/queries/predict-transact-sql.md) 函式，其會避免呼叫 Python 或 R 執行階段，因此一般來說速度更快。

## <a name="see-also"></a>另請參閱

 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Python 程式庫和資料類型](../../advanced-analytics/python/python-libraries-and-data-types.md)  
 [R 程式庫和 R 資料類型](../../advanced-analytics/r/r-libraries-and-data-types.md)  
 [SQL Server R Services](../../advanced-analytics/r/sql-server-r-services.md)   
 [SQL Server Machine Learning 服務的已知的問題](../../advanced-analytics/known-issues-for-sql-server-machine-learning-services.md)   
 [建立外部程式庫&#40;Transact SQL&#41;](../../t-sql/statements/create-external-library-transact-sql.md)  
 [sp_prepare &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-prepare-transact-sql.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [啟用外部指令碼伺服器設定選項](../../database-engine/configure-windows/external-scripts-enabled-server-configuration-option.md)   
 [SERVERPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/serverproperty-transact-sql.md)   
 [SQL Server 的 External Scripts 物件](../../relational-databases/performance-monitor/sql-server-external-scripts-object.md)  
[sys.dm_external_script_requests](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-requests.md)  
[sys.dm_external_script_execution_stats](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-execution-stats.md) 
