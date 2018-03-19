---
title: SCHEMA_NAME (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SCHEMA_NAME
- SCHEMA_NAME_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- SCHEMA_NAME function
- schemas [SQL Server], names
ms.assetid: 20071b77-2b6e-4ce7-a8e3-fa71480baf73
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 41dd04ebbbc5b07512d243e5d4ac77761ba9ca1e
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="schemaname-transact-sql"></a>SCHEMA_NAME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  傳回與結構描述識別碼相關聯的結構描述名稱。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
SCHEMA_NAME ( [ schema_id ] )  
```  
  
## <a name="arguments"></a>引數  
  
|詞彙|定義|  
|----------|----------------|  
|*schema_id*|結構描述的識別碼。 *schema_id* 為 **int**。若未定義 *schema_id*，SCHEMA_NAME 會傳回呼叫者預設結構描述的名稱。|  
  
## <a name="return-types"></a>傳回類型  
 **sysname**  
  
 當 *schema_id* 不是有效識別碼時，會傳回 NULL。  
  
## <a name="remarks"></a>Remarks  
 SCHEMA_NAME 會傳回系統結構描述和使用者自訂結構描述的名稱。 SCHEMA_NAME 可在選取清單、WHERE 子句及任何允許使用運算式的位置中呼叫。  
  
## <a name="examples"></a>範例  
  
### <a name="a-returning-the-name-of-the-default-schema-of-the-caller"></a>A. 傳回呼叫端預設結構描述的名稱  
  
```  
SELECT SCHEMA_NAME();  
```  
  
### <a name="b-returning-the-name-of-a-schema-by-using-an-id"></a>B. 使用識別碼來傳回結構描述的名稱  
  
```  
SELECT SCHEMA_NAME(1);  
```  
  
## <a name="see-also"></a>另請參閱  
 [運算式 &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [SCHEMA_ID &#40;Transact-SQL&#41;](../../t-sql/functions/schema-id-transact-sql.md)   
 [sys.schemas &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/schemas-catalog-views-sys-schemas.md)   
 [sys.database_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)   
 [中繼資料函式 &#40;Transact-SQL&#41;](../../t-sql/functions/metadata-functions-transact-sql.md)   
 [WHERE &#40;Transact-SQL&#41;](../../t-sql/queries/where-transact-sql.md)  
  
  

