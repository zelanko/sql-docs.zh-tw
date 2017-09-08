---
title: "CRYPT_GEN_RANDOM (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: f2732196567dc98dc768e81b305ffa72ed453a94
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="cryptgenrandom-transact-sql"></a>CRYPT_GEN_RANDOM (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

傳回 Crypto API (CAPI) 所產生的密碼編譯隨機數字。 輸出結果為所指定位元組數目的十六進位數字。
  
![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>語法  
  
```sql
CRYPT_GEN_RANDOM ( length [ , seed ] )   
```  
  
## <a name="arguments"></a>引數  
*length*  
正在建立之數字的長度。 最大值為 8000。 *長度*是型別**int**。
  
*種子*  
要當做隨機種子使用的選擇性資料。  必須有至少*長度*位元組的資料。 *種子*是**varbinary （8000)**。
  
## <a name="returned-types"></a>傳回的類型  
**varbinary （8000)**
  
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
[RAND &#40;TRANSACT-SQL &#41;](../../t-sql/functions/rand-transact-sql.md)
  
  

