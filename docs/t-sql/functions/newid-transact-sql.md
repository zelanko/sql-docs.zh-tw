---
title: "NEWID (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 07/29/2017
ms.prod: sql-non-specified
ms.prod_service: sql-data-warehouse, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- NEWID
- NEWID_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- uniqueidentifier data type
- NEWID function
ms.assetid: f7014e60-96d5-457e-afc3-72b60ba20c0f
caps.latest.revision: 39
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e6f9b19f1af5bc0b9c3bde1dfd7bddabd420f40d
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="newid-transact-sql"></a>NEWID (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-xxx-md.md)]

  建立類型的唯一值**uniqueidentifier**。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
NEWID ( )  
```  
  
## <a name="return-types"></a>傳回類型  
 **uniqueidentifier**  
  
## <a name="remarks"></a>備註  
 `NEWID()` 符合 RFC4122。  
  
## <a name="examples"></a>範例  
  
### <a name="a-using-the-newid-function-with-a-variable"></a>A. 搭配變數使用 NEWID 函數  
 下列範例會使用`NEWID()`將值指派給變數，宣告為**uniqueidentifier**資料型別。 值**uniqueidentifier**資料型別變數在列印之前會測試值。  
  
```  
-- Creating a local variable with DECLARE/SET syntax.  
DECLARE @myid uniqueidentifier  
SET @myid = NEWID()  
PRINT 'Value of @myid is: '+ CONVERT(varchar(255), @myid)  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Value of @myid is: 6F9619FF-8B86-D011-B42D-00C04FC964FF  
```  
  
> [!NOTE]  
>  NEWID 傳回的值，每部電腦都不相同。 顯示這個數字，只是為了說明。  
  
### <a name="b-using-newid-in-a-create-table-statement"></a>B. 在 CREATE TABLE 陳述式中使用 NEWID  
  
**適用於**:[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]
  
 下列範例會建立`cust`資料表具有**uniqueidentifier**資料型別，且利用 NEWID 資料表中填入預設值。 在指派 `NEWID()` 的預設值時，每個新的資料列和現有的資料列，都有唯一的 `CustomerID` 資料行值。  
  
```  
-- Creating a table using NEWID for uniqueidentifier data type.  
CREATE TABLE cust  
(  
 CustomerID uniqueidentifier NOT NULL  
   DEFAULT newid(),  
 Company varchar(30) NOT NULL,  
 ContactName varchar(60) NOT NULL,   
 Address varchar(30) NOT NULL,   
 City varchar(30) NOT NULL,  
 StateProvince varchar(10) NULL,  
 PostalCode varchar(10) NOT NULL,   
 CountryRegion varchar(20) NOT NULL,   
 Telephone varchar(15) NOT NULL,  
 Fax varchar(15) NULL  
);  
GO  
-- Inserting 5 rows into cust table.  
INSERT cust  
(CustomerID, Company, ContactName, Address, City, StateProvince,   
 PostalCode, CountryRegion, Telephone, Fax)  
VALUES  
 (NEWID(), 'Wartian Herkku', 'Pirkko Koskitalo', 'Torikatu 38', 'Oulu', NULL,  
 '90110', 'Finland', '981-443655', '981-443655')  
,(NEWID(), 'Wellington Importadora', 'Paula Parente', 'Rua do Mercado, 12', 'Resende', 'SP',  
 '08737-363', 'Brasil', '(14) 555-8122', '')  
,(NEWID(), 'Cactus Comidas para Ilevar', 'Patricio Simpson', 'Cerrito 333', 'Buenos Aires', NULL,   
 '1010', 'Argentina', '(1) 135-5555', '(1) 135-4892')  
,(NEWID(), 'Ernst Handel', 'Roland Mendel', 'Kirchgasse 6', 'Graz', NULL,  
 '8010', 'Austria', '7675-3425', '7675-3426')  
,(NEWID(), 'Maison Dewey', 'Catherine Dewey', 'Rue Joseph-Bens 532', 'Bruxelles', NULL,  
 'B-1180', 'Belgium', '(02) 201 24 67', '(02) 201 24 68');  
GO  
```  
  
### <a name="c-using-uniqueidentifier-and-variable-assignment"></a>C. 使用 uniqueidentifier 和變數指派  
 下列範例會宣告區域變數呼叫`@myid`為的變數**uniqueidentifier**資料型別。 之後，再利用 `SET` 陳述式來指派變數值。  
  
```  
DECLARE @myid uniqueidentifier ;  
SET @myid = 'A972C577-DFB0-064E-1189-0154C99310DAAC12';  
SELECT @myid;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [NEWSEQUENTIALID &#40;TRANSACT-SQL &#41;](../../t-sql/functions/newsequentialid-transact-sql.md)   
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [CAST 和 CONVERT &#40;TRANSACT-SQL &#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [資料類型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [系統函數 &#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-for-transact-sql.md)   
 [uniqueidentifier &#40;TRANSACT-SQL &#41;](../../t-sql/data-types/uniqueidentifier-transact-sql.md)   
 [序號](../../relational-databases/sequence-numbers/sequence-numbers.md)  
  
  

