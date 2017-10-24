---
title: "位元運算子 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 09/07/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
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
caps.latest.revision: 29
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 05976158e43d7dfafaf02289462d1537f5beeb36
ms.openlocfilehash: 5d04924a82578040f801864bb68905feebc53e94
ms.contentlocale: zh-tw
ms.lasthandoff: 09/08/2017

---
# <a name="bitwise-operators-transact-sql"></a>位元運算子 (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

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
* [& (位元 AND)](../../t-sql/language-elements/bitwise-and-transact-sql.md)  
* [& = (位元 AND EQUALS)](../../t-sql/language-elements/bitwise-and-equals-transact-sql.md)   
* [&#124;(位元 OR)](../../t-sql/language-elements/bitwise-or-transact-sql.md)  
* [&#124; = (位元 OR EQUALS)](../../t-sql/language-elements/bitwise-or-equals-transact-sql.md)   
* [^ (位元互斥 OR)](../../t-sql/language-elements/bitwise-exclusive-or-transact-sql.md)  
* [^ = (位元互斥 OR EQUALS)](../../t-sql/language-elements/bitwise-exclusive-or-equals-transact-sql.md)  
* [~ (位元 NOT)](../../t-sql/language-elements/bitwise-not-transact-sql.md)  
  
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
  
  

