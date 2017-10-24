---
title: "斜線星狀註解 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 07/27/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- /*...*/_TSQL
- Comment
- /*...*/
dev_langs:
- TSQL
helpviewer_keywords:
- nonexecuting text strings [SQL Server]
- /*...*/ (comment)
- remarks [SQL Server]
- comments [SQL Server]
ms.assetid: 4d9ab1b2-4bbb-4c16-beb1-cafc1af7417c
caps.latest.revision: 30
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 3e617c6f0108906046d6c6ea983d1bbc26082709
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="slash-star-comment-transact-sql"></a>斜線星狀註解 (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  指出使用者提供的文字。 之間的文字 / * 和\*/ 伺服器不會評估。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
/*  
text_of_comment  
*/  
```  
  
## <a name="arguments"></a>引數  
 *text_of_comment*  
 這是註解的文字。 這是一或多個字元字串。  
  
## <a name="remarks"></a>備註  
 註解可以插入個別行中，也可以插入 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式。 多行註解必須以 / * 和\*/。 通常用於多行註解的常用樣式慣例是第一行的開頭 /\*，後續行以\* \*，而且結尾\*/。  
  
 註解沒有長度上限。  
  
 支援巢狀註解。 如果 / * 字元模式，就會發生任何位置內的現有註解它當作巢狀註解的開頭，因此，需要一個結束\*/ 註解標記。 如果結束的註解標示不存在，就會產生錯誤。  
  
 例如，下列程式碼會產生錯誤。  
  
```  
DECLARE @comment AS varchar(20);  
GO  
/*  
SELECT @comment = '/*';  
*/   
SELECT @@VERSION;  
GO   
```  
  
 若要暫時解決這個錯誤，請進行下列變更。  
  
```  
DECLARE @comment AS varchar(20);  
GO  
/*  
SELECT @comment = '/*';  
*/ */  
SELECT @@VERSION;  
GO  
  
```  
  
## <a name="examples"></a>範例  
 下列範例會利用註解來說明程式碼區段應該執行的動作。  
  
```  
USE AdventureWorks2012;  
GO  
/*  
This section of the code joins the Person table with the Address table,   
by using the Employee and BusinessEntityAddress tables in the middle to   
get a list of all the employees in the AdventureWorks2012 database   
and their contact information.  
*/  
SELECT p.FirstName, p.LastName, a.AddressLine1, a.AddressLine2, a.City, a.PostalCode  
FROM Person.Person AS p  
JOIN HumanResources.Employee AS e ON p.BusinessEntityID = e.BusinessEntityID   
JOIN Person.BusinessEntityAddress AS ea ON e.BusinessEntityID = ea.BusinessEntityID  
JOIN Person.Address AS a ON ea.AddressID = a.AddressID;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [-&#40;註解 &#41;&#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/comment-transact-sql.md)   
 [流程控制語言 &#40;TRANSACT-SQL &#41;](~/t-sql/language-elements/control-of-flow.md)  
  
  


