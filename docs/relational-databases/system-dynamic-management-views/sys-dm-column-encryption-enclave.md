---
title: dm_column_encryption_enclave (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 10/11/2019
ms.prod: sql
ms.reviewer: vanto
ms.technology: system-objects
ms.topic: language-reference
author: jaszymas
ms.author: jaszymas
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: f41a5f704a50924a882e220786ac8cafc090237a
ms.sourcegitcommit: dacd9b6f90e6772a778a3235fb69412662572d02
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2020
ms.locfileid: "86279557"
---
# <a name="sysdm_column_encryption_enclave-transact-sql"></a>sys.dm_column_encryption_enclave (Transact-SQL)
[!INCLUDE [sqlserver2019-windows-only](../../includes/applies-to-version/sqlserver2019-windows-only.md)]

傳回 Always Encrypted 安全記憶體保護區的效能計數器。 如需詳細資訊，請參閱[具有安全記憶體保護區的 Always Encrypted](../security/encryption/always-encrypted-enclaves.md)。

如果記憶體保護區已設定，而且在上次重新開機後已正確初始化 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，則此視圖只會包含一個資料列。 如果記憶體保護區未設定，或未正確地初始化，則此視圖不會傳回任何資料列。 

|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|current_enclave_session_count|**int**|目前使用記憶體保護區的用戶端會話數目。|  
|current_column_encryption_key_count|**int**|記憶體保護區目前保留的資料行加密金鑰計數。|  
|current_memory_size_kb|**bigint**|記憶體保護區記憶體大小（KB）|  
|total_evicted_session_count|**bigint**|自從上次伺服器重新開機後收回的記憶體保護區會話總數。|   
  
## <a name="permissions"></a>權限  
需要 `VIEW SERVER STATE` 權限。   
  
## <a name="examples"></a>範例  
 
```sql  
SELECT * FROM sys.dm_column_encryption_enclave;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [設定 Always Encrypted 伺服器設定選項的記憶體保護區類型](../../database-engine/configure-windows/configure-column-encryption-enclave-type.md)
  
  
