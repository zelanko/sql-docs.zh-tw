---
title: IntelliSense 所支援的 Transact-SQL 語法 | Microsoft 文件
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.technology: scripting
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- Transact-SQL IntelliSense
- IntelliSense [SQL Server], Transact-SQL syntax
ms.assetid: 194e8f4f-fd7e-4f32-a169-f23531128004
author: markingmyname
ms.author: maghan
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 40a73c7b741ec4ac5ce624bce3f0a36fe573eda2
ms.sourcegitcommit: c29150492383f48ef484fa02a483cde1cbc68aca
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/17/2019
ms.locfileid: "65821600"
---
# <a name="transact-sql-syntax-supported-by-intellisense"></a>IntelliSense 所支援的 Transact-SQL 語法
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  此主題描述 [!INCLUDE[tsql](../../includes/tsql-md.md)] 中 IntelliSense 所支援的 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]陳述式和語法。  
  
## <a name="statements-supported-by-intellisense"></a>IntelliSense 所支援的陳述式  
 在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]中，IntelliSense 僅支援最常用的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式。 某些一般的 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 查詢編輯器條件可能會讓 IntelliSense 無法運作。 如需詳細資訊，請參閱[疑難排解 IntelliSense &#40;SQL Server Management Studio&#41;](../../relational-databases/scripting/troubleshooting-intellisense.md)。  
  
> [!NOTE]  
>  IntelliSense 不適用於已加密的資料庫物件，例如已加密的預存程序或使用者定義函數。 參數說明和快速資訊不適用於擴充預存程序和 CLR 整合使用者定義型別的參數。  
  
### <a name="select-statement"></a>SELECT 陳述式  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 查詢編輯器會針對 SELECT 陳述式中的下列語法元素提供 IntelliSense 支援：  
  
|||  
|-|-|  
|SELECT|WHERE|  
|FROM|ORDER BY|  
|HAVING|UNION|  
|FOR|GROUP BY|  
|頂端|OPTION (hint)|  
  
### <a name="additional-transact-sql-statements-that-are-supported"></a>其他支援的 Transact-SQL 陳述式  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 查詢編輯器也會針對下表所顯示的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式提供 IntelliSense 支援。  
  
|Transact-SQL 陳述式|支援的語法|例外狀況|  
|-----------------------------|----------------------|----------------|  
|[INSERT](../../t-sql/statements/insert-transact-sql.md)|所有語法，但 *execute_statement* 子句除外。|None|  
|[UPDATE](../../t-sql/queries/update-transact-sql.md)|所有語法。|None|  
|[DELETE](../../t-sql/statements/delete-transact-sql.md)|所有語法。|None|  
|[DECLARE@local_variable](../../t-sql/language-elements/declare-local-variable-transact-sql.md)|所有語法。|None|  
|[SET@local_variable](../../t-sql/language-elements/set-local-variable-transact-sql.md)|所有語法。|None|  
|[EXECUTE](../../t-sql/language-elements/execute-transact-sql.md)|可執行使用者定義的預存程序、系統預存程序、使用者定義的函數以及系統函數。|None|  
|[CREATE TABLE](../../t-sql/statements/create-table-transact-sql.md)|所有語法。|None|  
|[CREATE VIEW](../../t-sql/statements/create-view-transact-sql.md)|所有語法。|None|  
|[CREATE PROCEDURE](../../t-sql/statements/create-procedure-transact-sql.md)|所有語法。|EXTERNAL NAME 子句沒有任何 IntelliSense 支援。<br /><br /> 在 AS 子句中，IntelliSense 僅支援本主題所列的陳述式和語法。|  
|[ALTER PROCEDURE](../../t-sql/statements/alter-procedure-transact-sql.md)|所有語法|EXTERNAL NAME 子句沒有任何 IntelliSense 支援。<br /><br /> 在 AS 子句中，IntelliSense 僅支援本主題所列的陳述式和語法。|  
|[USE](../../t-sql/language-elements/use-transact-sql.md)|所有語法。|None|  
  
## <a name="intellisense-in-supported-statements"></a>支援陳述式中的 IntelliSense  
 當下列語法元素用於其中一個支援的 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 陳述式時， [!INCLUDE[tsql](../../includes/tsql-md.md)] 查詢編輯器中的 IntelliSense 便支援這些元素：  
  
-   所有聯結類型，包括 APPLY  
  
-   PIVOT 和 UNPIVOT  
  
-   下列資料庫物件的參考：  
  
    -   資料庫和結構描述  
  
    -   資料表、檢視、資料表值函式和資料表運算式  
  
    -   [資料行]  
  
    -   程序和程序參數  
  
    -   純量函數和純量運算式  
  
    -   區域變數  
  
    -   通用資料表運算式 (CTE)  
  
-   只在指令碼或批次的 CREATE 或 ALTER 陳述式中參考，但是由於指令碼或批次尚未執行而不存在資料庫中的資料庫物件。 這些物件如下所示：  
  
    -   已經在指令碼或批次的 CREATE TABLE 或 CREATE PROCEDURE 陳述式中指定的資料表和程序。  
  
    -   已經在指令碼或批次的 ALTER TABLE 或 ALTER PROCEDURE 陳述式中指定的資料表和程序變更。  
  
    > [!NOTE]  
    >  在執行 CREATE VIEW 陳述式之前，IntelliSense 不適用於 CREATE VIEW 陳述式的資料行。  
  
 當先前所列的元素用於 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式時，系統就不會針對它們提供 IntelliSense。 例如，用於 SELECT 陳述式的資料行名稱具有 IntelliSense 支援，但用於 CREATE FUNCTION 陳述式的資料行則沒有。  
  
## <a name="examples"></a>範例  
 在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 指令碼或批次中， [!INCLUDE[ssDE](../../includes/ssde-md.md)] 查詢編輯器中的 IntelliSense 僅支援本主題所列的陳述式和語法。 下列 [!INCLUDE[tsql](../../includes/tsql-md.md)] 程式碼範例將說明 IntelliSense 所支援的陳述式和語法元素。 例如，在下列批次中，當 `SELECT` 陳述式只有本身的編碼時，IntelliSense 便適用於此陳述式，但是當 `SELECT` 包含在 `CREATE FUNCTION` 陳述式內部時，則不適用。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT Name  
FROM Production.Product  
WHERE Name LIKE N'Road-250%' and Color = N'Red';  
GO  
CREATE FUNCTION Production.ufn_Red250 ()  
RETURNS TABLE  
AS  
RETURN   
(  
    SELECT Name  
    FROM AdventureWorks2012.Production.Product  
    WHERE Name LIKE N'Road-250%'  
      AND Color = N'Red'  
);GO  
```  
  
 這項功能也會套用至 CREATE PROCEDURE 或 ALTER PROCEDURE 陳述式之 AS 子句中的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式集合。  
  
 在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 指令碼或批次中，IntelliSense 支援已經在 CREATE 或 ALTER 陳述式中指定的物件。但是，由於陳述式尚未執行，所以這些物件不存在資料庫中。 例如，您可能會在查詢編輯器中輸入下列程式碼：  
  
```  
USE MyTestDB;  
GO  
CREATE TABLE MyTable  
    (PrimaryKeyCol   INT PRIMARY KEY,  
    FirstNameCol      NVARCHAR(50),  
   LastNameCol       NVARCHAR(50));  
GO  
SELECT   
```  
  
 在您輸入 `SELECT`之後，IntelliSense 就會列出 **[PrimaryKeyCol]**、 **[FirstNameCol]** 和 **[LastNameCol]** 當做選取清單中的可能元素，即使該指令碼尚未執行而且 `MyTable` 尚未存在 `MyTestDB`中也一樣。  
  
  
