---
title: TYPEPROPERTY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- TYPEPROPERTY
- TYPEPROPERTY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- status information [SQL Server], data types
- data types [SQL Server], status information
- TYPEPROPERTY function
ms.assetid: bc311c80-bac5-46ab-a5c8-68b1c6bbf24a
caps.latest.revision: 43
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c5aaeb94cfe33a36c1b918d00bbd7907acaa313f
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2018
ms.locfileid: "43065854"
---
# <a name="typeproperty-transact-sql"></a>TYPEPROPERTY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  傳回資料類型的相關資訊。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
TYPEPROPERTY (type , property)  
```  
  
## <a name="arguments"></a>引數  
 *type*  
 這是資料類型的名稱。  
  
 *property*  
 這是要針對資料類型傳回的資訊類型。 *property* 可以是下列值之一。  
  
|屬性|Description|傳回的值|  
|--------------|-----------------|--------------------|  
|**AllowsNull**|允許 Null 值的資料類型。|1 = True<br /><br /> 0 = False<br /><br /> NULL = 找不到資料類型。|  
|**OwnerId**|類型的擁有者。<br /><br /> 注意：結構描述擁有者不一定是類型擁有者。|非 Null = 類型擁有者的資料庫使用者識別碼。<br /><br /> NULL = 不支援的類型，或類型識別碼無效。|  
|**有效位數**|資料類型的有效位數。|位數或字元數。<br /><br /> -1 = **xml** 或大型數值資料類型<br /><br /> NULL = 找不到資料類型。|  
|**小數位數**|資料類型的小數位數。|資料類型的小數位數數目。<br /><br /> NULL = 資料類型不是 **numeric**，或找不到。|  
|**UsesAnsiTrim**|當建立資料類型時，ANSI 填補設定是 ON。|1 = True<br /><br /> 0 = False<br /><br /> NULL = 找不到資料類型，或它不是二進位或字串資料類型。|  
  
## <a name="return-types"></a>傳回類型  
 **int**  
  
## <a name="exceptions"></a>例外狀況  
 當發生錯誤，或呼叫端沒有檢視物件的權限時，便會傳回 NULL。  
  
 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，使用者只能檢視使用者擁有或被授與某些權限之安全性實體的中繼資料。 這表示發出中繼資料的內建函數 (例如，TYPEPROPERTY) 會在使用者不具有該物件任何權限時傳回 NULL。 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="examples"></a>範例  
  
### <a name="a-identifying-the-owner-of-a-data-type"></a>A. 識別資料類型的擁有者  
 下列範例會傳回資料類型的擁有者。  
  
```  
SELECT TYPEPROPERTY(SCHEMA_NAME(schema_id) + '.' + name, 'OwnerId') AS owner_id, name, system_type_id, user_type_id, schema_id  
FROM sys.types;  
```  
  
### <a name="b-returning-the-precision-of-the-tinyint-data-type"></a>B. 傳回 tinyint 資料類型的有效位數  
 下列範例會傳回 `tinyint` 資料類型的有效位數或位數數目。  
  
```  
SELECT TYPEPROPERTY( 'tinyint', 'PRECISION');  
```  
  
## <a name="see-also"></a>另請參閱  
 [TYPE_ID &#40;Transact-SQL&#41;](../../t-sql/functions/type-id-transact-sql.md)   
 [TYPE_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/type-name-transact-sql.md)   
 [COLUMNPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/columnproperty-transact-sql.md)   
 [中繼資料函數 &#40;Transact-SQL&#41;](../../t-sql/functions/metadata-functions-transact-sql.md)   
 [OBJECTPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/objectproperty-transact-sql.md)   
 [ALTER AUTHORIZATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-authorization-transact-sql.md)   
 [sys.types &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-types-transact-sql.md)  
  
  

