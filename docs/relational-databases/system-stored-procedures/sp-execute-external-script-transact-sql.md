---
title: "sp_execute_external_script (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 01/22/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_execute_external_script_TSQL
- sys.sp_execute_external_script
- sys.sp_execute_external_script_TSQL
- sp_execute_external_script
dev_langs: TSQL
helpviewer_keywords: sp_execute_external_script
ms.assetid: de4e1fcd-0e1a-4af3-97ee-d1becc7f04df
caps.latest.revision: "34"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 283db0150613d9d956cf5b0ec6b6fd295bc4444b
ms.sourcegitcommit: d7dcbcebbf416298f838a39dd5de6a46ca9f77aa
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/23/2018
---
# <a name="spexecuteexternalscript-transact-sql"></a>sp_execute_external_script (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  執行做為在外部位置的引數提供的指令碼。 必須在支援並註冊的語言中撰寫指令碼。 若要執行**sp_execute_external_script**，您必須先啟用外部指令碼使用陳述式， `sp_configure 'external scripts enabled', 1;`。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法

```
sp_execute_external_script   
    @language = N'language,   
    @script = N'script'  
    [ , @input_data_1 = N'input_data_1' ]   
    [ , @input_data_1_name = N'input_data_1_name' ]   
    [ , @output_data_1_name = N'output_data_1_name' ]  
    [ , @parallel = 0 | 1 ]  
    [ , @params = N'@parameter_name data_type [ OUT | OUTPUT ] [ ,...n ]' ] 
    [ , @parameter1 = 'value1' [ OUT | OUTPUT ] [ ,...n ] ]
```

## <a name="arguments"></a>引數
 @language= N'*語言*'  
 表示指令碼語言。 *語言*是**sysname**。  

 有效值為`Python`或`R`。 
  
 @script = N'*script*'  
 指定為常值或變數的輸入的外部語言指令碼。 *指令碼*是**nvarchar （max)**。  
  
 [ @input_data_1_name = N'*input_data_1_name*' ]  
 指定用來表示查詢所定義的變數名稱@input_data_1。 外部指令碼中變數的資料類型會因語言而定。 發生 R，則輸入的變數是資料框架。 在 [Python]，輸入必須是表格式。 *input_data_1_name*是**sysname**。  
  
 預設值是`InputDataSet`。  
  
 [ @input_data_1 =  N'*input_data_1*' ]  
 指定的表單中的外部指令碼所使用的輸入的資料[!INCLUDE[tsql](../../includes/tsql-md.md)]查詢。 資料型別*input_data_1*是**nvarchar （max)**。
  
 [ @output_data_1_name =  N'*output_data_1_name*' ]  
 包含要傳回之資料的外部指令碼中指定的變數名稱[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]預存程序呼叫完成時。 外部指令碼中變數的資料類型會因語言而定。 的輸出必須是資料框架。 Python，輸出必須熊資料框架。 *output_data_1_name*是**sysname**。  
  
 預設值為"OutputDataSet"。  
  
 [ @parallel = 0 | 1] 設定以啟用 R 指令碼的平行執行`@parallel`參數設為 1。 此參數的預設值為 0 (沒有 parallelism)。  
  
 請勿使用 RevoScaleR 函式，使用的 R 指令碼`@parallel`參數可以是有幫助處理大型資料集，假設兩者平行指令碼。 例如，當使用 R`predict`函式產生新的預測，請將設定模型`@parallel = 1`做為提示給查詢引擎。 如果可平行處理查詢，資料列散發根據**MAXDOP**設定。  
  
 如果`@parallel = 1`和輸出串流直接至用戶端電腦，然後在`WITH RESULTS SETS`子句是必要的而且必須指定輸出結構描述。  
  
 使用 RevoScaleR 函式的 R 指令碼，平行處理會自動處理，您不應該指定`@parallel = 1`至**sp_execute_external_script**呼叫。  
  
 [ @params = N' *@parameter_name data_type* [出 |輸出] [，.....n]']  
 外部指令碼中使用的輸入的參數宣告的清單。  
  
 [ @parameter1 = '*value1*' [出 |輸出] [，.....n]]  
 外部指令碼所使用的輸入參數的值清單。  

## <a name="remarks"></a>備註

使用**sp_execute_external_script**執行支援的語言撰寫的指令碼。 目前支援的語言是針對 SQL Server 2016 中，並將 Python 的 R 和 SQL Server 2017 的 R。 

> [!IMPORTANT]
> 查詢樹狀結構由[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用者無法執行的查詢上的任意作業。 

根據預設，這個預存程序所傳回的結果集是使用未命名資料行的輸出。 在指令碼內使用的資料行名稱的本機指令碼環境，而且不會反映在輸出的結果集。 若要將結果集資料行，使用`WITH RESULTS SET`子句[ `EXECUTE` ](../../t-sql/language-elements/execute-transact-sql.md)。
  
 除了傳回的結果集，您可以傳回純量值[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用輸出參數。 下列範例示範如何使用輸出參數傳回做為指令碼的輸入使用的序列化的 R 模型的：  

在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]與一起安裝的伺服器元件所組成[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，和一組工作站工具和資料科學家連接至的高效能環境的連線程式庫[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 您必須安裝在機器學習期間，元件[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]以啟用外部指令碼執行安裝程式。 如需詳細資訊，請參閱[設定 SQL Server 機器學習服務](../../advanced-analytics/r/set-up-sql-server-r-services-in-database.md)。  
  
您可以控制藉由設定外部資源集區的 外部指令碼所使用的資源。 如需詳細資訊，請參閱 [CREATE EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-resource-pool-transact-sql.md)。 工作負載的相關資訊可從資源管理員目錄檢視、 DMV 和計數器取得。 如需詳細資訊，請參閱[資源管理員目錄檢視 &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/resource-governor-catalog-views-transact-sql.md)，[資源管理員相關的動態管理檢視 &#40;TRANSACT-SQL &#41;](../../relational-databases/system-dynamic-management-views/resource-governor-related-dynamic-management-views-transact-sql.md)，和[SQL Server，外部指令碼物件](../../relational-databases/performance-monitor/sql-server-external-scripts-object.md)。  

監視指令碼執行使用[sys.dm_external_script_requests](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-requests.md)和[sys.dm_external_script_execution_stats](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-execution-stats.md)。 

## <a name="streaming-execution-for-r-and-python-scripts"></a>資料流執行 R 和 Python 指令碼  

資料流可讓處理更多資料，比可以納入記憶體中的 R 或 Python 指令碼。 若要控制的串流處理期間傳遞的資料列數目，指定一個整數值的參數，`@r_rowsPerRead`中`@params`集合。  例如，如果您定型的模型，會使用非常廣泛的資料，您無法調整要讀取較少的資料列，以確保所有資料列，可傳送資料的一個區塊中的值。 您也可以使用這個參數來管理正在讀取和處理一次，以降低伺服器效能問題的資料列數目。 
  
這兩個`@r_rowsPerRead`串流處理的參數和`@parallel`引數視為提示。 要套用提示，就能產生 SQL 的查詢計畫，其中包含平行處理。 如果不可行，就無法啟用平行處理。  
  
> [!NOTE]  
>  Enterprise 版本中才支援資料流和平行處理。 您可以在 Standard Edition 中的查詢中包含參數，而不會引發錯誤，但參數有任何效果和在單一處理序中執行 R 指令碼。  
  
## <a name="restrictions"></a>限制  


### <a name="data-types"></a>資料類型

輸入的查詢或參數中使用時，不支援下列資料類型`sp_execute_external_script`程序，並傳回不支援的類型錯誤。  

因應措施，**轉換**資料行或值，以支援的型別中[!INCLUDE[tsql](../../includes/tsql-md.md)]再將它傳送至外部指令碼。  
  
-   **cursor**  
  
-   **timestamp**  
  
-   **datetime2**， **datetimeoffset**，**時間**  
  
-   **sql_variant**  
  
-   **文字**，**映像**  
  
-   **xml**  
  
-   **hierarchyid**，**幾何**，**地理位置**  
  
-   CLR 使用者定義型別

一般情況下，任何的結果無法對應至[!INCLUDE[tsql](../../includes/tsql-md.md)]資料型別，會輸出為 NULL。  

### <a name="restrictions-specific-to-r"></a>R 的特定限制

如果輸入包含**datetime**不適合的值所允許的範圍中 R 的值，值會轉換成**NA**。 這是必要的因為[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]允許較大範圍的值超過支援的 R 語言。

浮點數的值 (例如， `+Inf`， `-Inf`， `NaN`) 中不支援[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]即使這兩種語言使用 IEEE 754。 目前的行為只會將值傳送至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]直接; 如此一來中的 SQL 用戶端[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]擲回錯誤。 因此，這些值會轉換成**NULL**。

## <a name="permissions"></a>Permissions

需要**EXECUTE ANY EXTERNAL SCRIPT**資料庫權限。  

## <a name="examples"></a>範例

此章節包含如何使用這個預存程序，執行 R 或 Python 指令碼的範例[!INCLUDE[tsql](../../includes/tsql-md.md)]。

### <a name="a-return-an-r-data-set-to-sql-server"></a>A. 返回 SQL Server 中的 R 資料集  

下列範例會建立使用的預存程序**sp_execute_external_script**傳回隨附 R 以光圈資料集[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  

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

### <a name="b-generate-an-r-model-based-on-data-from-sql-server"></a>B. 產生的 SQL Server 資料的 R 模型  

下列範例會建立使用的預存程序**sp_execute_external_script**來產生光圈模型，並傳回模型[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  

> [!NOTE]
>  這個範例需要 e1071 套件的預先安裝。 如需詳細資訊，請參閱[SQL Server 上安裝其他的 R 封裝](../../advanced-analytics/r/install-additional-r-packages-on-sql-server.md)。

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

若要產生類似的模型使用 Python，您需要變更語言識別項從`@language=N'R'`至`@language = N'Python'`，並進行必要的修改`@script`引數。 否則，所有參數函都式一樣。

### <a name="c-create-a-python-model-and-generate-scores-from-it"></a>C. 建立 Python 模型，並從其中產生分數

這個範例示範如何使用預存程序來\_執行\_外部\_指令碼來產生簡單的 Python 模型的分數。 

```sql
CREATE PROCEDURE [dbo].[py_generate_customer_scores]
AS
BEGIN

## Input query to generate the customer data
DECLARE @input_query NVARCHAR(MAX) = N'SELECT customer, orders, items, cost FROM dbo.Sales.Orders`

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

Python 程式碼中使用的資料行標題不會輸出到 SQL Server;因此，使用與結果陳述式，指定要使用的 sql 資料類型與資料行名稱。

計分，您也可以使用原生[預測](../../t-sql/queries/predict-transact-sql.md)函式，也就是通常會更快，因為它可避免呼叫 Python 或 R 執行階段。

## <a name="see-also"></a>另請參閱

 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Python 程式庫和資料類型](../../advanced-analytics/python/python-libraries-and-data-types.md)  
 [R 程式庫和 R 資料類型](../../advanced-analytics/r/r-libraries-and-data-types.md)  
 [SQL Server R Services](../../advanced-analytics/r/sql-server-r-services.md)   
 [SQL Server 機器學習服務的已知的問題](../../advanced-analytics/known-issues-for-sql-server-machine-learning-services.md)   
 [建立外部程式庫 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/create-external-library-transact-sql.md)  
 [sp_prepare &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-prepare-transact-sql.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [啟用外部指令碼伺服器組態選項](../../database-engine/configure-windows/external-scripts-enabled-server-configuration-option.md)   
 [SERVERPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/serverproperty-transact-sql.md)   
 [SQL Server 的 External Scripts 物件](../../relational-databases/performance-monitor/sql-server-external-scripts-object.md)  
[sys.dm_external_script_requests](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-requests.md)  
[sys.dm_external_script_execution_stats](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-execution-stats.md) 
