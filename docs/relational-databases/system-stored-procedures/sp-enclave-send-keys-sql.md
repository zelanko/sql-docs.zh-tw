---
title: sp_enclave_send_keys (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/26/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: vanto
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_enclave_send_keys
- sp_enclave_send_keys_TSQL
- sys.sp_enclave_send_keys
- sys.sp_enclave_send_keys_TSQL
helpviewer_keywords:
- sp_enclave_send_keys
author: jaszymas
ms.author: jaszymas
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: b4ced2feee2227ba1db492f721f57907069c5d99
ms.sourcegitcommit: 97e94b76f9f48d161798afcf89a8c2ac0f09c584
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/30/2019
ms.locfileid: "68661353"
---
# <a name="spenclavesendkeys----transact-sql"></a>sp_enclave_send_keys    (Transact-SQL)
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

將資料庫中所有已啟用記憶體保護區的資料行加密金鑰, 傳送至[安全記憶體保護區&#40;資料庫引擎&#41;Always Encrypted](../../relational-databases/security/encryption/always-encrypted-enclaves.md)所使用的記憶體保護區。

## <a name="syntax"></a>語法  
  
```
sp_enclave_send_keys
[ ;]  
```

## <a name="arguments"></a>引數

這個預存程式沒有任何引數。

## <a name="return-value"></a>傳回值

這個預存程式沒有傳回值。
  
## <a name="result-sets"></a>結果集

這個預存程式沒有任何結果集。
  
## <a name="remarks"></a>備註

如果符合下列所有條件, **sp_enclave_send_keys**會將已啟用記憶體保護區的資料行加密金鑰傳送至記憶體保護區:

- SQL Server 實例中已啟用記憶體保護區。
- 已從使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]用戶端驅動程式的應用程式叫用 sp_enclave_send_keys, 使用同時啟用 Always Encrypted 和記憶體保護區計算的資料庫連接, 支援安全記憶體保護區的 Always Encrypted。

## <a name="permissions"></a>Permissions

 需要資料庫中的**VIEW ANY COLUMN ENCRYPTION KEY definition**和**VIEW ANY COLUMN MASTER KEY definition**許可權。  
  
## <a name="examples"></a>範例  
  
```sql
EXEC sp_enclave_send_keys;  
```

## <a name="see-also"></a>另請參閱

 [使用 secure 記憶體保護區&#40;資料庫引擎的 Always Encrypted&#41;](../../relational-databases/security/encryption/always-encrypted-enclaves.md)   
 [教學課程：使用隨機加密在啟用記憶體保護區的資料行上建立和使用索引](../security/tutorial-creating-using-indexes-on-enclave-enabled-columns-using-randomized-encryption.md#step-3-create-an-index-with-role-separation)   
 [使用快取的資料行加密金鑰叫用索引作業](../security/encryption/configure-always-encrypted-enclaves.md#invoke-indexing-operations-using-cached-column-encryption-keys)   
 [使用隨機化加密之已啟用記憶體保護區的資料行索引](../security/encryption/always-encrypted-enclaves.md#indexes-on-enclave-enabled-columns-using-randomized-encryption)   
 [AlwaysOn 和資料庫移轉的考慮](../security/encryption/always-encrypted-enclaves.md#anchorname-1-considerations-availability-groups-db-migration)
