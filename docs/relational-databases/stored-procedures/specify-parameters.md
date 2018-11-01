---
title: 指定參數 | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.technology: stored-procedures
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- parameters [SQL Server], stored procedures
- stored procedures [SQL Server], parameters
- output parameters [SQL Server]
- input parameters [SQL Server]
ms.assetid: 902314fe-5f9c-4d0d-a0b7-27e67c9c70ec
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 42db9954a071865124d443be32203fc284dfe699
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47838956"
---
# <a name="specify-parameters"></a>指定參數
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  藉由指定程序參數，呼叫端程式就能夠將值傳入程序的主體。 這些值在程序執行期間可用於各種用途。 如果程序參數標示為 OUTPUT 參數，程序參數也可以將值傳回給呼叫端程式。  
  
 程序最多可以有 2100 個參數，每個參數各被指派名稱、資料類型和方向。 您可以選擇性指派預設值給參數。  
  
 下節提供有關傳遞值至參數，以及在程序呼叫期間如何使用每個參數屬性的詳細資訊。  
  
## <a name="passing-values-into-parameters"></a>將值傳遞至參數  
 以程序呼叫提供的參數值必須是常數或變數，函數名稱不可做為參數值。 變數可以是使用者定義的變數或系統變數，如 \@\@spid。  
  
 下列範例示範傳遞參數值至 `uspGetWhereUsedProductID`程序。 這些範例說明如何以常數和變數方式傳遞參數，以及如何使用變數傳遞函數值。  
  
```  
USE AdventureWorks2012;  
GO  
-- Passing values as constants.  
EXEC dbo.uspGetWhereUsedProductID 819, '20050225';  
GO  
-- Passing values as variables.  
DECLARE @ProductID int, @CheckDate datetime;  
SET @ProductID = 819;  
SET @CheckDate = '20050225';  
EXEC dbo.uspGetWhereUsedProductID @ProductID, @CheckDate;  
GO  
-- Try to use a function as a parameter value.  
-- This produces an error message.  
EXEC dbo.uspGetWhereUsedProductID 819, GETDATE();  
GO  
-- Passing the function value as a variable.  
DECLARE @CheckDate datetime;  
SET @CheckDate = GETDATE();  
EXEC dbo.uspGetWhereUsedProductID 819, @CheckDate;  
GO  
```  
  
## <a name="specifying-parameter-names"></a>指定參數名稱  
 建立程序及宣告參數名稱時，參數名稱必須以一個 \@ 字元開始，而且在程序範圍中必須是唯一的。  
  
 明確為參數命名以及在程序呼叫中指定適當值給每個參數，就能以任何順序提供參數。 例如，如果 **my_proc** 程序預期有三個參數，名稱分別為 **\@first**、**\@second** 和 **\@third**，您可以將傳遞給程序的值指派給參數名稱，例如：`EXECUTE my_proc @second = 2, @first = 1, @third = 3;`  
  
> [!NOTE]  
>  如果以 **\@parameter =**_value_ 形式提供一個參數值，則所有後續的參數就必須按照此方式來提供。 如果不是以 **\@parameter =**_value_ 形式傳遞參數值，則提供值的順序就必須與 CREATE PROCEDURE 陳述式中列出參數的順序一樣 (由左到右)。  
  
> [!WARNING]  
>  任何以 **\@parameter =**_value_ 形式傳遞的參數若有拼字錯誤，就會讓 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 產生錯誤，並導致程序無法執行。  
  
## <a name="specifying-parameter-data-types"></a>指定參數資料類型  
 在 CREATE PROCEDURE 陳述式中宣告時，參數必須定義一種資料類型。 參數的資料類型將決定在呼叫程序時參數可接受的值類型和範圍。 例如，若將參數定義為 **tinyint** 資料類型，在傳遞數值至該參數時，只能接受 0 到 255 範圍內的數值。 執行程序時，如果值與資料類型不相容的話，就會傳回錯誤。  
  
## <a name="specifying-parameter-default-values"></a>指定參數預設值  
 如果在宣告時，已指定參數的預設值，此參數視為選擇性參數。 在程序呼叫中，不需要提供值給選擇性參數。  
  
 在下列情況下會使用參數的預設值：  
  
-   在程序呼叫中未指定參數值。  
  
-   程序呼叫中指定 DEFAULT 關鍵字做為值。  
  
> [!NOTE]  
>  如果預設值是包含內嵌空白或標點的字串，或是以數字開頭 (例如 6xxx)，就必須將它括在單引號中。  
  
 如果無法指定適當的數值做為參數的預設值，您可以指定 NULL 做為預設值。 在沒有參數值的狀況下執行程序時，最好讓程序傳回自訂的訊息  
  
 下列範例使用一個輸入參數 `uspGetSalesYTD` 來建立 `@SalesPerson`程序。 NULL 做為預設值指派給參數，並用於錯誤處理陳述式，以便在未指定值給 `@SalesPerson` 參數而執行程序時，傳回自訂錯誤訊息。  
  
```  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID('Sales.uspGetSalesYTD', 'P') IS NOT NULL  
    DROP PROCEDURE Sales.uspGetSalesYTD;  
GO  
CREATE PROCEDURE Sales.uspGetSalesYTD  
@SalesPerson nvarchar(50) = NULL  -- NULL default value  
AS   
    SET NOCOUNT ON;   
  
-- Validate the @SalesPerson parameter.  
IF @SalesPerson IS NULL  
BEGIN  
   PRINT 'ERROR: You must specify the last name of the sales person.'  
   RETURN  
END  
-- Get the sales for the specified sales person and   
-- assign it to the output parameter.  
SELECT SalesYTD  
FROM Sales.SalesPerson AS sp  
JOIN HumanResources.vEmployee AS e ON e.BusinessEntityID = sp.BusinessEntityID  
WHERE LastName = @SalesPerson;  
RETURN  
GO  
  
```  
  
 下列範例執行此程序。 第一個陳述式會在不指定輸入值的情況下執行程序。 這將造成程序中的錯誤處理陳述式傳回自訂錯誤訊息。 第二個陳述式則提供輸入值並傳回預期的結果集。  
  
```  
-- Run the procedure without specifying an input value.  
EXEC Sales.uspGetSalesYTD;  
GO  
-- Run the procedure with an input value.  
EXEC Sales.uspGetSalesYTD N'Blythe';  
GO  
```  
  
 雖然可以省略已提供預設值的參數，但只能截斷參數清單。 例如，如果程序有五個參數，第四個和第五個參數可以省略。 但除非是以 **\@parameter =**_value_ 形式提供參數，否則只要包含第五個參數，就不能省略第四個參數。  
  
## <a name="specifying-parameter-direction"></a>指定參數方向  
 參數的方向可以是輸入或輸出，前者指將值傳入程序的主體，後者則指程序傳回值給呼叫端程式。 預設是輸入參數。  
  
 若要指定輸出參數，必須在 CREATE PROCEDURE 陳述式的參數定義中指定 OUTPUT 關鍵字。 程序結束時，會將輸出參數目前的值傳回給呼叫端程式。 呼叫端程式在執行程序時，也必須使用 OUTPUT 關鍵字，才能將參數值儲存在變數中，供呼叫端程式使用。  
  
 下列範例會建立 `Production.usp_GetList` 程序，以傳回價格不超過指定金額的產品清單。 此範例顯示使用多個 SELECT 陳述式和多個 OUTPUT 參數。 OUTPUT 參數可以讓外部程序、批次或一個以上的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式在程序執行過程中存取某一值集。  
  
```  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID ( 'Production.uspGetList', 'P' ) IS NOT NULL   
    DROP PROCEDURE Production.uspGetList;  
GO  
CREATE PROCEDURE Production.uspGetList @Product varchar(40)   
    , @MaxPrice money   
    , @ComparePrice money OUTPUT  
    , @ListPrice money OUT  
AS  
    SET NOCOUNT ON;  
    SELECT p.[Name] AS Product, p.ListPrice AS 'List Price'  
    FROM Production.Product AS p  
    JOIN Production.ProductSubcategory AS s   
      ON p.ProductSubcategoryID = s.ProductSubcategoryID  
    WHERE s.[Name] LIKE @Product AND p.ListPrice < @MaxPrice;  
-- Populate the output variable @ListPprice.  
SET @ListPrice = (SELECT MAX(p.ListPrice)  
        FROM Production.Product AS p  
        JOIN  Production.ProductSubcategory AS s   
          ON p.ProductSubcategoryID = s.ProductSubcategoryID  
        WHERE s.[Name] LIKE @Product AND p.ListPrice < @MaxPrice);  
-- Populate the output variable @compareprice.  
SET @ComparePrice = @MaxPrice;  
GO  
  
```  
  
 執行 `usp_GetList` 以傳回成本低於 $700 的 [!INCLUDE[ssSampleDBCoShort](../../includes/sssampledbcoshort-md.md)] 產品 (自行車) 清單。 OUTPUT 參數 **\@cost** 和 **\@compareprices** 會搭配流程控制語言使用，以便在 [訊息] 視窗中傳回訊息。  
  
> [!NOTE]  
>  在建立程序過程以及在使用變數過程中，必須定義 OUTPUT 變數。 參數名稱和變數名稱不一定要相符。 但是，資料類型和參數定位必須相符 (除非使用 **\@listprice=** *variable*)。  
  
```  
DECLARE @ComparePrice money, @Cost money ;  
EXECUTE Production.uspGetList '%Bikes%', 700,   
    @ComparePrice OUT,   
    @Cost OUTPUT  
IF @Cost <= @ComparePrice   
BEGIN  
    PRINT 'These products can be purchased for less than   
    $'+RTRIM(CAST(@ComparePrice AS varchar(20)))+'.'  
END  
ELSE  
    PRINT 'The prices for all products in this category exceed   
    $'+ RTRIM(CAST(@ComparePrice AS varchar(20)))+'.';  
  
```  
  
 部分結果集如下：  
  
```  
Product                                            List Price  
-------------------------------------------------- ------------------  
Road-750 Black, 58                                 539.99  
Mountain-500 Silver, 40                            564.99  
Mountain-500 Silver, 42                            564.99  
...  
Road-750 Black, 48                                 539.99  
Road-750 Black, 52                                 539.99  
  
(14 row(s) affected)  
  
These items can be purchased for less than $700.00.  
```  
  
## <a name="see-also"></a>另請參閱  
 [CREATE PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/create-procedure-transact-sql.md)  
  
  
