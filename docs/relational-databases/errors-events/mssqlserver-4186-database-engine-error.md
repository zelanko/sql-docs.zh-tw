---
description: MSSQLSERVER_4186
title: MSSQLSERVER_4186 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 4186 (Database Engine error)
ms.assetid: 1ae88554-f291-45bc-a186-6f41d9cd0fca
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 64d0e5012d6883a7933ccb7c48da0d1c6793d502
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471035"
---
# <a name="mssqlserver_4186"></a>MSSQLSERVER_4186
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>詳細資料  
  
| 屬性 | 值 |  
| :-------- | :---- |  
|產品名稱|SQL Server|  
|事件識別碼|4186|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱||  
|訊息文字|OUTPUT 子句中無法參考資料行 '%ls.%.*ls'，因為此資料行定義包含子查詢，或者參考了執行使用者或系統資料存取的函數。 函數如果不是結構描述繫結，根據預設會假設為要執行資料存取。 請考慮從資料行定義中移除子查詢或函數，或者從 OUTPUT 子句中移除資料行。|  
  
## <a name="explanation"></a>說明  
若要避免不具決定性的行為，當檢視表或嵌入資料表值函式中的資料行是由下列其中一種方法所定義時，OUTPUT 子句便不得參考該資料行：  
  
-   子查詢。  
  
-   執行使用者或系統資料存取的使用者定義函數，或假設會執行這類存取的使用者定義函數。  
  
-   包含使用者定義函數的計算資料行，而該函數會在其定義中執行使用者或系統資料存取。  
  
### <a name="examples"></a>範例  
**由子查詢所定義的檢視表資料行**  
  
下列範例會建立在選取清單中使用子查詢來定義資料行 `State` 的檢視表。 然後，UPDATE 陳述式會參考 OUTPUT 子句中的 `State` 資料行，並且由於選取清單中的子查詢而失敗。  
  
```  
USE AdventureWorks2012;  
GO  
CREATE VIEW dbo.V1  
AS  
    SELECT City,  
-- subquery to return the State name  
           (SELECT Name FROM Person.StateProvince AS sp   
            WHERE sp.StateProvinceID = a.StateProvinceID) AS State  
    FROM Person.Address AS a;  
GO  
--Reference the State column in the OUTPUT clause of an UPDATE statement  
UPDATE dbo.V1   
SET City = City + 'Test'   
OUTPUT deleted.City, deleted.State, inserted.City, inserted.State  
WHERE State = 'Texas';  
GO  
```  
  
**由函式所定義的檢視表資料行**  
  
下列範例會建立在選取清單中使用資料存取純量函式 `dbo.ufnGetStock` 來定義資料行 `CurrentInventory` 的檢視表。 然後，UPDATE 陳述式會參考 OUTPUT 子句中的 `CurrentInventory` 資料行。  
  
```  
USE AdventureWorks2012;  
GO  
CREATE VIEW Production.ReorderLevels  
AS  
    SELECT ProductID, ProductModelID, ReorderPoint,  
           dbo.ufnGetStock(ProductID) AS CurrentInventory  
    FROM Production.Product;  
GO  
  
UPDATE Production.ReorderLevels  
SET ReorderPoint += CurrentInventory  
OUTPUT deleted.ReorderPoint, deleted.CurrentInventory,  
       inserted.ReorderPoint, inserted.CurrentInventory  
WHERE ProductModelID BETWEEN 75 and 80;  
```  
  
## <a name="user-action"></a>使用者動作  
您可以使用下列其中一種方法來更正錯誤 4186：  
  
-   使用聯結 (而非子查詢) 來定義檢視表或函數中的資料行。 例如，您可以依照下列方式重新撰寫檢視表 `dbo.V1`。  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    CREATE VIEW dbo.V1  
    AS  
        SELECT City, sp.Name AS State  
        FROM Person.Address AS a   
        JOIN Person.StateProvince AS sp   
        ON sp.StateProvinceID = a.StateProvinceID;  
    ```  
  
-   檢查使用者定義函數的定義。 如果此函數沒有執行使用者或系統資料存取，請將函數更改為包含 WITH SCHEMABINDING 子句。  
  
-   從 OUTPUT 子句中移除資料行。  
  
## <a name="see-also"></a>另請參閱  
[OUTPUT 子句 &#40;Transact-SQL&#41;](~/t-sql/queries/output-clause-transact-sql.md)  
  
