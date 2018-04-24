---
title: CRYPT_GEN_RANDOM (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
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
ms.workload: Inactive
ms.openlocfilehash: 1742e0d609372fcb2ad17859b503185ba04075ad
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="cryptgenrandom-transact-sql"></a>CRYPT_GEN_RANDOM (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

傳回 Crypto API (CAPI) 所產生的密碼編譯隨機數字。 輸出結果為所指定位元組數目的十六進位數字。
  
![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>語法  
  
```sql
CRYPT_GEN_RANDOM ( length [ , seed ] )   
```  
  
## <a name="arguments"></a>引數  
*length*  
正在建立之數字的長度。 最大值為 8000。 *length* 的類型為 **int**。
  
*seed*  
要當做隨機種子使用的選擇性資料。  至少必須有 *length* 個位元組的資料。 *seed* 為 **varbinary(8000)**。
  
## <a name="returned-types"></a>傳回的類型  
**varbinary(8000)**
  
## <a name="permissions"></a>Permissions  
這個函數是公用的，而且不需要任何特殊權限。
  
## <a name="examples"></a>範例  
  
### <a name="a-generating-a-random-number"></a>A. 傳回隨機數字  
下列範例會產生長度為 50 個位元組的隨機數字。
  
```sql
SELECT CRYPT_GEN_RANDOM(50) ;  
```  
  
下列範例會使用 4 個位元組的種子來產生長度為 4 個位元組的隨機數字。
  
```sql
SELECT CRYPT_GEN_RANDOM(4, 0x25F18060) ;  
```  
  
## <a name="see-also"></a>另請參閱
[RAND &#40;Transact-SQL&#41;](../../t-sql/functions/rand-transact-sql.md)
  
  
