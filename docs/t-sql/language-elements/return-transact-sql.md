---
title: RETURN (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- RETURN_TSQL
- RETURN
dev_langs:
- TSQL
helpviewer_keywords:
- unconditionally exiting program
- stored procedures [SQL Server], exiting
- batches [SQL Server], exiting
- statement blocks [SQL Server]
- queries [SQL Server], exiting
- exiting queries [SQL Server]
- exiting procedures [SQL Server]
- RETURN statement
ms.assetid: 1d9c8247-fd89-4544-be9c-01c95b745db0
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Active
ms.openlocfilehash: e7584bdee4d9b07706bc961db23e0090e28cc581
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="return-transact-sql"></a>RETURN (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  無條件地結束查詢或程序。 RETURN 是立即而完整的，您隨時可以利用它來結束程序、批次或陳述式區塊。 系統不會執行 RETURN 之後的陳述式。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
RETURN [ integer_expression ]   
```  
  
## <a name="arguments"></a>引數  
 *integer_expression*  
 這是傳回的整數值。 預存程序可以向發出呼叫的程序或應用程式傳回一個整數值。  
  
## <a name="return-types"></a>傳回類型  
 選擇性地傳回 **int**。  
  
> [!NOTE]  
>  除非另有說明，否則所有系統預存程序都會傳回 0 值。 這表示成功，而非零值則表示失敗。  
  
## <a name="remarks"></a>Remarks  
 當搭配預存程序來使用時，RETURN 無法傳回 Null 值。 如果程序嘗試傳回 Null 值 (例如，當 @status 是 NULL 時，使用 RETURN @status)，便會產生一則警告訊息，而且會傳回 0 值。  
  
 您可以將傳回狀態值包括在執行目前程序之批次或程序的後續 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式中，不過，必須依照下列格式輸入：`EXECUTE @return_status = <procedure_name>`。  
  
## <a name="examples"></a>範例  
  
### <a name="a-returning-from-a-procedure"></a>A. 從程序傳回  
 下列範例會顯示當執行 `findjobs` 時，如果未在參數中指定任何使用者名稱，`RETURN` 會在訊息傳給使用者畫面之後，使程序結束。 如果指定了使用者名稱，便會從適當的系統資料表中，擷取這位使用者在目前資料庫中所建立之所有物件的名稱。  
  
```  
CREATE PROCEDURE findjobs @nm sysname = NULL  
AS   
IF @nm IS NULL  
    BEGIN  
        PRINT 'You must give a user name'  
        RETURN  
    END  
ELSE  
    BEGIN  
        SELECT o.name, o.id, o.uid  
        FROM sysobjects o INNER JOIN master..syslogins l  
            ON o.uid = l.sid  
        WHERE l.name = @nm  
    END;  
```  
  
### <a name="b-returning-status-codes"></a>B. 傳回狀態碼  
 下列範例會檢查指定連絡人之識別碼的州/省份。 如果是華盛頓州 (`WA`)，傳回的狀態就是 `1`。 任何其他狀況 (`2` 值不是 `WA`，或 `StateProvince` 沒有相符的資料列) 都會傳回 `ContactID`。  
  
```  
USE AdventureWorks2012;  
GO  
CREATE PROCEDURE checkstate @param varchar(11)  
AS  
IF (SELECT StateProvince FROM Person.vAdditionalContactInfo WHERE ContactID = @param) = 'WA'  
    RETURN 1  
ELSE  
    RETURN 2;  
GO  
```  
  
 下列範例會顯示執行 `checkstate` 的傳回狀態。 首先顯示在華盛頓州的連絡人，其次顯示不在華盛頓州的連絡人，之後，顯示無效的連絡人。 您必須先宣告 `@return_status` 本機變數，才能使用它。  
  
```  
DECLARE @return_status int;  
EXEC @return_status = checkstate '2';  
SELECT 'Return Status' = @return_status;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 Return Status 
  
 ------------- 
  
 1
 ```  
  
 指定不同的連絡號碼來重新執行查詢。  
  
```  
DECLARE @return_status int;  
EXEC @return_status = checkstate '6';  
SELECT 'Return Status' = @return_status;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 Return Status  
 -------------  
  
 2
 ```  
  
 指定另一個連絡號碼來重新執行查詢。  
  
```  
DECLARE @return_status int  
EXEC @return_status = checkstate '12345678901';  
SELECT 'Return Status' = @return_status;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 Return Status  
 -------------  
  
 2
 ```  
  
## <a name="see-also"></a>另請參閱  
 [ALTER PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-procedure-transact-sql.md)   
 [CREATE PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/create-procedure-transact-sql.md)   
 [DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)   
 [EXECUTE &#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md)   
 [SET @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/set-local-variable-transact-sql.md)   
 [THROW &#40;Transact-SQL&#41;](../../t-sql/language-elements/throw-transact-sql.md)  
  
  
