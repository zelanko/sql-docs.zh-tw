---
title: "位元運算子 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 09/07/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- operators [Transact-SQL], bitwise
- bitwise operators
- bit manipulations
ms.assetid: 2b994cf5-2daa-438a-b8c7-4bd8d451ac8d
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Active
ms.openlocfilehash: b0706080c0a878987fab8d2cc5f0c1677f43309b
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="bitwise-operators-transact-sql"></a>位元運算子 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  位元運算子會在整數資料類型類別目錄之任何資料類型的兩個運算式之間，執行位元操作。  
  位元運算子將兩個整數值轉換成二進位位元、 執行 AND、 OR 或 not 每個位元，產生的結果。 然後將結果轉換為整數。  
  
  例如，整數 170 將轉換成二進位 1010 1010年。
整數 75 將轉換成二進位 0100 1011年。

|! 運算子之後|位元的數學運算|
|---- |---- |
|與 <br> 如果在任何位置的位元皆為 1，結果會是 1。 |1010 1010 = 170 <br>0100 1011 =  75 <br>-----------------  <br> 0000 1010 =  10 |
|OR <br> 如果在任何位置的其中一個位元為 1，結果會是 1。 |1010 1010 = 170 <br>0100 1011 =  75 <br>-----------------  <br> 1110 1011 = 235|
|NOT  <br> 反轉每位元位置的位元值。 |1010 1010 = 170 <br>----------------- <br>  0101 0101 =   85 |
  
請參閱下列主題：   
* [& &#40;位元 AND &#41;](../../t-sql/language-elements/bitwise-and-transact-sql.md)  
* [& = &#40;位元 AND 指派 &#41;](../../t-sql/language-elements/bitwise-and-equals-transact-sql.md)   
* [&#124;&#40;位元 OR &#41;](../../t-sql/language-elements/bitwise-or-transact-sql.md)  
* [&#124; = &#40;位元 OR 指派 &#41;](../../t-sql/language-elements/bitwise-or-equals-transact-sql.md)   
* [^ &#40;位元互斥 OR &#41;](../../t-sql/language-elements/bitwise-exclusive-or-transact-sql.md)  
* [^ = &#40;位元互斥 OR 指派 &#41;](../../t-sql/language-elements/bitwise-exclusive-or-equals-transact-sql.md)  
* [~ &#40;位元 NOT &#41;](../../t-sql/language-elements/bitwise-not-transact-sql.md)  
  
 位元運算子的運算元可以是任何一種資料類型的整數或二進位字串資料類型類別目錄 (除了**映像**資料型別)，但這兩個運算元不能是任何一種資料類型的二進位字串資料類型類別目錄。 下表顯示支援的運算元資料類型。  
  
|左運算元|右運算元|  
|------------------|-------------------|  
|[binary](../../t-sql/data-types/binary-and-varbinary-transact-sql.md)|**int**， **smallint**，或**tinyint**|  
|[bit](../../t-sql/data-types/bit-transact-sql.md)|**int**， **smallint**， **tinyint**，或**位元**|  
|[int](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md)|**int**， **smallint**， **tinyint**，**二進位**，或**varbinary**|  
|[smallint](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md)|**int**， **smallint**， **tinyint**，**二進位**，或**varbinary**|  
|[tinyint](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md)|**int**， **smallint**， **tinyint**，**二進位**，或**varbinary**|  
|[varbinary](../../t-sql/data-types/binary-and-varbinary-transact-sql.md)|**int**， **smallint**，或**tinyint**|  
  
## <a name="see-also"></a>另請參閱  
 [運算子 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [資料類型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [複合運算子 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/compound-operators-transact-sql.md)   
  
