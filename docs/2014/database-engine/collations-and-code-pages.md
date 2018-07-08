---
title: Collations and Code Pages |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: c626dcac-0474-432d-acc0-cfa643345372
caps.latest.revision: 15
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 0632bb70a18930e71319554bba99b0660e986483
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37182889"
---
# <a name="collations-and-code-pages"></a>定序和字碼頁
  [!INCLUDE[hek_2](../includes/hek-2-md.md)] 對於記憶體最佳化的資料表中 (var)Char 資料行支援的字碼頁以及用於索引和原生編譯預存程序中支援的定序有一些限制。  
  
 (var)char 值的字碼頁會判斷字元與資料表中儲存的位元組表示法之間的對應。 例如，在 Windows Latin 1 字碼頁 (也就是 1252；[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 預設值) 中，字元 'a' 對應到 0x61 位元組。  
  
 (var)char 值的字碼頁是由與這個值相關的定序所決定。 例如，SQL_Latin1_General_CP1_CI_AS 定序有相關聯的字碼頁 1252。  
  
 值的定序可能是從資料庫定序繼承而來，也可能是使用 COLLATE 關鍵字明確指定。 如果資料庫包含記憶體最佳化資料表或原生編譯預存程序，則資料庫定序無法變更。 下列範例會設定資料庫定序及建立資料表，該資料表的資料行有不同的定序。 資料庫使用不區分大小寫的 Latin 定序。  
  
 只有當索引使用 BIN2 定序時，才能建立於字串資料行中。 LastName 變數會使用 BIN2 定序。 FirstName 會使用資料庫預設值，也就是 CI_AS (不區分大小寫、區分腔調字)。  
  
> [!IMPORTANT]  
>  您無法針對不使用 BIN2 定序的索引字串資料行使用排序依據或群組依據。  
  
```tsql  
CREATE DATABASE IMOLTP  
  
ALTER DATABASE IMOLTP ADD FILEGROUP IMOLTP_mod CONTAINS MEMORY_OPTIMIZED_DATA  
ALTER DATABASE IMOLTP ADD FILE( NAME = 'IMOLTP_mod' , FILENAME = 'c:\data\IMOLTP_mod') TO FILEGROUP IMOLTP_mod;  
--GO  
  
--  set the database collations  
ALTER DATABASE IMOLTP COLLATE Latin1_General_100_CI_AS  
GO  
  
--  
USE IMOLTP   
GO  
  
-- create a table with collation  
CREATE TABLE Employees (  
  EmployeeID int NOT NULL ,   
  LastName nvarchar(20) COLLATE Latin1_General_100_BIN2 NOT NULL INDEX IX_LastName NONCLUSTERED,   
  FirstName nvarchar(10) NOT NULL ,  
  CONSTRAINT PK_Employees PRIMARY KEY NONCLUSTERED HASH(EmployeeID)  WITH (BUCKET_COUNT=1024)  
) WITH (MEMORY_OPTIMIZED=ON, DURABILITY=SCHEMA_AND_DATA)  
GO  
```  
  
 記憶體最佳化的資料表和原生編譯的預存程序會套用以下限制：  
  
-   記憶體最佳化資料表中的 (var)char 資料行必須使用字碼頁 1252 定序。 這項限制並不適用於 n(var)char 資料行。 下列程式碼會擷取所有 1252 定序：  
  
    ```tsql  
    -- all supported collations for (var)char columns in memory-optimized tables  
    select * from sys.fn_helpcollations()  
    where collationproperty(name, 'codepage') = 1252;  
    ```  
  
     如果您需要儲存非拉丁字元，請使用 n(var)char 資料行。  
  
-   (n)(var)char 資料行上的索引只能使用 BIN2 定序來指定 (請參閱第一個範例)。 下列查詢會擷取所有支援的 BIN2 定序：  
  
    ```tsql  
    -- all supported collations for indexes on memory-optimized tables and   
    -- comparison/sorting in natively compiled stored procedures  
    select * from sys.fn_helpcollations() where name like '%BIN2'  
    ```  
  
     如果您透過解譯的 [!INCLUDE[tsql](../includes/tsql-md.md)] 存取資料表，您可以使用 `COLLATE` 關鍵字來透過運算式或排序作業變更定序。 請參閱最後一個範例當做這個情況的範例。  
  
-   如果資料庫定序不是字碼頁 1252 定序，則原生編譯預存程序無法使用 (var)char 類型的參數、區域變數或字串常數。  
  
-   原生編譯的預存程序中的所有運算式和排序作業都必須使用 BIN2 定序。 其含意為，所有的比較與排序作業都是根據字元的 Unicode 字碼指標 (二進位表示法)。 例如，所有排序都區分大小寫 ('Z' 排列在 'a' 之前)。 如有需要，請使用解譯的 [!INCLUDE[tsql](../includes/tsql-md.md)] 進行不區分大小寫的排序和比較。  
  
-   原生編譯的預存程序中不支援 UTF-16 資料截斷。 這表示該 n (var) char (*n*) 的值無法轉換成 n (var) char 類型 (*我*)，如果*我* < *n*的話定序具有 _SC 屬性。 例如，以下範例不受支援：  
  
    ```tsql  
    -- column definition using an _SC collation  
     c2 nvarchar(200) collate Latin1_General_100_CS_AS_SC not null   
    -- assignment to a smaller variable, requiring truncation  
     declare @c2 nvarchar(100) = '';  
     select @c2 = c2  
    ```  
  
     字串操作函數，例如 LEN、SUBSTRING、LTRIM 和具有 UTF-16 資料的 RTRIM，在原生方式編譯預存程序中都不受支援。 您無法對有 _SC 定序的 n(var)char 值使用這些字串操作函數。  
  
     使用大到足以避免截斷的類型來宣告變數。  
  
 下列範例顯示 In-Memory OLTP 中定序限制的部分影響及因應措施。 此範例使用上面指定的 Employees 資料表。 此範例會列出所有員工。 請注意在 LastName 中，因為使用二進位定序，所以大寫名稱會排在小寫前面。 因此，'Thomas' 會排在 'nolan' 前面，因為大寫字母具有較低的字碼指標。 FirstName 具有不區分大小寫的定序。 因此，排序是根據英文字母，而不是字元的字碼指標。  
  
```tsql  
-- insert a number of values  
INSERT Employees VALUES (1,'thomas', 'john')  
INSERT Employees VALUES (2,'Thomas', 'rupert')  
INSERT Employees VALUES (3,'Thomas', 'Jack')  
INSERT Employees VALUES (4,'Thomas', 'annie')  
INSERT Employees VALUES (5,'nolan', 'John')  
GO  
  
-- ===========  
SELECT EmployeeID, LastName, FirstName FROM Employees  
ORDER BY LastName, FirstName  
GO  
  
-- ===========  
-- specify collation: sorting uses case-insensitive collation, thus 'nolan' comes before 'Thomas'  
SELECT * FROM Employees  
ORDER BY LastName COLLATE Latin1_General_100_CI_AS, FirstName  
GO  
  
-- ===========  
-- retrieve employee by Name  
-- must use BIN2 collation for comparison in natively compiled stored procedures  
CREATE PROCEDURE usp_EmployeeByName @LastName nvarchar(20), @FirstName nvarchar(10)  
WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
AS BEGIN ATOMIC WITH   
(  TRANSACTION ISOLATION LEVEL = SNAPSHOT,  
  LANGUAGE = N'us_english'  
)  
  SELECT EmployeeID, LastName, FirstName FROM dbo.Employees  
  WHERE   
    LastName = @LastName AND  
    FirstName COLLATE Latin1_General_100_BIN2 = @FirstName  
  
END  
GO  
  
-- this does not return any rows, as EmployeeID 1 has first name 'john', which is not equal to 'John' in a binary collation  
EXEC usp_EmployeeByName 'thomas', 'John'  
  
-- this retrieves EmployeeID 1  
EXEC usp_EmployeeByName 'thomas', 'john'  
```  
  
## <a name="see-also"></a>另請參閱  
 [記憶體內部 OLTP &#40;記憶體內部最佳化&#41;](../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
