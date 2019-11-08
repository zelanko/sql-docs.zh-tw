---
title: DROP COLUMN MASTER KEY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/15/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DROP COLUMN MASTER KEY
- DROP_COLUMN_MASTER_KEY_TSQL
- DROP COLUMN MASTER
- DROP_COLUMN_MASTER_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.column_master_keys catalog view
ms.assetid: fd5e77c8-a3ae-4795-bb46-b322c0500041
author: jaszymas
ms.author: jaszymas
ms.openlocfilehash: f6267189a83816f1c77740e5df176cc2dda86428
ms.sourcegitcommit: 312b961cfe3a540d8f304962909cd93d0a9c330b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/05/2019
ms.locfileid: "73594151"
---
# <a name="drop-column-master-key-transact-sql"></a>DROP COLUMN MASTER KEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  從資料庫中卸除資料行主要金鑰。 這是中繼資料作業。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
DROP COLUMN MASTER KEY key_name;  
```  
  
## <a name="arguments"></a>引數  
 *key_name*  
 資料行主要金鑰名稱。  
  
## <a name="remarks"></a>Remarks  
 只有在沒有任何資料行加密金鑰值使用資料行主要金鑰來加密時，才能卸除資料行主要金鑰。 若要卸除資料行加密金鑰值，請使用 [DROP COLUMN ENCRYPTION KEY](../../t-sql/statements/drop-column-encryption-key-transact-sql.md) 陳述式。  
  
## <a name="permissions"></a>權限  
 需要資料庫的 **ALTER ANY COLUMN MASTER KEY** 權限。  
  
## <a name="examples"></a>範例  
  
### <a name="a-dropping-a-column-master-key"></a>A. 卸除資料行主要金鑰  
 下列範例會卸除名為 `MyCMK` 的資料行主要金鑰。  
  
```  
DROP COLUMN MASTER KEY MyCMK;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [CREATE COLUMN MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-column-master-key-transact-sql.md)   
 [CREATE COLUMN ENCRYPTION KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-column-encryption-key-transact-sql.md)   
 [DROP COLUMN ENCRYPTION KEY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-column-encryption-key-transact-sql.md)   
 [sys.column_master_keys &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-master-keys-transact-sql.md)  
 [Always Encrypted](../../relational-databases/security/encryption/always-encrypted-database-engine.md)   
 [具有安全記憶體保護區的 Always Encrypted](../../relational-databases/security/encryption/always-encrypted-enclaves.md)   
 [Always Encrypted 的金鑰管理概觀](../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)   
 [針對具有安全記憶體保護區的 Always Encrypted 管理金鑰](../../relational-databases/security/encryption/always-encrypted-enclaves-manage-keys.md)   
  
  
