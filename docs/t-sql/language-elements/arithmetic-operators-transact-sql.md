---
title: 算術運算子 (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- operators [Transact-SQL], arithmetic
- arithmetic operators
- math operations [Transact-SQL]
ms.assetid: a41b92a5-1061-4e4d-bb3b-a180b73c88fa
author: rothja
ms.author: jroth
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: b6fd33150c41b692c803348f3246a165b785f0a1
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/06/2020
ms.locfileid: "85990600"
---
# <a name="arithmetic-operators-transact-sql"></a>算術運算子 (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

算術運算子會執行一或多個資料類型的兩個運算式數學運算。 這些運算子是透過數值資料類型類別目錄來執行。 如需資料類型類別目錄的詳細資訊，請參閱 [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)。  
  
|運算子|意義|  
|--------------|-------------|  
|[+ (加)](../../t-sql/language-elements/add-transact-sql.md)|加|  
|[- (減)](../../t-sql/language-elements/subtract-transact-sql.md)|減|  
|[* (乘)](../../t-sql/language-elements/multiply-transact-sql.md)|乘|  
|[/ (除)](../../t-sql/language-elements/divide-transact-sql.md)|除|  
|[% (模數)](../../t-sql/language-elements/modulo-transact-sql.md)|傳回除法的整數餘數。 例如，12 % 5 = 2，因為 12 除以 5 的餘數是 2。|  
  
加號 (+) 和減號 (-) 運算子也可以用來對 **datetime** 和 **smalldatetime** 值執行算術運算。  
  
如需算術運算結果有效位數和小數位數的詳細資訊，請參閱[有效位數、小數位數和長度 &#40;Transact-SQL&#41;](../../t-sql/data-types/precision-scale-and-length-transact-sql.md)。  
  
## <a name="see-also"></a>另請參閱  
[數學函數 &#40;Transact-SQL&#41;](../../t-sql/functions/mathematical-functions-transact-sql.md)   
[資料類型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
[運算式 &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)  
  
  
