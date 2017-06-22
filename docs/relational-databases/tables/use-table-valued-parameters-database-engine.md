---
title: "使用資料表值參數 (Database Engine) | Microsoft 文件"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-tables
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- table-valued parameters
- table-valued parameters, about table-valued parameters
- parameters [SQL Server], table-valued
- TVP See table-valued parameters
ms.assetid: 5e95a382-1e01-4c74-81f5-055612c2ad99
caps.latest.revision: 31
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 021177aa350c47474e48453f7d9a5735e1083b04
ms.contentlocale: zh-tw
ms.lasthandoff: 06/22/2017

---
# <a name="use-table-valued-parameters-database-engine"></a>使用資料表值參數 (Database Engine)
[!INCLUDE[tsql-appliesto-ss2016-all_md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  資料表值參數是藉由使用使用者定義的資料表類型來進行宣告。 您可以使用資料表值參數，將多個資料列傳送到 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式或常式 (如預存程序或函數)，而不需要建立暫存資料表或許多參數。  
  
 資料表值參數就像是 OLE DB 和 ODBC 中的參數陣列，但是提供了更多的彈性，而且與 [!INCLUDE[tsql](../../includes/tsql-md.md)]更緊密整合在一起。 資料表值參數也會因為能夠參與以集合為基礎的作業而獲益。  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 會以傳址方式將資料表值參數傳遞給常式，以免產生輸入資料的複本。 您可以使用資料表值參數來建立及執行 [!INCLUDE[tsql](../../includes/tsql-md.md)] 常式，然後從 [!INCLUDE[tsql](../../includes/tsql-md.md)] 程式碼 (任何 Managed 語言中的 Managed 和原生用戶端) 呼叫這些常式。  
  
 **本主題內容：**  
  
 [優點](#Benefits)  
  
 [限制](#Restrictions)  
  
 [資料表值參數與BULK INSERT 作業的比較](#BulkInsert)  
  
 [範例](#Example)  
  
##  <a name="Benefits"></a> 優點  
 資料表值參數的範圍為預存程序、函數或動態 [!INCLUDE[tsql](../../includes/tsql-md.md)] 文字，與其他參數一模一樣。 同樣地，資料表類型之變數的範圍與使用 DECLARE 陳述式建立的其他任何區域變數一樣。 您可以在動態 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式內宣告資料表值變數，並將這些變數當做資料表值參數傳遞給預存程序和函數。  
  
 資料表值參數提供更大的彈性，而且在某些情況下，其效能優於暫存資料表或是傳遞參數清單的其他方法。 資料表值參數提供下列好處：  
  
-   不需要從用戶端鎖定初始資料母體。  
  
-   提供簡單的程式設計模型。  
  
-   可讓您將複雜的商務邏輯併入單一常式內。  
  
-   減少與伺服器之間的往返次數。  
  
-   可以有一個不同基數的資料表結構。  
  
-   具有強型別。  
  
-   可讓用戶端指定排序次序和唯一索引鍵。  
  
-   在預存程序中使用時，會像暫存資料表一樣被快取。 從 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]開始，也會為參數化查詢快取資料表值參數。  
  
##  <a name="Restrictions"></a> 限制  
 資料表值參數有下列限制：  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不會維護資料表值參數之資料行上的統計資料。  
  
-   資料表值參數必須當做輸入 READONLY 參數傳遞給 [!INCLUDE[tsql](../../includes/tsql-md.md)] 常式。 您不能在常式主體內針對資料表值參數執行 DML 作業，例如 UPDATE、DELETE 或 INSERT。  
  
-   您不能使用資料表值參數當做 SELECT INTO 或 INSERT EXEC 陳述式的目標。 資料表值參數可以在 SELECT INTO 的 FROM 子句中或是 INSERT EXEC 字串或預存程序內。  
  
##  <a name="BulkInsert"></a> 資料表值參數與BULK INSERT 作業的比較  
 使用資料表值參數可以和使用以集合為基礎之變數的其他方式相比較；但是，對於大型資料集而言，使用資料表值參數通常可以更快速。 與大量作業 (其啟動成本高於資料表值參數) 相較之下，當插入 1000 個以下的資料列時，資料表值參數會有很不錯的執行效能。  
  
 重複使用的資料表值參數會因為暫存資料表快取而獲益。 這種資料表快取提供了比同等的 BULK INSERT 作業更好的延展性。 藉由使用小型資料列插入作業，可能會因為使用參數清單或批次處理的陳述式 (而非 BULK INSERT 作業或資料表值參數) 而有效能上的小獲益。 但是，這些方法的便利性不如程式，而且當資料列增加時，效能會快速降低。  
  
 資料表值參數的執行效能等於或優於同等的參數陣列實作。  
  
##  <a name="Example"></a> 範例  
 下列範例使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 並示範如何建立資料表值參數類型、宣告變數來參考它、填入參數清單，然後將值傳遞給預存程序。  
  
```  
USE AdventureWorks2012;  
GO  
  
/* Create a table type. */  
CREATE TYPE LocationTableType AS TABLE   
( LocationName VARCHAR(50)  
, CostRate INT );  
GO  
  
/* Create a procedure to receive data for the table-valued parameter. */  
CREATE PROCEDURE dbo. usp_InsertProductionLocation  
    @TVP LocationTableType READONLY  
    AS   
    SET NOCOUNT ON  
    INSERT INTO AdventureWorks2012.Production.Location  
           (Name  
           ,CostRate  
           ,Availability  
           ,ModifiedDate)  
        SELECT *, 0, GETDATE()  
        FROM  @TVP;  
        GO  
  
/* Declare a variable that references the type. */  
DECLARE @LocationTVP AS LocationTableType;  
  
/* Add data to the table variable. */  
INSERT INTO @LocationTVP (LocationName, CostRate)  
    SELECT Name, 0.00  
    FROM AdventureWorks2012.Person.StateProvince;  
  
/* Pass the table variable data to a stored procedure. */  
EXEC usp_InsertProductionLocation @LocationTVP;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [CREATE TYPE &#40;Transact-SQL&#41;](../../t-sql/statements/create-type-transact-sql.md)   
 [DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)   
 [sys.types &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-types-transact-sql.md)   
 [sys.parameters &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-parameters-transact-sql.md)   
 [sys.parameter_type_usages &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-parameter-type-usages-transact-sql.md)   
 [CREATE PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/create-procedure-transact-sql.md)   
 [CREATE FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-function-transact-sql.md)  
  
  
