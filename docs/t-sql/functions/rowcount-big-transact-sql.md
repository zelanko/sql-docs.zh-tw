---
title: ROWCOUNT_BIG (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ROWCOUNT_BIG
- ROWCOUNT_BIG_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ROWCOUNT_BIG function
- number of rows affected by statement
- row affected by statements [SQL Server]
- statements [SQL Server], last statement
- counting rows
ms.assetid: 6e18a0eb-bb36-4348-90d9-8b1ecf095064
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: d1e6123b99308e053a3235d5e9fe8cd22a4daaa8
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85736441"
---
# <a name="rowcount_big-transact-sql"></a>ROWCOUNT_BIG (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  傳回上次執行之陳述式所影響的資料列數。 這個函式相當於 [@@ROWCOUNT](../../t-sql/functions/rowcount-transact-sql.md)，只是 ROWCOUNT_BIG 的傳回型別是 **bigint**。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
ROWCOUNT_BIG ( )  
```  
  
## <a name="return-types"></a>傳回型別  
 **bigint**  
  
## <a name="remarks"></a>備註  
 這個函數是在 SELECT 陳述式後面，它會傳回 SELECT 陳述式所傳回的列數。  
  
 這個函數是在 INSERT、UPDATE 或 DELETE 陳述式後面，它會傳回資料修改陳述式所影響的列數。  
  
 這個函數是在不傳回資料列數的陳述式後面 (例如 IF 陳述式)，它會傳回 0。  
  
## <a name="see-also"></a>另請參閱  
 [COUNT_BIG &#40;Transact-SQL&#41;](../../t-sql/functions/count-big-transact-sql.md)   
 [資料類型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
  
  
