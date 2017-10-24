---
title: "TYPE_NAME (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- TYPE_NAME_TSQL
- TYPE_NAME
dev_langs:
- TSQL
helpviewer_keywords:
- names [SQL Server], data types
- unqualified type names
- type names [SQL Server]
- data types [SQL Server], names
- TYPE_NAME function
ms.assetid: e4075a2e-5f70-440f-986b-9ec8434e07c1
caps.latest.revision: 42
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d3d60bec3a21bb5b1127b0f18977d3485979f20b
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="typename-transact-sql"></a>TYPE_NAME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  傳回指定類型識別碼的非限定類型名稱。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
TYPE_NAME ( type_id )   
```  
  
## <a name="arguments"></a>引數  
 *type_id*  
 這是將使用的類型識別碼。 *type_id*是**int**，它可以參考呼叫者有權存取任何結構描述中的型別。  
  
## <a name="return-types"></a>傳回類型  
 **sysname**  
  
## <a name="exceptions"></a>例外狀況  
 當發生錯誤，或呼叫端沒有檢視物件的權限時，便會傳回 NULL。  
  
 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，使用者只能檢視使用者擁有或被授與某些權限之安全性實體的中繼資料。 這表示發出中繼資料的內建函數 (例如，TYPE_NAME) 會在使用者不具有該物件任何權限時傳回 NULL。 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="remarks"></a>備註  
 TYPE_NAME 會傳回 NULL *type_id*無效或當呼叫端沒有足夠的權限參考的類型。  
  
 TYPE_NAME 適用於系統資料類型，也適用於使用者自訂資料類型。 類型可以包含在任何結構描述中，但一律會傳回非限定類型名稱。 這表示名稱沒有*結構描述***。** 前置詞。  
  
 系統函數可以用於選取清單、WHERE 子句以及任何可以使用運算式的位置。 如需詳細資訊，請參閱[運算式 &#40;TRANSACT-SQL &#41;](../../t-sql/language-elements/expressions-transact-sql.md)和[其中 &#40;TRANSACT-SQL &#41;](../../t-sql/queries/where-transact-sql.md).  
  
## <a name="examples"></a>範例  
 下列範例會針對 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫之 `Vendor` 資料表中的每個資料行，傳回物件名稱、資料行名稱和類型名稱。  
  
```  
SELECT o.name AS obj_name, c.name AS col_name,  
       TYPE_NAME(c.user_type_id) AS type_name  
FROM sys.objects AS o   
JOIN sys.columns AS c  ON o.object_id = c.object_id  
WHERE o.name = 'Vendor'  
ORDER BY col_name;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
obj_name        col_name                  type_name
--------------- ------------------------ --------------
Vendor          AccountNumber            AccountNumber
Vendor          ActiveFlag               Flag
Vendor          BusinessEntityID         int
Vendor          CreditRating             tinyint
Vendor          ModifiedDate             datetime
Vendor          Name                     Name
Vendor          PreferredVendorStatus    Flag
Vendor          PurchasingWebServiceURL  nvarchar

(8 row(s) affected)
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>範例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 下列範例會傳回`TYPE ID`識別碼資料型別的`1`。  
  
```  
SELECT TYPE_NAME(36) AS Type36, TYPE_NAME(239) AS Type239;  
GO  
```  
  
 如需類型的清單，查詢 sys.types。  
  
```  
SELECT * FROM sys.types;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [TYPE_ID &#40;TRANSACT-SQL &#41;](../../t-sql/functions/type-id-transact-sql.md)   
 [TYPEPROPERTY &#40;TRANSACT-SQL &#41;](../../t-sql/functions/typeproperty-transact-sql.md)   
 [sys.types &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-types-transact-sql.md)   
 [中繼資料函數 &#40;TRANSACT-SQL &#41;](../../t-sql/functions/metadata-functions-transact-sql.md)  
  
  


