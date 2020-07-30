---
title: TIMEFROMPARTS (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- TIMEFROMPARTS_TSQL
- TIMEFROMPARTS
dev_langs:
- TSQL
helpviewer_keywords:
- TIMEFROMPARTS function
ms.assetid: 786c65a1-2b3f-4e4b-82b6-4940d62f3801
author: julieMSFT
ms.author: jrasnick
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 3b22a13e149e63aa459d825b62bef4ab0145c928
ms.sourcegitcommit: df1f0f2dfb9452f16471e740273cd1478ff3100c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/29/2020
ms.locfileid: "87394215"
---
# <a name="timefromparts-transact-sql"></a>TIMEFROMPARTS (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  傳回包含指定精確度之指定時間的 **time** 值。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
TIMEFROMPARTS ( hour, minute, seconds, fractions, precision )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引數
 *hour*  
 指定小時的整數運算式。  
  
 *minute*  
 指定分鐘的整數運算式。  
  
 *seconds*  
 指定秒的整數運算式。  
  
 *fractions*  
 指定分數的整數運算式。  
  
 *有效位數*  
 指定要傳回之 **time** 值的精確度的整數常值。  
  
## <a name="return-types"></a>傳回型別  
 **time(** *precision* **)**  
  
## <a name="remarks"></a>備註  
 TIMEROMPARTS 會傳回完整初始化的時間值。 如果引數無效，將會引發錯誤。 如有任何參數為 null，會傳回 null。 然而，若 *precision* 引數為 Null，則會引發錯誤。  
  
 *fractions* 引數相依於 *precision* 引數。 例如，假設 *precision* 為 7，每個分數即表示 100 奈秒；如果 *precision* 為 3，每個分數即表示 1 毫秒。 如果 *precision* 的值為零，*fractions* 也必須為零，否則將引發錯誤。  
  
 這個函數可以遠端處理到 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 和更新版本的伺服器。 它無法遠端處理到版本低於 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 的伺服器。  
  
## <a name="examples"></a>範例  
  
### <a name="a-simple-example-without-fractions-of-a-second"></a>A. 不包含秒的小數部分的簡單範例  
  
```  
SELECT TIMEFROMPARTS ( 23, 59, 59, 0, 0 ) AS Result;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Result  
--------------------  
23:59:59.0000000  
  
(1 row(s) affected)  
```  
  
### <a name="b-example-with-fractions-of-a-second"></a>B. 含秒的小數部分的範例  
 以下範例示範 *fractions* 和 *precision* 參數的用法：  
  
1.  若 *fractions* 的值為 5、*precision* 的值為 1，則 *fractions* 的值表示 5/10 秒。  
  
2.  若 *fractions* 的值為 50、*precision* 的值為 2，則 *fractions* 的值表示 50/100 秒。  
  
3.  若 *fractions* 的值為 500、*precision* 的值為 3，則 *fractions* 的值表示 500/1000 秒。  
  
```sql  
SELECT TIMEFROMPARTS ( 14, 23, 44, 5, 1 );  
SELECT TIMEFROMPARTS ( 14, 23, 44, 50, 2 );  
SELECT TIMEFROMPARTS ( 14, 23, 44, 500, 3 );  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
----------------  
14:23:44.5  
  
(1 row(s) affected)  
  
----------------  
14:23:44.50  
  
(1 row(s) affected)  
  
----------------  
14:23:44.500  
  
(1 row(s) affected)  
```  
  

