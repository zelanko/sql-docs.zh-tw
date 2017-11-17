---
title: "卸除資料行主要金鑰 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 04/20/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 14
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d49d880d78982aa55bbaefc1fadc561e62a26dce
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

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
 資料行主要金鑰的名稱。  
  
## <a name="remarks"></a>備註  
 是否有任何資料行加密資料行主要金鑰所加密金鑰值，可以只會卸除資料行主要金鑰。 若要卸除資料行加密金鑰值，請使用[卸除資料行加密金鑰](../../t-sql/statements/drop-column-encryption-key-transact-sql.md)陳述式。  
  
## <a name="permissions"></a>Permissions  
 需要**ALTER ANY COLUMN MASTER KEY**資料庫的權限。  
  
## <a name="examples"></a>範例  
  
### <a name="a-dropping-a-column-master-key"></a>A. 卸除資料行主要金鑰  
 下列範例會卸除資料行主要金鑰，稱為`MyCMK`。  
  
```  
DROP COLUMN MASTER KEY MyCMK;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [CREATE COLUMN MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-column-master-key-transact-sql.md)   
 [CREATE COLUMN ENCRYPTION KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-column-encryption-key-transact-sql.md)   
 [卸除資料行加密金鑰 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/drop-column-encryption-key-transact-sql.md)   
 [永遠加密 &#40;Database Engine&#41;](../../relational-databases/security/encryption/always-encrypted-database-engine.md)   
 [sys.column_master_keys &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-master-keys-transact-sql.md)  
  
  

