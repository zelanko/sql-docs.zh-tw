---
title: "算術運算子 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 07/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
helpviewer_keywords:
- operators [Transact-SQL], arithmetic
- arithmetic operators
- math operations [Transact-SQL]
ms.assetid: a41b92a5-1061-4e4d-bb3b-a180b73c88fa
caps.latest.revision: "23"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: ce9ae44451b4307b2fa3e0668467ebe1358f7eaf
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="arithmetic-operators-transact-sql"></a>算術運算子 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  算術運算子會針對數值資料類型類別目錄中一或多個資料類型的兩個運算式，執行數學運算。 如需有關資料類型類別目錄的詳細資訊，請參閱[TRANSACT-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)。  
  
|運算子|意義|  
|--------------|-------------|  
|[+ (加)](../../t-sql/language-elements/add-transact-sql.md)|加|  
|[- (減)](../../t-sql/language-elements/subtract-transact-sql.md)|減|  
|[* (乘)](../../t-sql/language-elements/multiply-transact-sql.md)|乘|  
|[/ (Divide)](../../t-sql/language-elements/divide-transact-sql.md)|除|  
|[%（模數）](../../t-sql/language-elements/modulo-transact-sql.md)|傳回除法的整數餘數。 例如，12 % 5 = 2，因為 12 除以 5 的餘數是 2。|  
  
 加號 （+） 和減號 （-） 運算子也可用來執行算術運算上**datetime**和**smalldatetime**值。  
  
 如需有效位數和小數位數的算術運算結果的詳細資訊，請參閱[有效位數、 小數位數及長度 &#40;TRANSACT-SQL &#41;](../../t-sql/data-types/precision-scale-and-length-transact-sql.md).  
  
## <a name="see-also"></a>另請參閱  
 [數學函數 &#40;TRANSACT-SQL &#41;](../../t-sql/functions/mathematical-functions-transact-sql.md)   
 [資料類型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [運算式 &#40;。TRANSACT-SQL &#41;](../../t-sql/language-elements/expressions-transact-sql.md)  
  
  
