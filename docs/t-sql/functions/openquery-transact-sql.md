---
title: "OPENQUERY (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/16/2017
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
- OPENQUERY_TSQL
- OPENQUERY
dev_langs:
- TSQL
helpviewer_keywords:
- DELETE statement [SQL Server], OPENQUERY function
- OPENQUERY function
- FROM clause, OPENQUERY function
- UPDATE statement [SQL Server], OPENQUERY function
- pass-through queries [SQL Server]
- INSERT statement [SQL Server], OPENQUERY function
ms.assetid: b805e976-f025-4be1-bcb0-3a57b0c57717
caps.latest.revision: 42
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 834bba08c90262fd72881ab2890abaaf7b8f7678
ms.openlocfilehash: 2a3ad57f9cd898d4c059df725b380be28622035e
ms.contentlocale: zh-tw
ms.lasthandoff: 10/02/2017

---
# <a name="openquery-transact-sql"></a>OPENQUERY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  在指定的連結伺服器上，執行指定的傳遞查詢。 這部伺服器是 OLE DB 資料來源。 您可以依照資料表名稱的相同方式，在查詢的 FROM 子句中參考 OPENQUERY。 OPENQUERY 也可以被當作 INSERT、UPDATE 或 DELETE 陳述式的目標資料表加以參考。 它是根據 OLE DB 提供者的功能而定。 雖然查詢可以傳回多個結果集，但 OPENQUERY 只傳回第一個結果集。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
OPENQUERY ( linked_server ,'query' )  
```  
  
## <a name="arguments"></a>引數  
 *linked_server*  
 這是代表連結伺服器名稱的識別碼。  
  
 **'** *查詢* **'**  
 這是在連結伺服器中執行的查詢字串。 該字串的最大長度是 8 KB。  
  
## <a name="remarks"></a>備註  
 OPENQUERY 不接受變數作為其引數。  
  
 在連結的伺服器上，OPENQUERY 無法用來執行擴充預存程序。 不過，可以利用四部分名稱在連結的伺服器上執行擴充預存程序。 例如：  
  
```t-sql  
EXEC SeattleSales.master.dbo.xp_msver  
```  
  
 FROM 子句中 OPENDATASOURCE、OPENQUERY 或 OPENROWSET 的任何呼叫都會與當做更新目標使用之這些函數的任何呼叫進行個別且獨立的評估，即使完全相同的引數套用至這兩種呼叫也一樣。 尤其，針對其中一個呼叫結果所套用的篩選或聯結條件對於另一個呼叫的結果沒有作用。  
  
## <a name="permissions"></a>Permissions  
 任何使用者都可以執行 OPENQUERY。 您可以從定義給連結伺服器的設定，取得用來連接到遠端伺服器的權限。  
  
## <a name="examples"></a>範例  
  
### <a name="a-executing-an-update-pass-through-query"></a>A. 執行 UPDATE 傳遞查詢  
 下列範例會對在範例 A 中建立的連結伺服器使用 `UPDATE` 傳遞查詢。  
  
```t-sql  
UPDATE OPENQUERY (OracleSvr, 'SELECT name FROM joe.titles WHERE id = 101')   
SET name = 'ADifferentName';  
```  
  
### <a name="b-executing-an-insert-pass-through-query"></a>B. 執行 INSERT 傳遞查詢  
 下列範例會對在範例 A 中建立的連結伺服器使用 `INSERT` 傳遞查詢。  
  
```t-sql  
INSERT OPENQUERY (OracleSvr, 'SELECT name FROM joe.titles')  
VALUES ('NewTitle');  
```  
  
### <a name="c-executing-a-delete-pass-through-query"></a>C. 執行 DELETE 傳遞查詢  
 下列範例會使用 `DELETE` 傳遞查詢來刪除範例 C 中插入的資料列。  
  
```t-sql  
DELETE OPENQUERY (OracleSvr, 'SELECT name FROM joe.titles WHERE name = ''NewTitle''');  
```  
  
### <a name="d-executing-a-select-pass-through-query"></a>D. 執行 SELECT 傳遞查詢  
 下列範例會使用傳遞`SELECT`查詢，以選取範例 c 中插入的資料列  
  
```t-sql  
SELECT * FROM OPENQUERY (OracleSvr, 'SELECT name FROM joe.titles WHERE name = ''NewTitle''');  
```  
    
## <a name="see-also"></a>另請參閱  
 [DELETE &#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)   
 [FROM &#40;Transact-SQL&#41;](../../t-sql/queries/from-transact-sql.md)   
 [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [OPENDATASOURCE &#40;Transact-SQL&#41;](../../t-sql/functions/opendatasource-transact-sql.md)   
 [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)   
 [資料列集函數 &#40;TRANSACT-SQL &#41;](../../t-sql/functions/rowset-functions-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [sp_addlinkedserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)   
 [sp_serveroption &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-serveroption-transact-sql.md)   
 [UPDATE &#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md)   
 [其中 &#40;TRANSACT-SQL &#41;](../../t-sql/queries/where-transact-sql.md)  
  
  

