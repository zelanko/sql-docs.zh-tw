---
title: "GETANSINULL (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- GETANSINULL
- GETANSINULL_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- null values [SQL Server], default
- GETANSINULL function
- default nullability
- database nullability [SQL Server]
ms.assetid: 189399e4-428d-4902-b3a8-94f07fdefc6a
caps.latest.revision: 29
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 3a103d3d4cc1c66bfcfe47decd4366b47d7831e8
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="getansinull-transact-sql"></a>GETANSINULL (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  傳回這個工作階段之資料庫的預設 Null 屬性。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
GETANSINULL ( [ 'database' ] )  
```  
  
## <a name="arguments"></a>引數  
 '*資料庫*'  
 這是傳回的 Null 屬性資訊所針對的資料庫名稱。 *資料庫*是**char**或**nchar**。 如果**char**，*資料庫*隱含地轉換成**nchar**。  
  
## <a name="return-types"></a>傳回類型  
 **int**  
  
## <a name="remarks"></a>備註  
 當指定之資料庫的 Null 屬性接受 Null 值，且未明確定義資料行或資料類型 Null 屬性時，GETANSINULL 會傳回 1。 這是 ANSI NULL 預設值。  
  
 若要啟用 ANSI NULL 預設行為，則必須符合下列條件之一：  
  
-   ALTER DATABASE *database_name* SET ANSI_NULL_DEFAULT ON  
  
-   SET ANSI_NULL_DFLT_ON ON  
  
-   SET ANSI_NULL_DFLT_OFF OFF  
  
## <a name="examples"></a>範例  
 下列範例會傳回 `AdventureWorks2012` 資料庫的預設 Null 屬性。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT GETANSINULL('AdventureWorks2012')  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 ------  
1  

(1 row(s) affected)
 ```  
  
## <a name="see-also"></a>另請參閱  
 [系統函數 &#40;TRANSACT-SQL &#41;](../../relational-databases/system-functions/system-functions-for-transact-sql.md)  
  
  

