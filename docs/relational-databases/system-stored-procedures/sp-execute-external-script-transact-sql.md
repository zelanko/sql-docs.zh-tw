---
title: sp_execute_external_script(轉算-SQL) |微軟文件
ms.custom: ''
ms.date: 11/04/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: machine-learning
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
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions||=azuresqldb-mi-current'
ms.openlocfilehash: 8800df26e505f1fffe25e6f65218481e7a8158f0
ms.sourcegitcommit: 68583d986ff5539fed73eacb7b2586a71c37b1fa
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/04/2020
ms.locfileid: "80663008"
---
# <a name="sp_execute_external_script-transact-sql"></a>sp_execute_external_script (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
**sp_execute_external_script**儲存過程執行作為過程的輸入參數提供的腳本,並與[機器學習服務和](../../machine-learning/index.yml)[語言擴展](../../language-extensions/language-extensions-overview.md)一起使用。 

對於機器學習服務[,Python](../../machine-learning/concepts/extension-python.md)和[R](../../machine-learning/concepts/extension-r.md)是支援的語言。 對於語言擴展,JAVA 是支援的,但必須使用[創建外部語言](../../t-sql/statements/create-external-language-transact-sql.md)進行定義。

要執行**sp_execute_external_script**,必須首先安裝機器學習服務或語言擴展。 有關詳細資訊,請參閱在 Windows 與[Linux](../../linux/sql-server-linux-setup-machine-learning.md)[安裝 SQL 伺服器機器學習服務 (Python 和 R),](../../machine-learning/install/sql-machine-learning-services-windows-install.md)或在 Windows 和[Linux](../../linux/sql-server-linux-setup-language-extensions.md)上安裝[SQL 伺服器語言擴展](../../language-extensions/install/install-sql-server-language-extensions-on-windows.md)。
::: moniker-end

::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
**sp_execute_external_script**儲存過程執行作為過程的輸入參數提供的腳本,並在 SQL Server 2017 上與[機器學習服務](../../machine-learning/index.yml)一起使用。 

對於機器學習服務[,Python](../../machine-learning/concepts/extension-python.md)和[R](../../machine-learning/concepts/extension-r.md)是支援的語言。 

要執行**sp_execute_external_script**,必須首先安裝機器學習服務。 有關詳細資訊,請參閱在[Windows 上安裝 SQL 伺服器機器學習服務(Python 和 R)。](../../machine-learning/install/sql-machine-learning-services-windows-install.md)
::: moniker-end

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
**sp_execute_external_script**儲存過程執行作為過程的輸入參數提供的腳本,並在 SQL Server 2016 上與[R 服務](../../machine-learning/r/sql-server-r-services.md)一起使用。

對於 R 服務[,R](../../machine-learning/concepts/extension-r.md)是支援的語言。

要執行**sp_execute_external_script**,必須首先安裝 R 服務。 有關詳細資訊,請參閱在[Windows 上安裝 SQL 伺服器機器學習服務(Python 和 R)。](../../machine-learning/install/sql-r-services-windows-install.md)
::: moniker-end

 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  

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
::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
## <a name="syntax-for-2017-and-earlier"></a>2017 年及更早版本語法

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
 語言 =*language*N'**\@** 語言 '  
::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
 指示腳本語言。 *語言*是**sysname**。 有效值為**R** **、Python**和使用[創建外部語言](../../t-sql/statements/create-external-language-transact-sql.md)(例如 Java)定義的任何語言。
::: moniker-end
::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
 指示腳本語言。 *語言*是**sysname**。 在 SQL Server 2017 中,有效值為**R**和**Python**。
::: moniker-end
::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
 指示腳本語言。 *語言*是**sysname**。 在 SQL Server 2016 中,唯一有效的值是**R**。
::: moniker-end

 文稿 = N'*文稿*' 外部語言文本指定為文本**\@** 或變數輸入。 *腳本*是**nvarchar(最大值)。**  

`[ @input_data_1 =  N'input_data_1' ]`以[!INCLUDE[tsql](../../includes/tsql-md.md)]查詢的形式指定外部文本使用的輸入數據。 *input_data_1*的數據類型為**nvarchar(最大值)。**

`[ @input_data_1_name = N'input_data_1_name' ]`指定用於表示 定義的查詢@input_data_1的變數的名稱。 外部文本中變數的數據類型取決於語言。 在 R 的情況下,輸入變數是數據框。 在 Python 的情況下,輸入必須為表格。 *input_data_1_name*是**sysname**。  預設值為*InputDataSet*。  

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
`[ @input_data_1_order_by_columns = N'input_data_1_order_by_columns' ]`用於構建每個分區模型。 指定用於對結果集進行排序的列的名稱,例如按產品名稱。 外部文本中變數的數據類型取決於語言。 在 R 的情況下,輸入變數是數據框。 在 Python 的情況下,輸入必須為表格。

`[ @input_data_1_partition_by_columns = N'input_data_1_partition_by_columns' ]`用於構建每個分區模型。 指定用於分割資料的欄的名稱,例如地理區域或日期。 外部文本中變數的數據類型取決於語言。 在 R 的情況下,輸入變數是數據框。 在 Python 的情況下,輸入必須為表格。 
::: moniker-end

`[ @output_data_1_name =  N'output_data_1_name' ]`指定外部文本中變數的名稱,該變數包含完成存儲過程調用後要返回到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的數據。 外部文本中變數的數據類型取決於語言。 對於 R,輸出必須是數據框。 對於 Python,輸出必須是熊貓數據框。 *output_data_1_name*是**sysname**。  預設值為*輸出資料集*。  

`[ @parallel = 0 | 1 ]`通過將參數設置為 1,實現`@parallel`R 腳本的並行執行。 此參數的預設值為 0(無併行性)。 如果`@parallel = 1`輸出直接流式傳輸到用戶端計算機,則需要`WITH RESULT SETS`子句,並且必須指定輸出架構。  

 + 對於不使用 RevoScaleR 函數的 R`@parallel`腳本, 使用 參數可用於處理大型數據集,前提是腳本可以進行細微的並行化。 例如,將`predict`R 函數與模型一起使用以生成新預測`@parallel = 1`時, 將設置為查詢引擎的提示。 如果查詢可以並行化,則根據**MAXDOP**設置分配行。  
  
 + 對於使用 RevoScaleR 函數的 R 腳本,並行處理會`@parallel = 1`自動處理,並且 不應指定到**sp_execute_external_script**呼叫。  
  
`[ @params = N'@parameter_name data_type [ OUT | OUTPUT ] [ ,...n ]' ]`外部文本中使用的輸入參數聲明的清單。  
  
`[ @parameter1 = 'value1' [ OUT | OUTPUT ] [ ,...n ] ]`外部文本使用的輸入參數的值清單。  

## <a name="remarks"></a>備註

> [!IMPORTANT]
> 查詢樹由[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]該 樹控制,使用者無法對查詢執行任意操作。 

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
使用**sp_execute_external_script**執行使用受支援的語言編寫的腳本。 支援的語言是與機器學習服務一起使用的**Python**和**R,** 以及使用[「創建外部語言](../../t-sql/statements/create-external-language-transact-sql.md)」(例如 Java)定義的任何與語言擴展一起使用的語言。
::: moniker-end
::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
使用**sp_execute_external_script**執行使用受支援的語言編寫的腳本。 支援的語言是 SQL Server 2017 機器學習服務中的**Python**和**R。**
::: moniker-end
::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
使用**sp_execute_external_script**執行使用受支援的語言編寫的腳本。 唯一支援的語言是 SQL Server 2016 R 服務中的**R。**
::: moniker-end

預設情況下,此存儲過程返回的結果集使用未命名的列進行輸出。 文本中使用的列名稱是腳本環境的本地名稱,不會反映在輸出結果集中。 要命名結果集列,`WITH RESULT SET`請使用[`EXECUTE`](../../t-sql/language-elements/execute-transact-sql.md)子句。

除了傳回結果集外,您還可以使用 OUTPUT 參數將[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]標量值傳回到 。 
  
您可以通過設定外部資源池來控制外部文本使用的資源。 有關詳細資訊,請參閱[創建外部資源池&#40;處理-SQL&#41;](../../t-sql/statements/create-external-resource-pool-transact-sql.md)。 有關工作負載的資訊可以從資源調控器目錄視圖、DMV和計數器獲取。 有關詳細資訊,請參閱[資源調控器目錄檢視&#40;Transact-SQL&#41;、](../../relational-databases/system-catalog-views/resource-governor-catalog-views-transact-sql.md)[資源調控器相關動態管理視圖&#40;處理-SQL&#41;](../../relational-databases/system-dynamic-management-views/resource-governor-related-dynamic-management-views-transact-sql.md))和[SQL Server、外部腳本物件](../../relational-databases/performance-monitor/sql-server-external-scripts-object.md)。  

### <a name="monitor-script-execution"></a>監視文稿執行

使用[sys.dm_external_script_requests](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-requests.md)和[sys.dm_external_script_execution_stats](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-execution-stats.md)監視腳本執行。 

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
### <a name="parameters-for-partition-modeling"></a>分割區建模的參數

您可以設置兩個附加參數,以便在分區數據上啟用建模,其中分區基於您提供的一個或多個列,這些列自然地將資料集段段到僅在腳本執行期間創建和使用的邏輯分區中。 包含年齡、性別、地理區域、日期或時間的重複值的列是適合分區數據集的幾個示例。
 
這兩個參數是**input_data_1_partition_by_columns**和**input_data_1_order_by_columns**,其中第二個參數用於對結果集進行排序。 參數作為輸入傳遞給每個`sp_execute_external_script`分區的外部腳本一次。 有關詳細資訊和範例,請參閱[教程:建立基於分區的模型](https://docs.microsoft.com/sql/machine-learning/tutorials/r-tutorial-create-models-per-partition)。

可以通過`@parallel=1`指定 並行執行腳本。 如果輸入查詢可以並行化,則應將作為參數的`@parallel=1`一部分設定為`sp_execute_external_script`。 默認情況下,查詢優化器在具有 256 行以上的`@parallel=1`表下 運行,但如果要顯式處理此參數,此腳本將參數作為演示。

> [!Tip]
> 針對定型工作負載，您可以使用 `@parallel` 搭配任何任意的定型指令碼，甚至是使用非 Microsoft-rx 演算法的指令碼。 一般來說，只有 RevoScaleR 演算法 (具有 rx 前置詞) 在 SQL Server 的定型案例中提供平行處理原則。 但是,使用 SQL Server vNext 中的新參數,您可以並行化調用未專門設計此功能的功能的腳本。
::: moniker-end

### <a name="streaming-execution-for-python-and-r-scripts"></a>Python 與 R 文稿的流式處理  

流式處理允許 Python 或 R 文稿處理比記憶體中容納的數據多的數據。 要控制流式處理期間傳遞的行數,請在`@r_rowsPerRead``@params`集合中為參數指定整數值。  例如,如果您正在訓練使用非常寬數據的模型,則可以調整該值以讀取更少的行,以確保所有行都可以在一個數據塊中發送。 您還可以使用此參數管理一次讀取和處理的行數,以緩解伺服器性能問題。 
  
流和`@r_rowsPerRead``@parallel`參數的參數都應視為提示。 要應用提示,必須可以生成包含並行處理的 SQL 查詢計劃。 如果無法這樣做,則無法啟用並行處理。  
  
> [!NOTE]  
> 流和並行處理僅在企業版中支援。 您可以在標準版的查詢中包括參數,而不會引發錯誤,但參數不起作用,R 腳本在單個進程中運行。  
  
## <a name="restrictions"></a>限制  

### <a name="data-types"></a>資料類型

在輸入查詢或**sp_execute_external_script**過程的參數中使用時,不支援以下數據類型,並返回不支援的類型錯誤。  

作為解決方法,在將其**CAST**發送到外部腳[!INCLUDE[tsql](../../includes/tsql-md.md)]本 之前,將列或值強制轉換為受支援的類型。  
  
-   **cursor**  
  
-   **時間 戳**  
  
-   **日期時間2**,**日期時間偏移**,**時間**  
  
-   **sql_variant**  
  
-   **文字**,**影像**  
  
-   **xml**  
  
-   **層次結構**,**幾何 ,****地理**  
  
-   CLR 使用者定義型別

通常,任何無法映射到[!INCLUDE[tsql](../../includes/tsql-md.md)]資料類型的結果集都輸出為 NULL。  

### <a name="restrictions-specific-to-r"></a>特定於 R 的限制

如果輸入包含日期**時間**值不符合 R 中允許的值範圍,則值將轉換為**NA**。 這是必需的,因為[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]允許的值範圍比 R 語言中支援的值範圍更大。

即使兩種語言都使用`+Inf`IEEE 754,也不支援浮點值(`-Inf`例如`NaN`, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , , 。 當前行為只是將值直接發送到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)];因此,中的[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]SQL 用戶端會引發錯誤。 因此,這些值將轉換為**NULL**。

## <a name="permissions"></a>權限

需要**執行任何外部腳本**資料庫許可權。  

## <a name="examples"></a>範例

目前需要使用此儲存程序使用 執行 R 或 Python 文[!INCLUDE[tsql](../../includes/tsql-md.md)]稿的範例 。

### <a name="a-return-an-r-data-set-to-sql-server"></a>A. 將 R 資料集傳回 SQL 伺服器  

下面的範例建立儲存的程序,使用**sp_execute_external_script**將 R 中包含的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Iris 資料集傳回到 。  

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

### <a name="b-generate-an-r-model-based-on-data-from-sql-server"></a>B. 基於 SQL Server 的資料產生 R 模型  

下面的範例創建一個儲存過程,該過程使用**sp_execute_external_script**生成光圈模型並將模型[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]傳回到 。  

> [!NOTE]
>  此示例要求提前安裝 e1071 軟體包。 有關詳細資訊,請參閱在[SQL Server 安裝其他 R 套件](../../machine-learning/package-management/install-additional-r-packages-on-sql-server.md)。

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

Python 代碼中使用的列標題不會輸出到 SQL Server;但是,這些列標題不會輸出到 SQL Server。因此,使用 WITH RESULT 語句指定要使用的 SQL 的列名稱和資料類型。

若要計分，您也可以使用原生 [PREDICT](../../t-sql/queries/predict-transact-sql.md) 函式，其會避免呼叫 Python 或 R 執行階段，因此一般來說速度更快。

## <a name="see-also"></a>另請參閱

+ [SQL Server Machine Learning 服務](../../machine-learning/index.yml)
+ [SQL 伺服器語言延伸](../../language-extensions/language-extensions-overview.md)。 
+ [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
+ [Python 函式庫與資料型態](../../machine-learning/python/python-libraries-and-data-types.md)  
+ [R 函式庫和 R 資料型態](../../machine-learning/r/r-libraries-and-data-types.md)  
+ [SQL 伺服器 R 服務](../../machine-learning/r/sql-server-r-services.md)   
+ [SQL 伺服器機器學習服務的已知問題](../../machine-learning/known-issues-for-sql-server-machine-learning-services.md)   
+ [建立外部庫&#40;轉接-SQL&#41;](../../t-sql/statements/create-external-library-transact-sql.md)  
+ [sp_prepare&#40;交易 SQL&#41;](../../relational-databases/system-stored-procedures/sp-prepare-transact-sql.md)   
+ [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
+ [開啟外部文稿伺服器設定選項](../../database-engine/configure-windows/external-scripts-enabled-server-configuration-option.md)   
+ [SERVERPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/serverproperty-transact-sql.md)   
+ [SQL Server 的 External Scripts 物件](../../relational-databases/performance-monitor/sql-server-external-scripts-object.md)  
+ [sys.dm_external_script_requests](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-requests.md)  
+ [sys.dm_external_script_execution_stats](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-execution-stats.md) 
