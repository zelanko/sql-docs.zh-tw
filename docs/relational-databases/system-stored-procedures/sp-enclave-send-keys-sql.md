---
title: sp_enclave_send_keys (TRANSACT-SQL) |Microsoft Docs
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
ms.openlocfilehash: b3d5ed50ac407beebfb54370cf91f0f3b8ba3101
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68124687"
---
# <a name="spenclavesendkeys----transact-sql"></a>sp_enclave_send_keys    (Transact-SQL)
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

傳送所有啟用 enclave 的資料行加密金鑰在資料庫中所使用的記憶體保護區來[安全 enclaves 搭配永遠加密&#40;資料庫引擎&#41;](../../relational-databases/security/encryption/always-encrypted-enclaves.md)。

## <a name="syntax"></a>語法  
  
```
sp_enclave_send_keys
[ ;]  
```

## <a name="arguments"></a>引數

這個預存程序中的任何引數。

## <a name="return-value"></a>傳回值

這個預存程序沒有任何傳回值。
  
## <a name="result-sets"></a>結果集

這個預存程序中的任何結果集。
  
## <a name="remarks"></a>備註

**sp_enclave_send_keys**啟用 enclave 的資料行加密金鑰傳送到飛地，如果符合所有下列條件：

- Enclave 已啟用 SQL Server 執行個體。
- **sp_enclave_send_keys**已從應用程式使用叫用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]用戶端驅動程式，以使用已啟用的 Always Encrypted 和 enclave 計算的資料庫連線的安全 enclaves 支援 永遠加密。

## <a name="permissions"></a>Permissions

 需要**VIEW ANY COLUMN ENCRYPTION KEY DEFINITION**並**VIEW ANY COLUMN MASTER KEY DEFINITION**資料庫中的權限。  
  
## <a name="examples"></a>範例  
  
```sql
EXEC sp_enclave_send_keys;  
```

## <a name="see-also"></a>另請參閱

 [一律加密與安全 enclaves &#40;Database Engine&#41;](../../relational-databases/security/encryption/always-encrypted-enclaves.md)   
 [教學課程：建立及啟用 enclave 的資料行使用隨機的加密使用索引](../security/tutorial-creating-using-indexes-on-enclave-enabled-columns-using-randomized-encryption.md#step-3-create-an-index-with-role-separation)   
 [叫用的索引編製作業使用快取的資料行加密金鑰](../security/encryption/configure-always-encrypted-enclaves.md#invoke-indexing-operations-using-cached-column-encryption-keys)   
 [使用隨機加密的啟用 Enclave 的資料行的索引](../security/encryption/always-encrypted-enclaves.md#indexes-on-enclave-enabled-columns-using-randomized-encryption)   
 [AlwaysOn 和資料庫移轉的考量](../security/encryption/always-encrypted-enclaves.md#considerations-for-alwayson-and-database-migration)
