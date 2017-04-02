---
title: "使用 R 資料類型 | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "01/31/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 5df99e1c-a89a-42c1-9d68-ffe8d9577c94
caps.latest.revision: 16
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 12
---
# 使用 R 資料類型
  而 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支援幾種數十個資料類型，R 具有有限的純量資料類型 (數字的整數，複雜的邏輯，字元日期/時間和 raw)。 因此，當您在 R 指令碼中使用  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的資料時，可能會出現下列幾項差異：  
  
-   資料會以隱含方式轉換成相容的資料類型。  
  
-   無法以隱含方式轉換資料時，則會傳回錯誤。  
  
 一般而言，當您不清楚如何在 R 中使用特定的資料類型或資料結構時，皆可使用  `str()` 函數以取得 R 物件的內部結構和類型。 函數的結果會列印到 R 主控台，也會顯示在 **的 [訊息]**[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]索引標籤查詢結果中。  
  
 如果特定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] R、 不支援資料類型，但您需要在 R 指令碼中使用的資料行，我們建議您使用 [CAST 和 CONVERT & #40。TRANSACT-SQL & #41;](../../t-sql/functions/cast-and-convert-transact-sql.md) 如預期般在 R 指令碼中使用資料之前，會執行函式，以確保資料型別轉換。  
  
 如需詳細資訊 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料類型，請參閱 [資料類型 & #40。TRANSACT-SQL & #41;](../../t-sql/data-types/data-types-transact-sql.md)  
  
## R 與 SQL Server 之間的資料類型轉換  
 下表顯示在 R 指令碼中使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的資料，然後傳回給 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]時，資料類型和值的變更。  
  
|||||  
|-|-|-|-|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 類型|R 類別|輸入 **RESULT SET**|註解|  
|**smalldatetime**|`POSIXct`|**datetime**|以 GMT 來表示|  
|**smallmoney**|`numeric`|**float**||  
|**datetime**|`POSIXct`|**datetime**|以 GMT 來表示|  
|**money**|`numeric`|**float**||  
|**uniqueidentifier**|`character`|**varchar(max)**||  
|**numeric(p,s)**|`numeric`|**float**||  
|**decimal(p,s)**|`numeric`|**float**||  
|**date**|`POSIXct`|**datetime**|以 GMT 來表示|  
|**tinyint**|`integer`|**int**||  
|**bit**|`logical`|**bit**||  
|**smallint**|`integer`|**int**||  
|**int**|`integer`|**int**||  
|**float**|`numeric`|**float**||  
|**real**|`numeric`|**float**||  
|**bigint**|`numeric`|**float**||  
|**binary(n)**<br /><br /> n <= 8000|`raw`|**varbinary(max)**|只允許作為輸入參數和輸出|  
|**char(n)**<br /><br /> n <= 8000|`character`|**varchar(max)**||  
|**varbinary （n)**<br /><br /> n <= 8000|`raw`|**varbinary(max)**|只允許作為輸入參數和輸出|  
|**varchar （n)**<br /><br /> n <= 8000|`character`|**varchar(max)**||  
|**varbinary(max)**|`raw`|**varbinary(max)**|只允許作為輸入參數和輸出|  
  
## 資料類型轉換範例  
 下列查詢會取得一系列的值從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表，並使用預存程序  [sp_execute_external_script & #40。TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) 輸出使用 R 執行階段值。  
  
```  
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
  
```  
'data.frame':2 obs. of  4 variables:   
 $ c1: int  1 -11   
 $ c2: Factor w/ 2 levels "Hello","world": 1 2   
 $ c3: Factor w/ 2 levels "6732EA46-2D5D-430B-8A01-86E7F3351C3E",..: 2 1   
 $ cR: num  4 2  
```  
  
 從這裡開始，您可以看到下列資料類型轉換會與這項查詢一起以隱含方式執行：  
  
-   **資料行 C1**。 資料行表示為 **int** 中 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ，`integer` R、 中和 **int** 輸出結果集中。  
  
     未執行任何類型轉換。  
  
-   **資料行 C2**。 資料行表示為 **varchar （10)** 中 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ，`factor` R、 中和 **varchar （max)** 在輸出中。  
  
     請注意輸出如何變更。從 R （因素或規則的字串） 的任何字串將呈現為 **varchar （max)**, ，不管字串的長度為何。  
  
-   **資料行 C3**。  資料行表示為 **uniqueidentifier** 中 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ，`character` R、 中和 **varchar （max)** 在輸出中。  
  
     請注意所發生的資料類型轉換。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支援 **uniqueidentifier** 但 R 不; 因此，識別項會表示為字串。  
  
-   **資料行 C4**。 資料行包含由 R 指令碼產生且不存在於原始資料的值。  
 
 ## 另請參閱
 [SQL Server R 服務功能及工作](../../advanced-analytics/r-services/sql-server-r-services-features-and-tasks.md)
  
  