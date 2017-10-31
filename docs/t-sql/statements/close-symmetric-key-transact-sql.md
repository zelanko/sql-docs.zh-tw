---
title: "CLOSE SYMMETRIC KEY (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 05/15/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CLOSE SYMMETRIC KEY
- CLOSE_SYMMETRIC_KEY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- closing symmetric keys
- encryption [SQL Server], symmetric keys
- symmetric keys [SQL Server], closing
- CLOSE SYMMETRIC KEY statement
- cryptography [SQL Server], symmetric keys
ms.assetid: 3b083cbb-3c6a-4f59-8d34-601db1efcc83
caps.latest.revision: 29
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 18a4215cf009ebf89bf6ce709c0517455731c4b5
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="close-symmetric-key-transact-sql"></a>CLOSE SYMMETRIC KEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  關閉對稱金鑰，或關閉所有目前工作階段中開啟的對稱金鑰。  
  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
CLOSE { SYMMETRIC KEY key_name | ALL SYMMETRIC KEYS }  
```  
  
## <a name="arguments"></a>引數  
 *Key_name*  
 這是要關閉的對稱金鑰名稱。  
  
## <a name="remarks"></a>備註  
 開啟的對稱金鑰繫結到工作階段，而非安全性內容。 開啟的金鑰將持續保持可用狀態，直到明確關閉金鑰或結束工作階段為止。 CLOSE ALL SYMMETRIC KEYS 會關閉任何開啟目前的工作階段中使用的資料庫主要金鑰[OPEN MASTER KEY](../../t-sql/statements/open-master-key-transact-sql.md)陳述式。  開啟金鑰的相關資訊會顯示在[sys.openkeys &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-openkeys-transact-sql.md)目錄檢視。  
  
## <a name="permissions"></a>Permissions  
 關閉對稱金鑰不需要任何明確權限。  
  
## <a name="examples"></a>範例  
  
### <a name="a-closing-a-symmetric-key"></a>A. 關閉對稱金鑰  
 下列範例會關閉對稱金鑰 `ShippingSymKey04`。  
  
```  
CLOSE SYMMETRIC KEY ShippingSymKey04;  
GO  
```  
  
### <a name="b-closing-all-symmetric-keys"></a>B. 關閉所有對稱金鑰  
 下列範例會關閉目前工作階段中開啟的所有對稱金鑰，以及明確開啟的資料庫主要金鑰。  
  
```  
CLOSE ALL SYMMETRIC KEYS;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-symmetric-key-transact-sql.md)   
 [ALTER SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-symmetric-key-transact-sql.md)   
 [OPEN SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/open-symmetric-key-transact-sql.md)   
 [DROP SYMMETRIC KEY &#40;TRANSACT-SQL &#41;](../../t-sql/statements/drop-symmetric-key-transact-sql.md)  
  
  

