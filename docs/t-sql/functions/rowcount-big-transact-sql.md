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
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0299ca4be5b069b06a04c3a9d01d555996fab402
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47625726"
---
# <a name="rowcountbig-transact-sql"></a>ROWCOUNT_BIG (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  傳回上次執行之陳述式所影響的資料列數。 這個函式相當於 [@@ROWCOUNT](../../t-sql/functions/rowcount-transact-sql.md)，只是 ROWCOUNT_BIG 的傳回型別是 **bigint**。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
ROWCOUNT_BIG ( )  
```  
  
## <a name="return-types"></a>傳回類型  
 **bigint**  
  
## <a name="remarks"></a>Remarks  
 這個函數是在 SELECT 陳述式後面，它會傳回 SELECT 陳述式所傳回的列數。  
  
 這個函數是在 INSERT、UPDATE 或 DELETE 陳述式後面，它會傳回資料修改陳述式所影響的列數。  
  
 這個函數是在不傳回資料列數的陳述式後面 (例如 IF 陳述式)，它會傳回 0。  
  
## <a name="see-also"></a>另請參閱  
 [COUNT_BIG &#40;Transact-SQL&#41;](../../t-sql/functions/count-big-transact-sql.md)   
 [資料類型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
  
  
