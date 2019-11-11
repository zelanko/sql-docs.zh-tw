---
title: '@@ROWCOUNT (Transact-SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 08/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- '@@ROWCOUNT_TSQL'
- '@@ROWCOUNT'
dev_langs:
- TSQL
helpviewer_keywords:
- '@@ROWCOUNT function'
- number of rows affected by statement
- row affected by statements [SQL Server]
- statements [SQL Server], last statement
- counting rows
ms.assetid: 97a47998-81d9-4331-a244-9eb8b6fe4a56
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 5baec7bb0328f6765bc4d4e1a04993074ad62999
ms.sourcegitcommit: f688a37bb6deac2e5b7730344165bbe2c57f9b9c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/08/2019
ms.locfileid: "73843520"
---
# <a name="x40x40rowcount-transact-sql"></a>&#x40;&#x40;ROWCOUNT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  傳回受到前一個陳述式所影響的資料列數。 如果資料列的數目超過 20 億，請使用 [ROWCOUNT_BIG](../../t-sql/functions/rowcount-big-transact-sql.md)。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
@@ROWCOUNT  
```  
  
## <a name="return-types"></a>傳回類型  
 **int**  
  
## <a name="remarks"></a>Remarks  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式可以使用下列方式，在 @@ROWCOUNT 中設定該值：  
  
-   將 @@ROWCOUNT 設為受影響或讀取的資料列數。 資料列不一定會傳送到用戶端。  
  
-   保留來自前一個陳述式執行的 @@ROWCOUNT。  
  
-   將 @@ROWCOUNT 重設為 0，但不將該值傳回用戶端。  
  
 進行簡單指派的陳述式一律會將 @@ROWCOUNT 值設為 1。 它不會傳送任何資料列給用戶端。 這些陳述式的範例如下：SET @*local_variable*、RETURN、READTEXT，以及如 SELECT GETDATE() 或 SELECT **'***一般文字***'** 等無查詢的選取陳述式。  
  
 在查詢中進行指派的陳述式，或是在查詢中使用 RETURN 的陳述式，會將 @@ROWCOUNT 值設為受到該查詢影響或讀取的資料列數，例如：SELECT @*local_variable* = c1 FROM t1。  
  
 資料操作語言 (DML) 陳述式會將 @@ROWCOUNT 值設為受該查詢影響的資料列數，並且將該值傳回給用戶端。 DML 陳述式可能不會傳送任何資料列給用戶端。  
  
 DECLARE CURSOR 和 FETCH 會將 @@ROWCOUNT 值設為 1。  
  
 EXECUTE 陳述式會保留前一個 @@ROWCOUNT。  
  
 USE、SET \<選項>、DEALLOCATE CURSOR、CLOSE CURSOR、PRINT、RAISERROR、BEGIN TRANSACTION 或 COMMIT TRANSACTION 等陳述式，會將 ROWCOUNT 值重設為 0。  
  
 原生編譯的預存程序會保留上一個 @@ROWCOUNT。 原生編譯預存程序中的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式不會設定 @@ROWCOUNT。 如需詳細資訊，請參閱[原生編譯的預存程序](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md)。  
  
## <a name="examples"></a>範例  
 下列範例會執行 `UPDATE` 陳述式，並且使用 `@@ROWCOUNT` 來偵測是否有任何資料列變更。  
  
```  
USE AdventureWorks2012;  
GO  
UPDATE HumanResources.Employee   
SET JobTitle = N'Executive'  
WHERE NationalIDNumber = 123456789  
IF @@ROWCOUNT = 0  
PRINT 'Warning: No rows were updated';  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [系統函數 &#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-category-transact-sql.md)   
 [SET ROWCOUNT &#40;Transact-SQL&#41;](../../t-sql/statements/set-rowcount-transact-sql.md)  
  
  
