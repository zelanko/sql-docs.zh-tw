---
title: "float 和 real (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 7/22/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|data-types
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- float
- real_TSQL
- real
- float_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- numeric data type, floating point
- float data type
- floating point data [SQL Server]
- real data type
ms.assetid: 08ea66b7-624e-4d8b-86bc-750ff76cdfc5
caps.latest.revision: 40
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: dd20fe12af6f1dcaf378d737961bc2ba354aabe5
ms.openlocfilehash: 0ce2e3272c30057f533796e0822256c6235de0c1
ms.contentlocale: zh-tw
ms.lasthandoff: 10/04/2017

---
# <a name="float-and-real-transact-sql"></a>float 和 real (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

用來搭配浮點數值資料使用的近似數值資料類型。 浮點數資料是近似的；因此，並非資料類型範圍內的所有值都能夠精確地表示。 ISO 同義字**真實**是**float(24)**。
  
![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>語法  
**float** [ **(***n***)** ] 其中 *n* 是用來儲存的位元數尾數的**float**科學記號標記法中的數字，因此，它規定的有效位數和儲存體大小。 如果 *n* 指定，則它必須是介於**1**和**53**。 預設值 *n* 是**53**。
  
|*n*值|有效位數|儲存體大小|  
|---|---|---|
|**1-24**|7 位數|4 個位元組|  
|**25-53**|15 位數|8 個位元組|  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]會將 *n* 做為其中一個兩個可能值。 如果**1**<=n<=**24**，  *n* 會被視為**24**。 如果**25**<=n<=**53**，  *n* 會被視為**53**。  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Float**[**(n)**] 資料類型符合 ISO 標準的所有值 *n* 從**1**透過**53**。 同義字**雙精確度**是**float(53)**。
  
## <a name="remarks"></a>備註  
  
|資料類型|範圍|儲存空間|  
|---|---|---|
|**float**|- 1.79E+308 到 -2.23E-308、0 及 2.23E-308 到 1.79E+308|值而定*n*|  
|**real**|- 3.40E + 38 到 -1.18E - 38、0 及 1.18E - 38 到 3.40E + 38|4 個位元組|  
  
##  <a name="converting-float-and-real-data"></a>轉換 float 與 real 資料  
值的**float**它們轉換成任何整數類型時，會被截斷。
  
當您想要轉換的**float**或**真實**成字元資料，使用 STR 字串函數是比 CAST （） 來得有用。 這是因為 STR 可以對格式有較多的控制。 如需詳細資訊，請參閱[STR &#40;TRANSACT-SQL &#41;](../../t-sql/functions/str-transact-sql.md)和[函式 &#40;TRANSACT-SQL &#41;](../../t-sql/functions/functions.md).
  
轉換**float**值使用科學記號標記法來**十進位**或**數值**限制為 17 個有效位數僅的值。 任何值 < 5e-18 無條件捨去為 0。
  
## <a name="see-also"></a>另請參閱
[ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
[CAST 和 CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)  
[資料類型轉換 &#40; Database Engine &#41;](../../t-sql/data-types/data-type-conversion-database-engine.md)  
[資料類型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
[DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)  
[SET @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/set-local-variable-transact-sql.md)
  
  

