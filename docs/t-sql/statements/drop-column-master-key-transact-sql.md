---
title: DROP COLUMN MASTER KEY (Transact-SQL) | Microsoft Docs
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
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 207fd618b0381f69a74bee00bf92b7df248b8aed
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
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
  
## <a name="permissions"></a>Permissions  
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
 [永遠加密 &#40;Database Engine&#41;](../../relational-databases/security/encryption/always-encrypted-database-engine.md)   
 [sys.column_master_keys &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-master-keys-transact-sql.md)  
  
  
