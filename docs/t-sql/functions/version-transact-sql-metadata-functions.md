---
title: "版本 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 95a79b33-98f2-4929-a1a5-93b522a9e152
caps.latest.revision: 7
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 1905ef3b0f31e91d6cec00c0314770b7686e8c51
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="version---transact-sql-metadata-functions"></a>版本-Transact SQL 中繼資料函數
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw_md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

 傳回的版本[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]或[!INCLUDE[ssPDW_md](../../includes/sspdw-md.md)]應用裝置上執行。  
  
![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [TRANSACT-SQL 語法慣例 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
-- Azure SQL Data Warehouse and Parallel Data Warehouse  
VERSION ( )  
```  
  
## <a name="arguments"></a>引數  
  
## <a name="general-remarks"></a>一般備註  
必須指定資料表名稱[FROM](../../t-sql/queries/from-transact-sql.md)子句，這個函式傳回的結果。 結果資料列將會傳回每個資料列的結果集的查詢。使用[(TRANSACT-SQL)](../../t-sql/queries/top-transact-sql.md)限制傳回的資料列數目。  
  
## <a name="examples"></a>範例  
下列範例會傳回的版本號碼。  
  
```  
SELECT VERSION();  
```  
  
## <a name="see-also"></a>另請參閱 
[SESSION_ID (TRANSACT-SQL)](../../t-sql/functions/session-id-transact-sql.md)  
[DB_NAME &#40;TRANSACT-SQL &#41;](../../t-sql/functions/db-name-transact-sql.md)  
  
  

