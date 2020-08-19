---
description: sys.dm_column_encryption_enclave (Transact-SQL)
title: sys. dm_column_encryption_enclave (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 10/11/2019
ms.prod: sql
ms.reviewer: vanto
ms.technology: system-objects
ms.topic: language-reference
author: jaszymas
ms.author: jaszymas
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: 480215cc2157887eedbafd7a5cf4368f03e65c93
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88423282"
---
# <a name="sysdm_column_encryption_enclave-transact-sql"></a>sys.dm_column_encryption_enclave (Transact-SQL)
[!INCLUDE [sqlserver2019-windows-only](../../includes/applies-to-version/sqlserver2019-windows-only.md)]

傳回 Always Encrypted 的安全記憶體保護區的效能計數器。 如需詳細資訊，請參閱[具有安全記憶體保護區的 Always Encrypted](../security/encryption/always-encrypted-enclaves.md)。

如果記憶體保護區已設定，而且在上一次重新開機後已正確初始化 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，則視圖只會包含一個資料列。 如果未設定記憶體保護區，或未正確地將它初始化，則 view 不會傳回任何資料列。 

|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|current_enclave_session_count|**int**|目前使用記憶體保護區的用戶端會話數目。|  
|current_column_encryption_key_count|**int**|記憶體保護區目前保留的資料行加密金鑰計數。|  
|current_memory_size_kb|**bigint**|記憶體保護區記憶體大小（KB）|  
|total_evicted_session_count|**bigint**|自從上一次伺服器重新開機之後，已收回的記憶體保護區會話總計數。|   
  
## <a name="permissions"></a>權限  
需要 `VIEW SERVER STATE` 權限。   
  
## <a name="examples"></a>範例  
 
```sql  
SELECT * FROM sys.dm_column_encryption_enclave;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [設定 Always Encrypted 伺服器設定選項的記憶體保護區類型](../../database-engine/configure-windows/configure-column-encryption-enclave-type.md)
  
  
