---
title: "SYMKEYPROPERTY (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SYMKEYPROPERTY_TSQL
- SYMKEYPROPERTY
dev_langs: TSQL
helpviewer_keywords: SYMKEYPROPERTY
ms.assetid: 3d1f7075-3a3c-4660-8cd0-ed938b86fecd
caps.latest.revision: "14"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 12f285530db5557acb4b1317656bc53abbe59df0
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="symkeyproperty-transact-sql"></a>SYMKEYPROPERTY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  傳回根據 EKM 模組所建立之對稱金鑰的演算法。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
SYMKEYPROPERTY ( Key_ID , 'algorithm_desc' | 'string_sid' | 'sid' )  
```  
  
## <a name="arguments"></a>引數  
 *Key_ID*  
 這是資料庫中的對稱金鑰的 Key_ID。 若要在只知道金鑰名稱時尋找 Key_ID，請使用 SYMKEY_ID。 *Key_ID*是資料型別**int**。  
  
 **'**algorithm_desc**'**  
 指定輸出會傳回對稱金鑰的演算法描述。 僅適用於根據 EKM 模組所建立的對稱金鑰。  
  
## <a name="return-types"></a>傳回類型  
 **sql_variant**  
  
## <a name="permissions"></a>Permissions  
 需要對稱金鑰的部分權限，而且呼叫端尚未被拒絕對稱金鑰的 VIEW 權限。  
  
## <a name="examples"></a>範例  
 下列範例會傳回含有 Key_ID 256 之對稱金鑰的演算法。  
  
```  
SELECT SYMKEYPROPERTY(256, 'algorithm_desc') AS Algorithm ;  
GO  
```  
  
## <a name="see-also"></a>請參閱＜  
 [ASYMKEY_ID &#40;TRANSACT-SQL &#41;](../../t-sql/functions/asymkey-id-transact-sql.md)   
 [ALTER SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-symmetric-key-transact-sql.md)   
 [DROP SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-symmetric-key-transact-sql.md)   
 [加密階層](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [sys.symmetric_keys &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-symmetric-keys-transact-sql.md)   
 [安全性目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [KEY_ID &#40;TRANSACT-SQL &#41;](../../t-sql/functions/key-id-transact-sql.md)   
 [ASYMKEYPROPERTY &#40;TRANSACT-SQL &#41;](../../t-sql/functions/asymkeyproperty-transact-sql.md)  
  
  
