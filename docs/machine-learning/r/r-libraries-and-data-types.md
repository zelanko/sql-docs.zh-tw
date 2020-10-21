---
title: 轉換 R 與 SQL 資料類型
description: 檢閱資料科學與機器學習解決方案中 R 與 SQL Server 之間的隱含與明確資料類型轉換。
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 10/06/2020
ms.topic: how-to
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=azuresqldb-mi-current||=sqlallproducts-allversions'
ms.openlocfilehash: 2cd8a40fc1c85b8a58216a4c15ff0d1bb56df1da
ms.sourcegitcommit: 783b35f6478006d654491cb52f6edf108acf2482
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/09/2020
ms.locfileid: "91892238"
---
# <a name="data-type-mappings-between-r-and-sql-server"></a>R 與 SQL Server 之間的資料類型對應
[!INCLUDE [SQL Server 2016 and later](../../includes/applies-to-version/sqlserver2016.md)]

本文列出在 SQL Server 機器學習服務中使用 R 整合功能時，所支援資料類型及所執行的資料類型轉換。

## <a name="base-r-version"></a>基底 R 版本

SQL Server 2016 R Services 與具有 R 的 SQL Server 機器學習服務與特定 Microsoft R Open 版本保持一致。 例如，最新版 SQL Server 2019 機器學習服務的建置基礎為 Microsoft R Open 3.5.2。

若要檢視與特定 SQL Server 執行個體建立關聯的 R 版本，請在 SQL 執行個體中開啟 **RGui**。 例如，SQL Server 2019 預設執行個體的路徑會是：`C:\Program Files\Microsoft SQL Server\MSSQL15.MSSQLSERVER\R_SERVICES\bin\x64\Rgui.exe`。

此工具會載入基底 R 與其他程式庫。 在工作階段啟動時載入的每個套件，都會在通知中提供套件版本資訊。

## <a name="r-and-sql-data-types"></a>R 與 SQL 資料類型

雖然 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支援數十種資料類型，但 R 的純量資料類型 (數字、整數、複雜、邏輯、字元、日期/時間和原始) 數量有限。 因此，每當您在 R 指令碼中使用來自 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的資料時，資料可能會隱含地轉換為相容的資料類型。 不過，通常無法自動執行精確的轉換，而且會傳回錯誤，例如「未處理的 SQL 資料類型」。

此節列出所提供的隱含轉換，並列出不支援的資料類型。 針對在 R 與 SQL Server 之間對應資料類型，我們提供一些指導方針。

## <a name="implicit-data-type-conversions"></a>隱含資料類型轉換

下表顯示在 R 指令碼中使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的資料，然後傳回給 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]時，資料類型和值的變更。

| SQL 類型                         | R 類別     | RESULT SET 類型    | 註解            |
|----------------------------------|-------------|--------------------|---------------------|
| **bigint**                       | `numeric`   | **float**          | 使用 `sp_execute_external_script` 執行 R 指令碼允許以 bigint 資料類型作為輸入資料。 不過，由於其會轉換成 R 的數值類型，因此極高值或具有小數點的值會出現精確度遺失情況。 R 最多只支援 53 位元整數，之後會開始出現精確度遺失的情況。                                                                                         |
| **binary(n)**<br /> n <= 8000    | `raw`       | **varbinary(max)** | 只允許作為輸入參數和輸出 |
| **bit**                          | `logical`   | **bit**            |                     |
| **char(n)**<br /> n <= 8000      | `character` | **varchar(max)**   | 由於在未明確設定 *stringsAsFactors* 參數的情況下建立輸入資料框架 (input_data_1)，因此資料行類型將取決於 R 中的 *default.stringsAsFactors()*                                                                                                                                                                                                                                           |
| **datetime**                     | `POSIXct`   | **datetime**       | 以 GMT 來表示  |
| **date**                         | `POSIXct`   | **datetime**       | 以 GMT 來表示  |
| **decimal(p,s)**                 | `numeric`   | **float**          | 使用 `sp_execute_external_script` 來執行 R 指令碼，以允許將 decimal 資料類型作為輸入資料。 不過，由於其會轉換成 R 的數值類型，因此極高值或具有小數點的值會出現精確度遺失情況。 `sp_execute_external_script` 與 R 指令碼不支援資料類型的完整範圍，且會改變最後幾個小數位數，特別是分數的小數位數。 |
| **float**                        | `numeric`   | **float**          |                     |
| **int**                          | `integer`   | **int**            |                     |
| **money**                        | `numeric`   | **float**          | 使用 `sp_execute_external_script` 來執行 R 指令碼，以允許將 money 資料類型作為輸入資料。 不過，由於其會轉換成 R 的數值類型，因此極高值或具有小數點的值會出現精確度遺失情況。 有時候，美分值不精確，且會發出警告：警告：無法精確地表示美分值。                                               |
| **numeric(p,s)**                 | `numeric`   | **float**          | 使用 `sp_execute_external_script` 執行 R 指令碼，以允許將 numeric 資料類型作為輸入資料。 不過，由於其會轉換成 R 的數值類型，因此極高值或具有小數點的值會出現精確度遺失情況。 `sp_execute_external_script` 與 R 指令碼不支援資料類型的完整範圍，且會改變最後幾個小數位數，特別是分數的小數位數。 |
| **real**                         | `numeric`   | **float**          |                     |
| **smalldatetime**                | `POSIXct`   | **datetime**       | 以 GMT 來表示  |
| **smallint**                     | `integer`   | **int**            |                     |
| **smallmoney**                   | `numeric`   | **float**          |                     |
| **tinyint**                      | `integer`   | **int**            |                     |
| **uniqueidentifier**             | `character` | **varchar(max)**   |                     |
| **varbinary(n)**<br /> n <= 8000 | `raw`       | **varbinary(max)** | 只允許作為輸入參數和輸出 |
| **varbinary(max)**               | `raw`       | **varbinary(max)** | 只允許作為輸入參數和輸出 |
| **varchar(n)**<br /> n <= 8000   | `character` | **varchar(max)**   | 由於在未明確設定 *stringsAsFactors* 參數的情況下建立輸入資料框架 (input_data_1)，因此資料行類型將取決於 R 中的 *default.stringsAsFactors()*                                                                                                                                                                                                                                           |

## <a name="data-types-not-supported-by-r"></a>R 不支援的資料類型

在 [SQL Server 類型系統](../../t-sql/data-types/data-types-transact-sql.md)所支援的資料類型類別中，以下幾個類型在傳遞到 R 程式碼時很有可能會造成問題：

+ 列在 SQL 類型系統文章中＜其他＞  一節的資料類型：**cursor**、**timestamp**、**hierarchyid**、**uniqueidentifier**、**sql_variant**、**xml**、**table**
+ 所有空間類型
+ **image**

## <a name="data-types-that-might-convert-poorly"></a>轉換效果可能不佳的資料類型

+ 除了 **datetimeoffset** 之外，大部分的日期時間類型應該都能順利運作。
+ 支援大部分的數值資料類型，但 **money** 和 **smallmoney** 的轉換可能會失敗。
+ 支援 **varchar**，但由於 SQL Server 一般使用 Unicode，因此建議您盡可能使用 **nvarchar** 及其他 Unicode 文字資料類型。
+ 來自 RevoScaleR 函數庫且具有 rx 前置詞的函數，可以處理 SQL 二進位資料類型 (**binary** 和 **varbinary**)，但在大部分案例中，這些類型都需要特別處理。 大部分的 R 程式碼都無法搭配二進位資料行使用。

  
 如需 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型的詳細資訊，請參閱[資料類型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)

## <a name="changes-in-data-types-between-sql-server-versions"></a>SQL Server 各版本間的資料類型變更

Microsoft SQL Server 2016 和更新版本包含資料類型轉換和幾個其他作業的改進。 這些改進大部分都為處理浮點數類型提供更高的精確度，以及對傳統 **datetime** 類型的作業做出次要變更。

當您使用 130 或更高的資料庫相容性層級時，這些改進預設都可供使用。 不過，如果您使用不同的相容性層級，或使用較舊版本連線到資料庫，則可能會看見不同的數值精確度或其他結果。 

如需詳細資訊，請參閱[處理某些資料類型和不常見作業的 SQL Server 2016 改進 (機器翻譯)](https://support.microsoft.com/help/4010261/sql-server-2016-improvements-in-handling-some-data-types-and-uncommon-)。
 

## <a name="verify-r-and-sql-data-schemas-in-advance"></a>預先驗證 R 和 SQL 資料結構描述

一般而言，當您不清楚如何在 R 中使用特定的資料類型或資料結構時，皆可使用  `str()` 函數以取得 R 物件的內部結構和類型。 函數的結果會列印到 R 主控台，也會顯示在 **的 [訊息]** [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]索引標籤查詢結果中。 

當您從資料庫擷取要用於 R 程式碼的資料時，應該一律刪除無法用於 R 的資料行，以及其他對於分析沒有幫助的資料行，例如 GUIDS (Uniqueidentifier)、時間戳記和其他用於稽核的資料行，或是由 ETL 處理序建立的譜系資訊。 

請注意，包含不必要的資料行可能會大幅降低 R 程式碼的效能，尤其是使用高基數資料行做為因素的時候。 因此，我們建議您事先使用 SQL Server 系統預存程序和資訊檢視取得特定資料表的資料類型，並刪除或轉換不相容的資料行。 如需詳細資訊，請參閱 [Transact-SQL 中的資訊結構描述檢視](../../relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)

如果 R 不支援特定的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型，但您需要在 R 指令碼中使用該資料的數個資料行，建議您先使用 [CAST 和 CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md) 函數，以確保資料類型轉換會如預期般地執行，再於 R 指令碼中使用該資料。  

> [!WARNING]
> 如果您在移動資料時使用 **rxDataStep** 來卸除不相容的資料行，請留意 **RxSqlServerData** 資料來源類型不支援引數 _varsToKeep_ 和 _varsToDrop_。


## <a name="examples"></a>範例

### <a name="example-1-implicit-conversion"></a>範例 1：隱含轉換

以下範例示範資料在 SQL Server 和 R 之間進行來回行程時的轉換方式。

查詢會從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表取得一系列的值，並使用預存程序 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) 來使用 R 執行階段輸出值。

```sql
CREATE TABLE MyTable (    
 c1 int,    
 c2 varchar(10),    
 c3 uniqueidentifier    
);    
go    
INSERT MyTable VALUES(1, 'Hello', newid());    
INSERT MyTable VALUES(-11, 'world', newid());    
SELECT * FROM MyTable;    
  
EXECUTE sp_execute_external_script    
 @language = N'R'    
 , @script = N'    
inputDataSet["cR"] <- c(4, 2)    
str(inputDataSet)    
outputDataSet <- inputDataSet'    
 , @input_data_1 = N'SELECT c1, c2, c3 FROM MyTable'    
 , @input_data_1_name = N'inputDataSet'    
 , @output_data_1_name = N'outputDataSet'    
 WITH RESULT SETS((C1 int, C2 varchar(max), C3 varchar(max), C4 float));  
```

**結果**

|資料列 \#|C1|C2|C3|C4|
|-|-|-|-|-|
|1|1|您好|6e225611-4b58-4995-a0a5-554d19012ef1|4|
|2|-11|world|6732ea46-2d5d-430b-8ao1-86e7f3351c3e|2|

請注意，在 R 中使用 `str` 函數可取得輸出資料的結構描述。 此函數傳回下列資訊：

```output
'data.frame':2 obs. of  4 variables:
 $ c1: int  1 -11
 $ c2: Factor w/ 2 levels "Hello","world": 1 2
 $ c3: Factor w/ 2 levels "6732EA46-2D5D-430B-8A01-86E7F3351C3E",..: 2 1
 $ cR: num  4 2
```

從這裡開始，您可以看到下列資料類型轉換會與這項查詢一起以隱含方式執行：

+ **資料行 C1**。 資料行在 **ssNoversion** 中會表示為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，在 R 中會表示為 `integer` 而在輸出結果集中則為 **ssNoversion** 。  
  
  未執行任何類型轉換。  
  
+ **資料行 C2**。 資料行在 **ssNoversion** 中會表示為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，在 R 中會表示為 `factor` 而在輸出結果集中則為 **varchar(max)** 。  
  
  請注意輸出的變更方式；來自 R 的任何字串 (因素或一般字串) 不管字串的長度為何，皆會以 **varchar(max)** 表示。  
  
+ **資料行 C3**。  資料行在 **ssNoversion** 中會表示為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，在 R 中會表示為 `character` 而在輸出結果集中則為 **varchar(max)** 。
  
  請注意所發生的資料類型轉換。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支援 **ssNoversion** ，但 R 則否，因此識別項會表示為字串。
  
+ **資料行 C4**。 資料行包含由 R 指令碼產生且不存在於原始資料的值。


## <a name="example-2-dynamic-column-selection-using-r"></a>範例 2：使用 R 進行動態資料行選取

以下範例示範如何使用 R 程式碼來檢查無效的資料行類型。 程式碼會使用 SQL Server 系統檢視來取得指定資料表的結構描述，並移除任何具有指定無效類型的資料行。

```R
connStr <- "Server=.;Database=TestDB;Trusted_Connection=Yes"
data <- RxSqlServerData(connectionString = connStr, sqlQuery = "SELECT COLUMN_NAME FROM TestDB.INFORMATION_SCHEMA.COLUMNS WHERE TABLE_NAME = N'testdata' AND DATA_TYPE <> 'image';")
columns <- rxImport(data)
columnList <- do.call(paste, c(as.list(columns$COLUMN_NAME), sep = ","))
sqlQuery <- paste("SELECT", columnList, "FROM testdata")
```

## <a name="see-also"></a>另請參閱

+ [Python 與 SQL Server 之間的資料類型對應](../python/python-libraries-and-data-types.md)
