---
title: "DATALENGTH (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 07/29/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DATALENGTH_TSQL
- DATALENGTH
dev_langs:
- TSQL
helpviewer_keywords:
- number of bytes representing expression
- data types [SQL Server], length
- DATALENGTH function
- expressions [SQL Server], length
- lengths [SQL Server], data
ms.assetid: 00f377f1-cc3e-4eac-be47-b3e3f80267c9
caps.latest.revision: 31
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 77c7eb1fcde9b073b3c08f412ac0e46519763c74
ms.openlocfilehash: d8887c50cb482e27bce63e08aa18b8ca54616faa
ms.contentlocale: zh-tw
ms.lasthandoff: 10/17/2017

---
# <a name="datalength-transact-sql"></a>DATALENGTH (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

傳回用來代表任何運算式的位元組數目。
  
![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>語法  
  
```sql
DATALENGTH ( expression )   
```  
  
## <a name="arguments"></a>引數  
*expression*  
是[運算式](../../t-sql/language-elements/expressions-transact-sql.md)的任何資料類型。
  
## <a name="return-types"></a>傳回型別
**bigint**如果*運算式*屬於**varchar （max)**， **nvarchar （max)**或**varbinary （max)**資料型別。否則**int**。
  
## <a name="remarks"></a>備註  
DATALENGTH 是特別適合用於**varchar**， **varbinary**，**文字**，**映像**， **nvarchar**，和**ntext**資料類型，因為這些資料類型可以儲存可變長度的資料。
  
NULL 的 DATALENGTH 是 NULL。
  
> [!NOTE]  
>  相容性層級可能會影響傳回值。 如需相容性層級的詳細資訊，請參閱 [ALTER DATABASE 相容性層級 &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)。  
  
## <a name="examples"></a>範例  
下列範例會尋找 `Name` 資料表中 `Product` 資料行的長度。
  
```sql
-- Uses AdventureWorks  
  
SELECT length = DATALENGTH(EnglishProductName), EnglishProductName  
FROM dbo.DimProduct  
ORDER BY EnglishProductName;  
GO  
```  
  
## <a name="see-also"></a>另請參閱
[LEN &#40;TRANSACT-SQL &#41;](../../t-sql/functions/len-transact-sql.md)  
[CAST 和 CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[資料類型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
[系統函數 &#40;TRANSACT-SQL &#41;](../../relational-databases/system-functions/system-functions-for-transact-sql.md)
  
  


