---
title: CRYPT_GEN_RANDOM (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- CRYPT_GEN_RANDOM_TSQL
- CRYPT_GEN_RANDOM
dev_langs:
- TSQL
helpviewer_keywords:
- CRYPT_GEN_RANDOM function
ms.assetid: b74bd9d4-758e-4b94-89a0-76dcda6d8c42
caps.latest.revision: 11
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 2971701764238c0517558c1daf64296e4727d5ea
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "33049985"
---
# <a name="cryptgenrandom-transact-sql"></a>CRYPT_GEN_RANDOM (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

這個函數會傳回 Crypto API (CAPI) 所產生的密碼編譯隨機數字。 `CRYPT_GEN_RANDOM` 會傳回一個十六進位數且其長度符合指定的位元組數目。
  
![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>語法  
  
```sql
CRYPT_GEN_RANDOM ( length [ , seed ] )   
```  
  
## <a name="arguments"></a>引數  
*length*  
`CRYPT_GEN_RANDOM` 會建立的數字長度 (以位元組為單位)。 *length* 引數必須有一個 **int** 資料類型，以及一個介於 1 到 8000 之間的值。 **int** 值若超出此範圍，則 `CRYPT_GEN_RANDOM` 會傳回 NULL。 
  
*seed*  
選擇性十六進位數字，當作一個隨機種子值。 *seed* 的長度必須符合 *length* 引數的值。 *seed* 引數有一個 **varbinary(8000)** 資料類型。
  
## <a name="returned-types"></a>傳回的類型  
**varbinary(8000)**
  
## <a name="permissions"></a>Permissions  
這個函數是公用的，而且不需要任何特殊權限。
  
## <a name="examples"></a>範例  
  
### <a name="a-generating-a-random-number"></a>A. 傳回隨機數字  
這個範例會產生 50 位元組長度的隨機數字：
  
```sql
SELECT CRYPT_GEN_RANDOM(50) ;  
```  
  
這個範例會使用 4 位元組種子來產生 4 位元組長度的隨機數字：
  
```sql
SELECT CRYPT_GEN_RANDOM(4, 0x25F18060) ;  
```  
  
## <a name="see-also"></a>另請參閱
[RAND &#40;Transact-SQL&#41;](../../t-sql/functions/rand-transact-sql.md)
  
  
