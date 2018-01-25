---
title: "使用 R 資料類型 | Microsoft Docs"
ms.custom: SQL2016_New_Updated
ms.date: 01/31/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 5df99e1c-a89a-42c1-9d68-ffe8d9577c94
caps.latest.revision: "16"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 14bfba68925f357c39fc192ae7852055a7e91f4f
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="r-libraries-and-r-data-types"></a>R 程式庫和 R 資料類型

本主題會描述所包含的 R 程式庫和資料類型所支援的下列產品：

+ SQL Server 2016 R 服務 （資料庫）
+ SQL Server 機器學習服務 （資料庫）

本主題也會列出不支援的資料類型和清單的資料類型轉換的 R 與 SQL Server 之間傳遞資料時可能會隱含地執行。

## <a name="r-libraries"></a>R 程式庫

R 服務和機器學習服務使用 R，這兩種產品與特定版本的 Microsoft R Open 對齊。 例如，最新版本中，SQL Server 2017 機器學習服務，根據 Microsoft R Open 3.3.3。

若要檢視 SQL Server 的特定執行個體相關聯的 R 版本，請開啟 RGui。

1. 預設執行個體中，路徑就是，如下所示：`C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\bin\x64\`
2. 顯示訊息列出 R 散發和 Microsoft R Open 的版本號碼。

若要尋找包含特定版本的 Microsoft R Server 中的 R 版本，請參閱[R 伺服器-What's New](https://msdn.microsoft.com/microsoft-r/rserver-whats-new#new-and-updated-packages)。

請注意，SQL Server 中的封裝管理系統表示多個版本的 R 封裝可以安裝在相同的電腦上，具有多個使用者共用相同的封裝，或使用不同版本的相同的封裝。 如需詳細資訊，請參閱[SQL Server 中的 R 封裝管理](../r/r-package-management-for-sql-server-r-services.md)。

## <a name="r-and-sql-data-types"></a>R 和 SQL 資料類型

而[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]支援數個數十種資料類型，R 具有有限的純量資料類型 (數字、 整數、 複雜、 邏輯、 字元、 日期/時間和 raw)。 如此一來，每當您使用的資料[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]在 R 指令碼，資料可能會隱含地轉換成相容的資料類型。 不過，通常完全無法執行轉換，並傳回錯誤，例如 「 未處理的 SQL 資料類型 」。

此區段會列出所提供，並列出不支援的資料類型的隱含轉換。 以對應 R 與 SQL Server 之間的資料類型提供的一些指導方針。

## <a name="implicit-data-type-conversions-between-r-and-sql-server"></a>R 與 SQL Server 之間的隱含資料類型轉換

下表顯示在 R 指令碼中使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的資料，然後傳回給 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]時，資料類型和值的變更。

|SQL 類型|R 類別|RESULT SET 類型|註解|
|-|-|-|-|
|**bigint**|`numeric`|**float**||
|**binary(n)**<br /><br /> n <= 8000|`raw`|**varbinary(max)**|只允許作為輸入參數和輸出|
|**bit**|`logical`|**bit**||
|**char(n)**<br /><br /> n <= 8000|`character`|**varchar(max)**||
|**datetime**|`POSIXct`|**datetime**|以 GMT 來表示|
|**date**|`POSIXct`|**datetime**|以 GMT 來表示|
|**decimal(p,s)**|`numeric`|**float**||
|**float**|`numeric`|**float**||
|**int**|`integer`|**int**||
|**money**|`numeric`|**float**||
|**numeric(p,s)**|`numeric`|**float**||
|**real**|`numeric`|**float**||
|**smalldatetime**|`POSIXct`|**datetime**|以 GMT 來表示|
|**smallint**|`integer`|**int**||
|**smallmoney**|`numeric`|**float**||
|**tinyint**|`integer`|**int**||
|**uniqueidentifier**|`character`|**varchar(max)**||
|**varbinary(n)**<br /><br /> n <= 8000|`raw`|**varbinary(max)**|只允許作為輸入參數和輸出|
|**varbinary(max)**|`raw`|**varbinary(max)**|只允許作為輸入參數和輸出|
|**varchar(n)**<br /><br /> n <= 8000|`character`|**varchar(max)**||


## <a name="data-types-not-supported-by-r"></a>R 不支援的資料類型

在 [SQL Server 類型系統](../../t-sql/data-types/data-types-transact-sql.md)所支援的資料類型類別中，以下幾個類型在傳遞到 R 程式碼時很有可能會造成問題：

+ 中所列的資料類型**其他**SQL 類型系統主題的章節：**游標**，**時間戳記**， **hierarchyid**， **uniqueidentifier**， **sql_variant**， **xml**，**資料表**
+ 所有空間類型
+ **image**

## <a name="data-types-that-might-convert-poorly"></a>轉換效果可能不佳的資料類型

+ 除了 **datetimeoffset** 之外，大部分的 datetime 類型應該都能順利運作 
+ 支援大部分的數值資料類型，但 **money** 和 **smallmoney** 的轉換可能會失敗
+ 支援 **varchar**，但由於 SQL Server 一般使用 Unicode，因此建議您盡可能使用 **nvarchar** 及其他 Unicode 文字資料類型。
+ 來自 RevoScaleR 函數庫且具有 rx 前置詞的函數，可以處理 SQL 二進位資料類型 (**binary** 和 **varbinary**)，但在大部分案例中，這些類型都需要特別處理。 大部分的 R 程式碼都無法搭配二進位資料行使用。

  
 如需 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型的詳細資訊，請參閱[資料類型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)

## <a name="changes-in-data-types-between-sql-server-2016-and-earlier-versions"></a>SQL Server 2016 與舊版之間的資料類型變更

Microsoft SQL Server 2016 和 Microsoft Azure SQL Database 包含資料類型轉換和幾個其他作業的改進。 這些改進大部分都為處理浮點數類型提供更高的精確度，以及對傳統 **datetime** 類型的作業做出次要變更。

當您使用 130 或更高的資料庫相容性層級時，這些改進預設都可供使用。 不過，如果您使用不同的相容性層級，或使用較舊版本連線到資料庫，則可能會看見不同的數值精確度或其他結果。 

如需詳細資訊，請參閱[處理某些資料類型和不常見作業的 SQL Server 2016 改進 (機器翻譯)](https://support.microsoft.com/help/4010261/sql-server-2016-improvements-in-handling-some-data-types-and-uncommon-)。
 

## <a name="verify-r-and-sql-data-schemas-in-advance"></a>預先驗證 R 和 SQL 資料結構描述 

一般而言，當您不清楚如何在 R 中使用特定的資料類型或資料結構時，皆可使用  `str()` 函數以取得 R 物件的內部結構和類型。 函數的結果會列印到 R 主控台，也會顯示在 **的 [訊息]**[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]索引標籤查詢結果中。 

當您從資料庫擷取要用於 R 程式碼的資料時，應該一律刪除無法用於 R 的資料行，以及其他對於分析沒有幫助的資料行，例如 GUIDS (Uniqueidentifier)、時間戳記和其他用於稽核的資料行，或是由 ETL 處理序建立的歷程資訊。 

請注意，包含不必要的資料行可能會大幅降低 R 程式碼的效能，尤其是使用高基數資料行做為因素的時候。 因此，我們建議您事先使用 SQL Server 系統預存程序和資訊檢視取得特定資料表的資料類型，並刪除或轉換不相容的資料行。 如需詳細資訊，請參閱 [Transact-SQL 中的資訊結構描述檢視](../../relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)

如果 R 不支援特定的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型，但您需要在 R 指令碼中使用該資料的數個資料行，建議您先使用 [CAST 和 CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md) 函數，以確保資料類型轉換會如預期般地執行，再於 R 指令碼中使用該資料。  

> [!WARNING]
如果您在移動資料時使用 **rxDataStep** 來卸除不相容的資料行，請留意 **RxSqlServerData** 資料來源類型不支援引數 _varsToKeep_ 和 _varsToDrop_。


## <a name="examples"></a>範例

### <a name="example-1-implicit-conversion"></a>範例 1︰隱含轉換

以下範例示範資料在 SQL Server 和 R 之間進行來回行程時的轉換方式。

查詢會取得一系列的值從[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料表，並使用預存程序[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)輸出使用 R 執行階段值。

```SQL
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

||||||
|-|-|-|-|-|
||C1|C2|C3|C4|
|1|1|Hello|6e225611-4b58-4995-a0a5-554d19012ef1|4|
|1|-11|world|6732ea46-2d5d-430b-8ao1-86e7f3351c3e|2|

請注意，在 R 中使用 `str` 函數可取得輸出資料的結構描述。 此函數傳回下列資訊：

<code>'data.frame':2 obs. of  4 variables:</code>
<code> $ c1: int  1 -11</code>
<code> $ c2: Factor w/ 2 levels "Hello","world": 1 2</code>
<code> $ c3: Factor w/ 2 levels "6732EA46-2D5D-430B-8A01-86E7F3351C3E",..: 2 1</code>
<code> $ cR: num  4 2</code>

從這裡開始，您可以看到下列資料類型轉換會與這項查詢一起以隱含方式執行：

-   **資料行 C1**。 資料行在 **ssNoversion** 中會表示為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，在 R 中會表示為 `integer` 而在輸出結果集中則為 **ssNoversion** 。  
  
     未執行任何類型轉換。  
  
-   **資料行 C2**。 資料行在 **ssNoversion** 中會表示為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，在 R 中會表示為 `factor` 而在輸出結果集中則為 **varchar(max)** 。  
  
     請注意輸出的變更方式；來自 R 的任何字串 (因素或一般字串) 不管字串的長度為何，皆會以 **varchar(max)**表示。  
  
-   **資料行 C3**。  資料行在 **ssNoversion** 中會表示為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，在 R 中會表示為 `character` 而在輸出結果集中則為 **varchar(max)** 。
  
     請注意所發生的資料類型轉換。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支援 **ssNoversion** ，但 R 則否，因此識別項會表示為字串。
  
-   **資料行 C4**。 資料行包含由 R 指令碼產生且不存在於原始資料的值。


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

[Python 程式庫和資料類型](../python/python-libraries-and-data-types.md)
