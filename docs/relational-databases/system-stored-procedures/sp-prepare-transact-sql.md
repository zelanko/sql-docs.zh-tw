---
title: sp_prepare (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 02/28/2018
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cursor_prepare_TSQL
- sp_cursor_prepare
dev_langs:
- TSQL
helpviewer_keywords:
- sp_prepare
ms.assetid: f328c9eb-8211-4863-bafa-347e1bf7bb3f
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d9095536219fc0cdc419a0952217b0eeb2ef19f5
ms.sourcegitcommit: 9b41725d6db9957dd7928a3620fe4db41eb51c6e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/13/2020
ms.locfileid: "88173102"
---
# <a name="sp_prepare-transact-sql"></a>sp_prepare (Transact SQL)
[!INCLUDE [sql-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdbmi-asa-pdw.md)]

準備參數化 [!INCLUDE[tsql](../../includes/tsql-md.md)] 語句並傳回執行的語句*控制碼*。  `sp_prepare` 的叫用方式是在表格式資料流 (TDS) 封包中指定 ID = 11。  
  
 ![文章連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```syntaxsql  
sp_prepare handle OUTPUT, params, stmt, options  
```  
  
## <a name="arguments"></a>引數  
 *圖*  
 這是 SQL Server 產生的*備妥控制碼*識別碼。 *handle*是具有**int**傳回值的必要參數。  
  
 *params*  
 識別參數化的陳述式。 變數的*params*定義會取代語句中的參數標記。 *params*是針對**Ntext**、 **Nchar**或**Nvarchar**輸入值呼叫的必要參數。 如果陳述式未參數化，則輸入 NULL 值。  
  
 *把*  
 定義資料指標結果集。 *Stmt*參數是必要的，而且會呼叫**Ntext**、 **Nchar**或**Nvarchar**輸入值。  
  
 *options*  
 傳回資料指標結果集資料行描述的選擇性參數。 *選項*需要下列 int 輸入值：  
  
|值|描述|  
|-----------|-----------------|  
|0x0001|RETURN_METADATA|  
  
## <a name="examples"></a>範例  
A. 下列範例會準備及執行簡單陳述式。  
  
```sql  
DECLARE @P1 INT;  
EXEC sp_prepare @P1 OUTPUT,   
    N'@P1 NVARCHAR(128), @P2 NVARCHAR(100)',  
    N'SELECT database_id, name FROM sys.databases WHERE name=@P1 AND state_desc = @P2';  
EXEC sp_execute @P1, N'tempdb', N'ONLINE';  
EXEC sp_unprepare @P1;  
```

B. 下列範例會準備 AdventureWorks2016 資料庫中的語句，並在稍後使用控制碼執行它。

```sql
-- Prepare query
DECLARE @P1 INT;  
EXEC sp_prepare @P1 OUTPUT,   
    N'@Param INT',  
    N'SELECT *
FROM Sales.SalesOrderDetail AS sod
INNER JOIN Production.Product AS p ON sod.ProductID = p.ProductID
WHERE SalesOrderID = @Param
ORDER BY Style DESC;';  

-- Return handle for calling application
SELECT @P1;
GO
```
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]

```
-----------
1

(1 row affected)
```

然後，應用程式會在捨棄備妥的計畫之前，使用控制碼值1執行查詢兩次。

```sql
EXEC sp_execute 1, 49879;  
GO

EXEC sp_execute 1, 48766;
GO

EXEC sp_unprepare 1; 
GO
```
  
## <a name="see-also"></a>另請參閱  
 [系統預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  

