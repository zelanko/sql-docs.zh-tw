---
title: RAND (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: sql-data-warehouse, database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- RAND
- RAND_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- RAND function
- values [SQL Server], random float
- random float value
ms.assetid: 363c84d6-b9fa-49ba-9a75-e44f27535ff6
author: julieMSFT
ms.author: jrasnick
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 6f69b3aadea5a426cc478eadd9c3228242161060
ms.sourcegitcommit: 768f046107642f72693514f51bf2cbd00f58f58a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/23/2020
ms.locfileid: "87111345"
---
# <a name="rand-transact-sql"></a>RAND (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-xxx-md.md)]

  傳回介於 0 到 1 (不含) 之間的似隨機 **float**。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
RAND ( [ seed ] )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引數
 *seed*  
 為提供初始值的整數[運算式](../../t-sql/language-elements/expressions-transact-sql.md) (**tinyint**、**smallint**，或 **int**)。 如果未指定 *seed*，[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 便會隨機指派一個初始值。 只要指定初始值之後，傳回的結果一律相同。  
  
## <a name="return-types"></a>傳回型別  
 **float**  
  
## <a name="remarks"></a>備註  
 以同樣的初始值反覆呼叫 RAND()，傳回的結果都是一樣的。  
  
 在一個連接中，如果 RAND() 是以指定的初始值呼叫，則後續所有對 RAND() 的呼叫，都會根據初始的 RAND() 呼叫而產生結果。 例如，下面這個查詢一定會傳回同樣順序的號碼。  
  
```sql  
SELECT RAND(100), RAND(), RAND()   
```  
  
## <a name="examples"></a>範例  
 在下列範例中，RAND 函數會產生四個不同的隨機號碼。  
  
```sql  
DECLARE @counter SMALLINT;  
SET @counter = 1;  
WHILE @counter < 5  
   BEGIN  
      SELECT RAND() Random_Number  
      SET @counter = @counter + 1  
   END;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [數學函數 &#40;Transact-SQL&#41;](../../t-sql/functions/mathematical-functions-transact-sql.md)  
  
  
