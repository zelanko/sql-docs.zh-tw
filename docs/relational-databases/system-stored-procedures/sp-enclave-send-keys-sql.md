---
description: sp_enclave_send_keys (Transact-SQL)
title: sp_enclave_send_keys (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 10/19/2019
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
monikerRange: '>= sql-server-ver15'
ms.openlocfilehash: 0fc33aa4e45e742f50321336bd01ab136c8e966a
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97462699"
---
# <a name="sp_enclave_send_keys-transact-sql"></a>sp_enclave_send_keys (Transact-SQL)
[!INCLUDE [sqlserver2019-windows-only](../../includes/applies-to-version/sqlserver2019-windows-only.md)]

將資料庫中定義的資料行加密金鑰傳送至與 [Always Encrypted 搭配安全記憶體保護區](../security/encryption/always-encrypted-enclaves.md)使用的伺服器端安全記憶體保護區。

`sp_enclave_send_keys` 只傳送記憶體保護區啟用的金鑰，並加密使用隨機化加密且具有索引的資料行。 若為一般使用者查詢，用戶端驅動程式會使用查詢中計算所需的索引鍵來提供記憶體保護區。 `sp_enclave_send_keys` 傳送資料庫中定義的所有資料行加密金鑰，並將其用於索引加密資料行。 

`sp_enclave_send_keys` 提供簡單的方法，將金鑰傳送至記憶體保護區，並在資料行加密金鑰快取中填入後續的索引作業。 用 `sp_enclave_send_keys` 來啟用：
- 如果 DBA 無法存取資料行主要金鑰 (s) ，則為可重建或更改加密資料庫資料行之索引或統計資料的 DBA。 請參閱使用快取的資料 [行加密金鑰來叫用編制索引作業](../security/encryption/always-encrypted-enclaves-create-use-indexes.md#invoke-indexing-operations-using-cached-column-encryption-keys)。
- [!INCLUDE [ssnoversion-md](../../includes/ssnoversion-md.md)] 完成加密資料行上索引的復原。 請參閱 [資料庫](../security/encryption/always-encrypted-enclaves.md#database-recovery)復原。
- 使用 .NET Framework Data Provider SQL Server 的應用程式，可將資料大量載入加密資料行。

若要成功叫 `sp_enclave_send_keys` 用，您必須連接到資料庫，並啟用資料庫連接的 Always Encrypted 和記憶體保護區計算。 您也必須能夠存取資料行主要金鑰，以保護資料行加密金鑰，您將會傳送，而且您需要存取資料庫中 Always Encrypted 金鑰中繼資料的許可權。 

## <a name="syntax"></a>語法  
  
```
sp_enclave_send_keys
[ ;]  
```

## <a name="arguments"></a>引數

這個預存程式沒有引數。

## <a name="return-value"></a>傳回值

這個預存程式沒有傳回值。
  
## <a name="result-sets"></a>結果集

這個預存程式沒有結果集。
  
## <a name="permissions"></a>權限

 需要 `VIEW ANY COLUMN ENCRYPTION KEY DEFINITION` 資料庫的和 `VIEW ANY COLUMN MASTER KEY DEFINITION` 許可權。  
  
## <a name="examples"></a>範例  
  
```sql
EXEC sp_enclave_send_keys;  
```

## <a name="see-also"></a>另請參閱
- [具有安全記憶體保護區的 Always Encrypted](../security/encryption/always-encrypted-enclaves.md) 
 
- [使用具有安全記憶體保護區的 Always Encrypted 在資料行上建立及使用索引](../security/encryption/always-encrypted-enclaves-create-use-indexes.md)

- [教學課程：使用隨機化加密在啟用記憶體保護區的資料行上建立和使用索引](../security/tutorial-creating-using-indexes-on-enclave-enabled-columns-using-randomized-encryption.md)
