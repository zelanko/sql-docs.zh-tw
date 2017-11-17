---
title: "COL_LENGTH (TRANSACT-SQL) |Microsoft 文件"
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
- COL_LENGTH
- COL_LENGTH_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- lengths [SQL Server], columns
- COL_LENGTH function
- column properties [SQL Server]
- column length [SQL Server]
ms.assetid: cf891206-c49f-40eb-858e-eefd2b638a33
caps.latest.revision: 20
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 3e0debbe52f8e0bbff8e8f7cc0d6509e1e9436b5
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="collength-transact-sql"></a>COL_LENGTH (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

傳回資料行的定義長度 (以位元組為單位)。
  
![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>語法  
  
```sql
COL_LENGTH ( 'table' , 'column' )   
```  
  
## <a name="arguments"></a>引數  
**'** *資料表* **'**  
這是要判斷資料行長度資訊的資料表名稱。 *資料表*之類型的運算式**nvarchar**。
  
**'** *資料行* **'**  
這是要判斷長度的資料行名稱。 *資料行*之類型的運算式**nvarchar**。
  
## <a name="return-type"></a>傳回類型
**smallint**
  
## <a name="exceptions"></a>例外狀況  
當發生錯誤，或呼叫端沒有檢視物件的權限時，便會傳回 NULL。
  
在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，使用者只能檢視使用者擁有或被授與某些權限之安全性實體的中繼資料。 這表示發出中繼資料的內建函數 (例如，COL_LENGTH) 會在使用者不具有該物件任何權限時傳回 NULL。 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。
  
## <a name="remarks"></a>備註  
類型的資料行**varchar**宣告**max**規範 (**varchar （max)**)，COL_LENGTH 會傳回 – 1 的值。
  
## <a name="examples"></a>範例  
下列範例會顯示 `varchar(40)` 類型之資料行和 `nvarchar(40)` 類型之資料行的傳回值。
  
```sql
USE AdventureWorks2012;  
GO  
CREATE TABLE t1(c1 varchar(40), c2 nvarchar(40) );  
GO  
SELECT COL_LENGTH('t1','c1')AS 'VarChar',  
      COL_LENGTH('t1','c2')AS 'NVarChar';  
GO  
DROP TABLE t1;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
VarChar     NVarChar  
40          80  
```  
  
## <a name="see-also"></a>另請參閱
[運算式 &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)  
[中繼資料函數 &#40;TRANSACT-SQL &#41;](../../t-sql/functions/metadata-functions-transact-sql.md)  
[COL_NAME &#40;TRANSACT-SQL &#41;](../../t-sql/functions/col-name-transact-sql.md)  
[COLUMNPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/columnproperty-transact-sql.md)
  
  

