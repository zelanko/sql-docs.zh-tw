---
description: Version - Transact SQL 中繼資料函式
title: VERSION (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 95a79b33-98f2-4929-a1a5-93b522a9e152
author: julieMSFT
ms.author: jrasnick
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest'
ms.openlocfilehash: 164c05d3a8d78ad296af31bcbcbf797c0c77e56b
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97421363"
---
# <a name="version---transact-sql-metadata-functions"></a>Version - Transact SQL 中繼資料函式
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

 傳回在應用裝置上執行之 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 或 [!INCLUDE[ssPDW_md](../../includes/sspdw-md.md)] 的版本。  
  
![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例 &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```syntaxsql
-- Azure Synapse Analytics and Parallel Data Warehouse  
VERSION ( )  
```  
  
## <a name="arguments"></a>引數  
  
## <a name="general-remarks"></a>一般備註  
必須在 [FROM](../../t-sql/queries/from-transact-sql.md) 子句中指定資料表名稱，此函式才能傳回結果。 在查詢的結果集中，將會傳回每個資料列的結果資料列；請使用 [TOP (Transact-SQL)](../../t-sql/queries/top-transact-sql.md) 限制所傳回的資料列數目。  
  
## <a name="examples"></a>範例  
下列範例會傳回版本號碼。  
  
```sql
SELECT VERSION();  
```  
  
## <a name="see-also"></a>另請參閱 
[SESSION_ID (Transact-SQL)](../../t-sql/functions/session-id-transact-sql.md)  
[DB_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/db-name-transact-sql.md)  
  
  
