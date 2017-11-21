---
title: "COLUMNS_UPDATED (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- COLUMNS_UPDATED_TSQL
- COLUMNS_UPDATED
dev_langs:
- TSQL
helpviewer_keywords:
- COLUMNS_UPDATED function
- testing columns
- column testing [SQL Server]
- updated columns
ms.assetid: 765fde44-1f95-4015-80a4-45388f18a42c
caps.latest.revision: 53
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 8ddb7462ee985ee62efa70455d27c91a51193124
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="columnsupdated-transact-sql"></a>COLUMNS_UPDATED (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

傳回**varbinary**指出資料表或檢視的插入或更新中的資料行的位元模式。 [!INCLUDE[tsql](../../includes/tsql-md.md)] INSERT 或 UPDATE 觸發程序主體內的任何位置都可以利用 COLUMNS_UPDATED，來測試觸發程序是否應該執行特定動作。
  
![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>語法  
  
```sql
COLUMNS_UPDATED ( )   
```  
  
## <a name="return-types"></a>傳回型別
**varbinary**
  
## <a name="remarks"></a>備註  
COLUMNS_UPDATED 會測試多個資料行所執行的 UPDATE 或 INSERT 動作。 若要測試的 UPDATE 或 INSERT 作業在一個資料行上，使用[update （)](../../t-sql/functions/update-trigger-functions-transact-sql.md)。
  
COLUMNS_UPDATED 會傳回由左至右排序的一或多個位元組，每個位元組中最不重要的位元在最右邊。 最左邊位元組的最右邊位元代表資料表的第一個資料行；左邊的下一個位元代表第二個資料行，依此類推。 如果建立觸發程序的資料表包含超出八個資料行，COLUMNS_UPDATED 會傳回多個位元組，最不重要的位元組在最左邊。 COLUMNS_UPDATED 會針對 INSERT 動作中的所有資料行傳回 TRUE，因為插入了明確的值或隱含的 (NULL) 值。
  
若要進行特定資料行的更新或插入測試，請遵照含有位元運算子和所測試的資料行之整數位元遮罩的語法。 例如，資料表**t1**包含資料行**C1**， **C2**， **C3**， **C4**，和**C5**. 若要確認該資料行**C2**， **C3**，和**C4**都更新 (與資料表**t1**有 UPDATE 觸發程序)，遵循與語法**& 14**。 若要測試是否唯一資料行**C2**是更新，指定**& 2**。
  
COLUMNS_UPDATED 可用在 [!INCLUDE[tsql](../../includes/tsql-md.md)] INSERT 或 UPDATE 觸發程序內的任何位置。
  
INFORMATION_SCHEMA.COLUMNS 檢視表的 ORDINAL_POSITION 資料行與 COLUMNS_UPDATED 所傳回之資料行的位元模式不相容。 若要取得與 COLUMNS_UPDATED 相容的位元模式，在您查詢 `ColumnID` 檢視表時，請依照下列範例所示來參考 `COLUMNPROPERTY` 系統函數的 `INFORMATION_SCHEMA.COLUMNS` 屬性。
  
```sql
SELECT TABLE_NAME, COLUMN_NAME,  
    COLUMNPROPERTY(OBJECT_ID(TABLE_SCHEMA + '.' + TABLE_NAME),  
    COLUMN_NAME, 'ColumnID') AS COLUMN_ID  
FROM AdventureWorks2012.INFORMATION_SCHEMA.COLUMNS  
WHERE TABLE_NAME = 'Person';  
```  
  
## <a name="column-sets"></a>資料行集
針對資料表定義資料行集之後，COLUMNS_UPDATED 函數就會按照下列方式運作：
-   當您明確更新屬於資料行集之成員的資料行時，該資料行的對應位元會設定為 1，而資料行集的位元也會設定為 1。  
-   當您明確更新資料行集時，此資料行集的位元會設定為 1，而該資料表中所有疏鬆資料行的位元也會設定為 1。  
-   若為插入作業，所有位元都會設定為 1。  
  
     由於對資料行集所做的變更會導致該資料行集中所有資料行的位元都設定為 1，因此資料行集中沒有變更的資料行會看似已經修改過。 如需資料行集的詳細資訊，請參閱 [使用資料行集](../../relational-databases/tables/use-column-sets.md)。  
  
## <a name="examples"></a>範例  
  
### <a name="a-using-columnsupdated-to-test-the-first-eight-columns-of-a-table"></a>A. 利用 COLUMNS_UPDATED 來測試資料表的前八個資料行  
下列範例會建立兩份資料表：`employeeData` 和 `auditEmployeeData`。 `employeeData` 資料表會保留機密的員工薪資資訊，人力資源部門的成員可以修改這項資訊。 如果員工的社會保險號碼 (SSN)、年薪或銀行帳戶有了改變，就會產生一筆稽核記錄，且會插入 `auditEmployeeData` 稽核資料表中。
  
藉由使用 `COLUMNS_UPDATED()`，可以快速測試含有機密員工資訊之資料行的任何變更。 只有在您嘗試偵測資料表中前八個資料行的變更時，利用這個方式來使用 `COLUMNS_UPDATED()` 才有效。
  
```sql
USE AdventureWorks2012;  
GO  
IF EXISTS(SELECT TABLE_NAME FROM INFORMATION_SCHEMA.TABLES  
   WHERE TABLE_NAME = 'employeeData')  
   DROP TABLE employeeData;  
IF EXISTS(SELECT TABLE_NAME FROM INFORMATION_SCHEMA.TABLES  
   WHERE TABLE_NAME = 'auditEmployeeData')  
   DROP TABLE auditEmployeeData;  
GO  
CREATE TABLE dbo.employeeData (  
   emp_id int NOT NULL PRIMARY KEY,  
   emp_bankAccountNumber char (10) NOT NULL,  
   emp_salary int NOT NULL,  
   emp_SSN char (11) NOT NULL,  
   emp_lname nchar (32) NOT NULL,  
   emp_fname nchar (32) NOT NULL,  
   emp_manager int NOT NULL  
   );  
GO  
CREATE TABLE dbo.auditEmployeeData (  
   audit_log_id uniqueidentifier DEFAULT NEWID() PRIMARY KEY,  
   audit_log_type char (3) NOT NULL,  
   audit_emp_id int NOT NULL,  
   audit_emp_bankAccountNumber char (10) NULL,  
   audit_emp_salary int NULL,  
   audit_emp_SSN char (11) NULL,  
   audit_user sysname DEFAULT SUSER_SNAME(),  
   audit_changed datetime DEFAULT GETDATE()  
   );  
GO  
CREATE TRIGGER dbo.updEmployeeData   
ON dbo.employeeData   
AFTER UPDATE AS  
/*Check whether columns 2, 3 or 4 have been updated. If any or all  
columns 2, 3 or 4 have been changed, create an audit record. The
bitmask is: power(2,(2-1))+power(2,(3-1))+power(2,(4-1)) = 14. To test   
whether all columns 2, 3, and 4 are updated, use = 14 instead of >0  
(below).*/
  
   IF (COLUMNS_UPDATED() & 14) > 0  
/*Use IF (COLUMNS_UPDATED() & 14) = 14 to see whether all columns 2, 3,   
and 4 are updated.*/  
      BEGIN  
-- Audit OLD record.  
      INSERT INTO dbo.auditEmployeeData  
         (audit_log_type,  
         audit_emp_id,  
         audit_emp_bankAccountNumber,  
         audit_emp_salary,  
         audit_emp_SSN)  
         SELECT 'OLD',   
            del.emp_id,  
            del.emp_bankAccountNumber,  
            del.emp_salary,  
            del.emp_SSN  
         FROM deleted del;  
  
-- Audit NEW record.  
      INSERT INTO dbo.auditEmployeeData  
         (audit_log_type,  
         audit_emp_id,  
         audit_emp_bankAccountNumber,  
         audit_emp_salary,  
         audit_emp_SSN)  
         SELECT 'NEW',  
            ins.emp_id,  
            ins.emp_bankAccountNumber,  
            ins.emp_salary,  
            ins.emp_SSN  
         FROM inserted ins;  
   END;  
GO  
  
/*Inserting a new employee does not cause the UPDATE trigger to fire.*/  
INSERT INTO employeeData  
   VALUES ( 101, 'USA-987-01', 23000, 'R-M53550M', N'Mendel', N'Roland', 32);  
GO  
  
/*Updating the employee record for employee number 101 to change the   
salary to 51000 causes the UPDATE trigger to fire and an audit trail to   
be produced.*/  
  
UPDATE dbo.employeeData  
   SET emp_salary = 51000  
   WHERE emp_id = 101;  
GO  
SELECT * FROM auditEmployeeData;  
GO  
  
/*Updating the employee record for employee number 101 to change both   
the bank account number and social security number (SSN) causes the   
UPDATE trigger to fire and an audit trail to be produced.*/  
  
UPDATE dbo.employeeData  
   SET emp_bankAccountNumber = '133146A0', emp_SSN = 'R-M53550M'  
   WHERE emp_id = 101;  
GO  
SELECT * FROM dbo.auditEmployeeData;  
  
GO  
```  
  
### <a name="b-using-columnsupdated-to-test-more-than-eight-columns"></a>B. 利用 COLUMNS_UPDATED 來測試八個以上資料行  
若要測試會影響資料表中前八個資料行以外之資料行的更新，請利用 `SUBSTRING` 函數來測試 `COLUMNS_UPDATED` 所傳回的正確位元。 下列範例會測試影響資料行的更新`3`， `5`，和`9`中`AdventureWorks2012.Person.Person`資料表。
  
```sql
USE AdventureWorks2012;  
GO  
IF OBJECT_ID (N'Person.uContact2', N'TR') IS NOT NULL  
    DROP TRIGGER Person.uContact2;  
GO  
CREATE TRIGGER Person.uContact2 ON Person.Person  
AFTER UPDATE AS  
    IF ( (SUBSTRING(COLUMNS_UPDATED(),1,1) & 20 = 20)   
        AND (SUBSTRING(COLUMNS_UPDATED(),2,1) & 1 = 1) )   
    PRINT 'Columns 3, 5 and 9 updated';  
GO  
  
UPDATE Person.Person   
   SET NameStyle = NameStyle,  
      FirstName=FirstName,  
      EmailPromotion=EmailPromotion;  
GO  
```  
  
## <a name="see-also"></a>另請參閱
[位元運算子 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/bitwise-operators-transact-sql.md)  
[CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)  
[更新 &#40; &#41;&#40;TRANSACT-SQL &#41;](../../t-sql/functions/update-trigger-functions-transact-sql.md)
  
  

