---
title: "SCHEMA_ID (TRANSACT-SQL) |Microsoft 文件"
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
- SCHEMA_ID
- SCHEMA_ID_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- identification numbers [SQL Server], schemas
- schemas [SQL Server], IDs
- SCHEMA_ID function
- IDs [SQL Server], schemas
- default schema IDs
ms.assetid: c8e34df5-3eea-459f-ae40-050909ce9fda
caps.latest.revision: 39
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 77c7eb1fcde9b073b3c08f412ac0e46519763c74
ms.openlocfilehash: 6034b43145cf81c23359149b07f3b6caaffcc352
ms.contentlocale: zh-tw
ms.lasthandoff: 10/17/2017

---
# <a name="schemaid-transact-sql"></a>SCHEMA_ID (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  傳回與結構描述名稱相關聯的結構描述識別碼。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
SCHEMA_ID ( [ schema_name ] )   
```  
  
## <a name="arguments"></a>引數  
  
|詞彙|定義|  
|----------|----------------|  
|*schema_name*|這是結構描述的名稱。 *schema_name*是**sysname**。 如果*schema_name*未指定，SCHEMA_ID 會傳回呼叫端的預設結構描述的識別碼。|  
  
## <a name="return-types"></a>傳回類型  
 **int**  
  
 如果，則會傳回 NULL *schema_name*不是有效的結構描述。  
  
## <a name="remarks"></a>備註  
 SCHEMA_ID 會傳回系統結構描述和使用者自訂結構描述的識別碼。 SCHEMA_ID 可在選取清單、WHERE 子句及任何允許使用運算式的位置中呼叫。  
  
## <a name="examples"></a>範例  
  
### <a name="a-returning-the-default-schema-id-of-a-caller"></a>A. 傳回呼叫端的預設結構描述識別碼  
  
```  
SELECT SCHEMA_ID();  
```  
  
### <a name="b-returning-the-schema-id-of-a-named-schema"></a>B. 傳回具名結構描述的結構描述識別碼  
  
```  
SELECT SCHEMA_ID('dbo');  
```  
  
## <a name="see-also"></a>另請參閱  
 [中繼資料函數 &#40;TRANSACT-SQL &#41;](../../t-sql/functions/metadata-functions-transact-sql.md)   
 [SCHEMA_NAME &#40;TRANSACT-SQL &#41;](../../t-sql/functions/schema-name-transact-sql.md)   
 [sys.schemas &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/schemas-catalog-views-sys-schemas.md)  
  
  


