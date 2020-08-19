---
description: sp_execute_external_script (Transact-SQL)
title: sp_execute_external_script (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 08/06/2020
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: machine-learning-services
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
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=azuresqldb-mi-current||=sqlallproducts-allversions'
ms.openlocfilehash: b820003b3039a8561dd299a7fb85c1d52b043bda
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88447184"
---
# <a name="sp_execute_external_script-transact-sql"></a>sp_execute_external_script (Transact-SQL)
[!INCLUDE [SQL Server 2016 SQL MI](../../includes/applies-to-version/sqlserver2016-asdbmi.md)]

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
**Sp_execute_external_script**預存程式會執行以輸入引數形式提供給程式的腳本，並與[Machine Learning 服務](../../machine-learning/sql-server-machine-learning-services.md)和[語言延伸](../../language-extensions/language-extensions-overview.md)模組搭配使用。 

針對 Machine Learning 服務， [Python](../../machine-learning/concepts/extension-python.md) 和 [R](../../machine-learning/concepts/extension-r.md) 是支援的語言。 針對語言延伸模組，支援 JAVA，但必須使用 [CREATE EXTERNAL Language](../../t-sql/statements/create-external-language-transact-sql.md)來定義。

若要執行 **sp_execute_external_script**，您必須先安裝 Machine Learning 服務或語言擴充功能。 如需詳細資訊，請參閱在 Windows 和[linux](../../linux/sql-server-linux-setup-machine-learning.md)[上安裝 SQL Server Machine Learning Services (Python 和 R) ](../../machine-learning/install/sql-machine-learning-services-windows-install.md) ，或在 Windows 和[Linux](../../linux/sql-server-linux-setup-language-extensions.md)[上安裝 SQL Server 語言擴充](../../language-extensions/install/install-sql-server-language-extensions-on-windows.md)功能。
::: moniker-end

::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
**Sp_execute_external_script**預存程式會執行以輸入引數形式提供給程式的腳本，並與 SQL Server 2017 上的[Machine Learning 服務](../../machine-learning/sql-server-machine-learning-services.md)搭配使用。

針對 Machine Learning 服務， [Python](../../machine-learning/concepts/extension-python.md) 和 [R](../../machine-learning/concepts/extension-r.md) 是支援的語言。

若要執行 **sp_execute_external_script**，您必須先安裝 Machine Learning 服務。 如需詳細資訊，請參閱 [在 Windows 上安裝 SQL Server Machine Learning Services (Python 和 R) ](../../machine-learning/install/sql-machine-learning-services-windows-install.md)。
::: moniker-end

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
**Sp_execute_external_script**預存程式會執行以輸入引數形式提供給程式的腳本，並在 SQL Server 2016 上搭配[R 服務](../../machine-learning/r/sql-server-r-services.md)使用。

R 服務的  [r](../../machine-learning/concepts/extension-r.md) 是支援的語言。

若要執行 **sp_execute_external_script**，您必須先安裝 R 服務。 如需詳細資訊，請參閱 [在 Windows 上安裝 SQL Server Machine Learning Services (Python 和 R) ](../../machine-learning/install/sql-r-services-windows-install.md)。
::: moniker-end

::: moniker range="=azuresqldb-mi-current||=sqlallproducts-allversions"
**Sp_execute_external_script**預存程式會執行以輸入引數形式提供給程式的腳本，並與[Azure SQL 受控執行個體中的 Machine Learning 服務](/azure/azure-sql/managed-instance/machine-learning-services-overview)搭配使用。

針對 Machine Learning 服務， [Python](../../machine-learning/concepts/extension-python.md) 和 [R](../../machine-learning/concepts/extension-r.md) 是支援的語言。

若要執行 **sp_execute_external_script**，您必須先啟用 Machine Learning 服務。 如需詳細資訊，請參閱 [AZURE SQL 中的 Machine Learning 服務受控執行個體檔](/azure/azure-sql/managed-instance/machine-learning-services-overview)。
::: moniker-end

![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=azuresqldb-mi-current||=sqlallproducts-allversions"
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
::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
## <a name="syntax-for-sql-server-2017-and-earlier"></a>SQL Server 2017 及更早版本的語法

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
 ** \@ language** = N '*language*'  
::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
 指出指令碼語言。 *語言* 為 **sysname**。 有效值為 **R**、 **Python**和以 [CREATE EXTERNAL language](../../t-sql/statements/create-external-language-transact-sql.md) 定義的任何語言 (例如，JAVA) 。
::: moniker-end
::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
 指出指令碼語言。 *語言* 為 **sysname**。 在 SQL Server 2017 中，有效的值為 **R** 和 **Python**。
::: moniker-end
::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
 指出指令碼語言。 *語言* 為 **sysname**。 在 SQL Server 2016 中，唯一有效的值是 **R**。
::: moniker-end
::: moniker range="=azuresqldb-mi-current||=sqlallproducts-allversions"
 指出指令碼語言。 *語言* 為 **sysname**。 在 Azure SQL 受控執行個體中，有效的值為 **R** 和 **Python**。
::: moniker-end

 ** \@ 腳本**= N '*script*' 外部語言腳本指定為常值或變數輸入。 *腳本* 是 **Nvarchar (max) **。  

`[ @input_data_1 =  N'input_data_1' ]` 以查詢的形式指定外部腳本所使用的輸入資料 [!INCLUDE[tsql](../../includes/tsql-md.md)] 。 *Input_data_1*的資料類型為**Nvarchar (max) **。

`[ @input_data_1_name = N'input_data_1_name' ]` 指定用來表示所定義之查詢的變數名稱 @input_data_1 。 外部腳本中變數的資料類型取決於語言。 如果是 R，則輸入變數是資料框架。 在 Python 的案例中，輸入必須是表格式的。 *input_data_1_name* 為 **sysname**。  預設值為 *>inputdataset*。  

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
`[ @input_data_1_order_by_columns = N'input_data_1_order_by_columns' ]` 用來建立每個資料分割模型。 指定用來排序結果集的資料行名稱，例如依產品名稱。 外部腳本中變數的資料類型取決於語言。 如果是 R，則輸入變數是資料框架。 在 Python 的案例中，輸入必須是表格式的。

`[ @input_data_1_partition_by_columns = N'input_data_1_partition_by_columns' ]` 用來建立每個資料分割模型。 指定用來分割資料的資料行名稱，例如地理區域或日期。 外部腳本中變數的資料類型取決於語言。 如果是 R，則輸入變數是資料框架。 在 Python 的案例中，輸入必須是表格式的。 
::: moniker-end

`[ @output_data_1_name =  N'output_data_1_name' ]` 指定外部腳本中的變數名稱，這個變數包含 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 完成預存程序呼叫時要傳回的資料。 外部腳本中變數的資料類型取決於語言。 針對 R，輸出必須是資料框架。 針對 Python，輸出必須是 pandas 資料框架。 *output_data_1_name* 為 **sysname**。  預設值為 *OutputDataSet*。  

`[ @parallel = 0 | 1 ]` 將參數設定為1，以啟用 R 腳本的平行執行 `@parallel` 。 此參數的預設值為 0 (沒有平行處理) 。 如果要將 `@parallel = 1` 輸出直接串流處理至用戶端電腦，則 `WITH RESULT SETS` 需要子句，而且必須指定輸出架構。  

 + 針對不使用 RevoScaleR 函式的 R 腳本，使用  `@parallel` 參數有助於處理大型資料集，假設腳本可以完整平行處理。 例如，使用 R `predict` 函數搭配模型來產生新的預測時，請將設定 `@parallel = 1` 為查詢引擎的提示。 如果可以平行處理查詢，則會根據 **MAXDOP** 設定來散發資料列。  
  
 + 針對使用 RevoScaleR 函式的 R 腳本，平行處理會自動處理，您不應該指定 `@parallel = 1` **sp_execute_external_script** 呼叫。  
  
`[ @params = N'@parameter_name data_type [ OUT | OUTPUT ] [ ,...n ]' ]` 外部腳本中所使用的輸入參數宣告清單。  
  
`[ @parameter1 = 'value1' [ OUT | OUTPUT ] [ ,...n ] ]` 外部腳本所使用之輸入參數的值清單。  

## <a name="remarks"></a>備註

> [!IMPORTANT]
> 查詢樹狀結構由 SQL machine learning 控制，使用者無法對查詢執行任意作業。

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
使用 **sp_execute_external_script** 來執行以支援語言撰寫的腳本。 支援的語言為搭配 Machine Learning 服務使用的 **Python** 和 **R** ，以及以 [CREATE EXTERNAL language](../../t-sql/statements/create-external-language-transact-sql.md) 定義的任何語言 (例如，搭配語言擴充功能使用的 JAVA) 。
::: moniker-end
::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
使用 **sp_execute_external_script** 來執行以支援語言撰寫的腳本。 支援的語言為 SQL Server 2017 Machine Learning Services 中的 **Python** 和 **R** 。
::: moniker-end
::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
使用 **sp_execute_external_script** 來執行以支援語言撰寫的腳本。 唯一支援的語言是 SQL Server 2016 R Services 中的 **r** 。
::: moniker-end
::: moniker range="=azuresqldb-mi-current||=sqlallproducts-allversions"
使用 **sp_execute_external_script** 來執行以支援語言撰寫的腳本。 支援的語言為 Azure SQL 受控執行個體 Machine Learning 服務中的 **Python** 和 **R** 。
::: moniker-end

根據預設，這個預存程式所傳回的結果集會是具有未命名資料行的輸出。 腳本中使用的資料行名稱在腳本環境中是本機的，且不會反映在輸出結果集中。 若要命名結果集資料行，請使用的 `WITH RESULT SET` 子句 [`EXECUTE`](../../t-sql/language-elements/execute-transact-sql.md) 。

除了傳回結果集之外，您還可以使用輸出參數傳回純量值。

::: moniker range=">=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions"
您可以藉由設定外部資源集區來控制外部腳本所使用的資源。 如需詳細資訊，請參閱 [&#40;transact-sql&#41;建立外部資源集 ](../../t-sql/statements/create-external-resource-pool-transact-sql.md)區。 工作負載的相關資訊可從 resource governor 目錄 views、DMV 和計數器取得。 如需詳細資訊，請參閱 [Resource Governor &#40;transact-sql&#41;的目錄檢視 ](../../relational-databases/system-catalog-views/resource-governor-catalog-views-transact-sql.md)、 [Resource Governor 相關動態管理檢視 &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/resource-governor-related-dynamic-management-views-transact-sql.md)和 [SQL Server 的外部腳本物件](../../relational-databases/performance-monitor/sql-server-external-scripts-object.md)。  
::: moniker-end

### <a name="monitor-script-execution"></a>監視腳本執行

使用 [sys. dm_external_script_requests](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-requests.md) 和 [sys. dm_external_script_execution_stats](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-execution-stats.md)監視腳本執行。

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
### <a name="parameters-for-partition-modeling"></a>資料分割模型的參數

您可以設定兩個額外的參數來啟用分割資料的模型化，其中的資料分割是根據您提供的一或多個資料行，自然地將資料集分割成建立的邏輯分割區，並只在腳本執行期間使用。 包含年齡、性別、地理區域、日期或時間之重複值的資料行，是幾個可讓您成為分割資料集的範例。

這兩個參數是 **input_data_1_partition_by_columns** 和 **input_data_1_order_by_columns**，而第二個參數則是用來排序結果集。 參數會以輸入的形式傳遞至， `sp_execute_external_script` 並針對每個資料分割執行一次外部腳本。 如需詳細資訊和範例，請參閱 [教學課程：建立資料分割型模型](https://docs.microsoft.com/sql/machine-learning/tutorials/r-tutorial-create-models-per-partition)。

您可以藉由指定，以平行方式執行腳本 `@parallel=1` 。 如果可以平行處理輸入查詢，您應該將設為 `@parallel=1` 的引數的一部分 `sp_execute_external_script` 。 根據預設，查詢最佳化工具會在 `@parallel=1` 具有超過256個數據列的資料表上運作，但如果您想要明確處理此問題，此腳本會將參數包含為示範。

> [!Tip]
> 針對定型工作負載，您可以使用 `@parallel` 搭配任何任意的定型指令碼，甚至是使用非 Microsoft-rx 演算法的指令碼。 一般來說，只有 RevoScaleR 演算法 (具有 rx 前置詞) 在 SQL Server 的定型案例中提供平行處理原則。 但利用 SQL Server 2019 和更新版本中的新參數，您可以平行處理腳本，以呼叫未特別以該功能設計的函式。
::: moniker-end

### <a name="streaming-execution-for-python-and-r-scripts"></a>Python 和 R 腳本的串流執行  

串流可讓 Python 或 R 腳本使用超過記憶體所能容納的資料。 若要控制串流期間傳遞的資料列數目，請在集合中為參數指定整數值 `@r_rowsPerRead` `@params` 。  例如，如果您要定型的模型會使用非常廣泛的資料，您可以調整值以讀取較少的資料列，以確保所有資料列都可以在一個資料區塊中傳送。 您也可以使用這個參數來管理一次讀取和處理的資料列數目，以減少伺服器效能問題。 
  
`@r_rowsPerRead`串流和引數的參數都 `@parallel` 應該視為提示。 針對要套用的提示，必須可以產生包含平行處理的 SQL 查詢計劃。 如果這不可行，則無法啟用平行處理。  
  
> [!NOTE]  
> 只有 Enterprise Edition 才支援串流和平行處理。 您可以在 Standard Edition 的查詢中包含參數，而不會引發錯誤，但參數沒有任何作用，而且 R 腳本會在單一進程中執行。  
  
## <a name="restrictions"></a>限制  

### <a name="data-types"></a>資料類型

在 **sp_execute_external_script** 程式的輸入查詢或參數中使用時，不支援下列資料類型，而且會傳回不支援的類型錯誤。  

因應措施是將資料行或值 **轉換** 成中支援的型別， [!INCLUDE[tsql](../../includes/tsql-md.md)] 然後再將它傳送至外部腳本。  
  
+ **cursor**  
  
+ **timestamp**  
  
+ **datetime2**、 **datetimeoffset**、 **time**  
  
+ **sql_variant**  
  
+ **文字**、 **影像**  
  
+ **xml**  
  
+ **hierarchyid**、 **geometry**、 **geography**  
  
+ CLR 使用者定義型別

一般而言，任何無法對應到資料類型的結果集 [!INCLUDE[tsql](../../includes/tsql-md.md)] 都會輸出為 Null。  

### <a name="restrictions-specific-to-r"></a>R 的特定限制

如果輸入包含的 **日期時間** 值不符合 R 中允許的值範圍，則會將值轉換成 **NA**。 這是必要的，因為 SQL machine learning 允許比 R 語言支援更大範圍的值。

浮點數 (例如， `+Inf` `-Inf` `NaN` 即使這兩種語言都使用 IEEE 754，仍不支援 SQL machine learning 中的) 。 目前的行為只會直接將值傳送至 SQL;因此，SQL 用戶端會擲回錯誤。 因此，這些值會轉換成 **Null**。

## <a name="permissions"></a>權限

需要 **EXECUTE ANY EXTERNAL SCRIPT** 資料庫許可權。  

## <a name="examples"></a>範例

本章節包含如何使用這個預存程式來執行 R 或 Python 腳本的範例 [!INCLUDE[tsql](../../includes/tsql-md.md)] 。

### <a name="a-return-an-r-data-set-to-sql-server"></a>A. 將 R 資料集傳回 SQL Server  

下列範例會建立一個預存程式，該預存程式會使用 **sp_execute_external_script** 來傳回 R 隨附的鳶尾花資料集。  

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

### <a name="b-create-a-python-model-and-generate-scores-from-it"></a>B. 建立 Python 模型，並從中產生分數

此範例說明如何使用 `sp_execute_external_script` ，在簡單的 Python 模型上產生分數。

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

Python 程式碼中使用的資料行標題不會輸出到 SQL Server;因此，請使用 WITH RESULT 語句來指定要使用的 SQL 資料行名稱和資料類型。

::: moniker range=">=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions"
### <a name="c-generate-an-r-model-based-on-data-from-sql-server"></a>C. 根據 SQL Server 的資料產生 R 模型  

下列範例會建立一個預存程式，該預存程式會使用 **sp_execute_external_script** 來產生鳶尾花模型並傳回模型。  

> [!NOTE]
> 此範例需要預先安裝 e1071 套件。 如需詳細資訊，請參閱 [SQL Server 上的安裝其他 R 套件](../../machine-learning/package-management/install-additional-r-packages-on-sql-server.md)。

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
::: moniker-end

若要計分，您也可以使用原生 [PREDICT](../../t-sql/queries/predict-transact-sql.md) 函式，其會避免呼叫 Python 或 R 執行階段，因此一般來說速度更快。

## <a name="see-also"></a>另請參閱

+ [SQL 機器學習服務](../../machine-learning/index.yml)
+ [SQL Server 語言擴充](../../language-extensions/language-extensions-overview.md)功能。 
+ [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
+ [CREATE EXTERNAL LIBRARY &#40;Transact-sql&#41;](../../t-sql/statements/create-external-library-transact-sql.md)  
+ [sp_prepare &#40;交易 SQL&#41;](../../relational-databases/system-stored-procedures/sp-prepare-transact-sql.md)   
+ [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
+ [外部指令碼已啟用伺服器組態選項](../../database-engine/configure-windows/external-scripts-enabled-server-configuration-option.md)   
+ [SERVERPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/serverproperty-transact-sql.md)   
+ [SQL Server, 外部指令碼物件](../../relational-databases/performance-monitor/sql-server-external-scripts-object.md)  
+ [sys.dm_external_script_requests](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-requests.md)  
+ [sys.dm_external_script_execution_stats](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-execution-stats.md) 
