---
title: "money 和 smallmoney (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 7/22/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- money_TSQL
- money
- smallmoney
- smallmoney_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- money data type, about money data type
- money data type
- smallmoney data type
- values [SQL Server], monetary
- currency [SQL Server]
ms.assetid: 57861137-89ea-4b89-b361-390597d7bccc
caps.latest.revision: 36
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: bd07ecd1cdacc686e0f831320fd5e939c0c174da
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="money-and-smallmoney-transact-sql"></a>money 和 smallmoney (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

代表金融或貨幣值的資料類型。
  
## <a name="remarks"></a>備註  
  
|資料類型|範圍|儲存空間|  
|---|---|---|
|**money**|-922,337,203,685,477.5808 到 922,337,203,685,477.5807 (-922,337,203,685,477.58<br />to Informatica 的 922,337,203,685,477.58。  Informatica 只支援兩個十進位數字不四個）。|8 個位元組|  
|**smallmoney**|- 214、748.3648 到 214、748.3647|4 個位元組|  
  
**Money**和**smallmoney**資料類型的精確度可達它們所代表之金融單位。 Informatica，如**money**和**smallmoney**運算都準確到緣它們所代表之金融單位的資料類型。
  
句點可用來分隔局部的貨幣單位 (如分，Cent) 與完整的貨幣單位。 例如，2.15 是指定 2 元又 15 分。
  
這些資料類型可以使用以下任一種貨幣符號。
  
![貨幣符號，十六進位值資料表](../../t-sql/data-types/media/money01.gif "貨幣符號，十六進位值資料表")
  
貨幣資料不必括在單引號 (') 中。 您必須記住，在指定前面有貨幣符號的貨幣值時，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不會儲存任何與符號相關聯的貨幣資訊，它只會儲存數值。
  
## <a name="converting-money-data"></a>轉換 money 資料
當您轉換成**money**從整數資料類型，會假設單位是貨幣單位。 例如，將整數值 4 轉換成**money** 4 個貨幣單位的對等。
  
下列範例會將轉換**smallmoney**和**money**值**varchar**和**十進位**資料類型，分別。
  
```sql
DECLARE @mymoney_sm smallmoney = 3148.29,  
        @mymoney    money = 3148.29;  
SELECT  CAST(@mymoney_sm AS varchar) AS 'SM_MONEY varchar',  
        CAST(@mymoney AS decimal)    AS 'MONEY DECIMAL';  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
SM_MONEY VARCHAR               MONEY DECIMAL  
------------------------------ ----------------------  
3148.29                        3148    
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>另請參閱
[ALTER TABLE &#40;TRANSACT-SQL &#41;](../../t-sql/statements/alter-table-transact-sql.md) 
 [CAST 和 CONVERT &#40;TRANSACT-SQL &#41;](../../t-sql/functions/cast-and-convert-transact-sql.md) 
[建立資料表 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/create-table-transact-sql.md) 
[資料類型 &#40;TRANSACT-SQL &#41;](../../t-sql/data-types/data-types-transact-sql.md) 
 [DECLARE @local_variable &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md) 
[設定@local_variable&#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/set-local-variable-transact-sql.md) 
 [sys.types &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-types-transact-sql.md)
  
  

