---
title: IDENTITY (Function) (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- IDENTITY_TSQL
- IDENTITY
dev_langs:
- TSQL
helpviewer_keywords:
- IDENTITY function
- SELECT statement [SQL Server], IDENTITY function
- inserting identity columns
- columns [SQL Server], creating
- identity columns [SQL Server], IDENTITY function
ms.assetid: ebec77eb-fc02-4feb-b6c5-f0098d43ccb6
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 70fbbbae7e04331130346702c8f974669d53942a
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="identity-function-transact-sql"></a>IDENTITY (函數) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  為僅供設定 INTO *table* 子句的 SELECT 陳述式，用來將識別欄位插入新資料表。 雖然相似，但 IDENTITY 函數不是搭配 CREATE TABLE 和 ALTER TABLE 使用的 IDENTITY 屬性。  
  
> [!NOTE]  
>  若要建立可用於多個資料表中或可在不參考任何資料表的情況下從應用程式進行呼叫的自動遞增數字，請參閱 [序號](../../relational-databases/sequence-numbers/sequence-numbers.md)。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
IDENTITY (data_type [ , seed , increment ] ) AS column_name  
```  
  
## <a name="arguments"></a>引數  
 *data_type*  
 這是識別欄位的資料類型。 識別欄位的有效資料類型是整數資料類型類別目錄的任何資料類型，但 **bit** 資料類型或 **decimal** 資料類型除外。  
  
 *seed*  
 這是要指派給資料表中第一個資料列的整數值。 每個後續的資料列都會被指派下一個識別值，也就是最後一個 IDENTITY 值加上 *increment* 值。 如果既未指定 *seed*，也未指定 *increment*，則兩者都會預設為 1。  
  
 *increment*  
 為要新增至資料表中後續資料列之 *seed* 值的整數值。  
  
 *column_name*  
 這是要插入新資料表之資料行的名稱。  
  
## <a name="return-types"></a>傳回類型  
 傳回與 *data_type* 相同的值。  
  
## <a name="remarks"></a>Remarks  
 由於這個函數會在資料表中建立一個資料行，因此，您必須依照下列方式之一，在選取清單中指定一個資料行名稱：  
  
```  
--(1)  
SELECT IDENTITY(int, 1,1) AS ID_Num  
INTO NewTable  
FROM OldTable;  
  
--(2)  
SELECT ID_Num = IDENTITY(int, 1, 1)  
INTO NewTable  
FROM OldTable;  
  
```  
  
## <a name="examples"></a>範例  
 下列範例會將 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 資料庫之 `Contact` 資料表中所有的資料列，插入稱為 `NewContact` 的新資料表中。 這個 IDENTITY 函數在 `NewContact` 資料表中，使識別碼從 100 開始，而不是從 1 開始。  
  
```  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID (N'Person.NewContact', N'U') IS NOT NULL  
    DROP TABLE Person.NewContact;  
GO  
ALTER DATABASE AdventureWorks2012 SET RECOVERY BULK_LOGGED;  
GO  
SELECT  IDENTITY(smallint, 100, 1) AS ContactNum,  
        FirstName AS First,  
        LastName AS Last  
INTO Person.NewContact  
FROM Person.Person;  
GO  
ALTER DATABASE AdventureWorks2012 SET RECOVERY FULL;  
GO  
SELECT ContactNum, First, Last FROM Person.NewContact;  
GO  
  
```  
  
## <a name="see-also"></a>另請參閱  
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [@@IDENTITY &#40;Transact-SQL&#41;](../../t-sql/functions/identity-transact-sql.md)   
 [IDENTITY &#40;屬性&#41; &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql-identity-property.md)   
 [SELECT @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/select-local-variable-transact-sql.md)   
 [DBCC CHECKIDENT &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checkident-transact-sql.md)   
 [sys.identity_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-identity-columns-transact-sql.md)  
  
  
