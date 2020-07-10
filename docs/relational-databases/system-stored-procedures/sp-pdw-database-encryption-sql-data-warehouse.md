---
title: sp_pdw_database_encryption (SQL 資料倉儲) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.service: sql-data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: f5ccb424-7a95-4557-b774-c69de33c1545
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 5f2c4fde17918e148ac26581fcb6f99057e38800
ms.sourcegitcommit: 01297f2487fe017760adcc6db5d1df2c1234abb4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/09/2020
ms.locfileid: "86197322"
---
# <a name="sp_pdw_database_encryption-sql-data-warehouse"></a>sp_pdw_database_encryption (SQL 資料倉儲) 
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  使用**sp_pdw_database_encryption**在設備上啟用透明資料加密 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 。 當**sp_pdw_database_encryption**設為1時，請使用**ALTER database**語句，利用 TDE 來加密資料庫。  
  
## <a name="syntax"></a>語法  
  
```sql  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
sp_pdw_database_encryption [ [ @enabled = ] enabled ] ;  
```  
  
#### <a name="parameters"></a>參數  
`[ @enabled = ] enabled`決定是否啟用透明資料加密。 *enabled*是**int**，它可以是下列其中一個值：  
  
-   0 = 停用  
  
-   1 = 啟用  
  
 執行不含參數的**sp_pdw_database_encryption** ，會以純量結果集的形式傳回設備上 TDE 的目前狀態：0表示已停用，或1表示已啟用。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** (成功) 或**1** (失敗)   
  
## <a name="remarks"></a>備註  
 當使用**sp_pdw_database_encryption**啟用 TDE 時，會卸載 tempdb 資料庫、重新建立和加密。 基於這個理由，在有其他使用 tempdb 的作用中會話時，無法在設備上啟用 TDE。 在設備上啟用或停用 TDE 是一個動作，它會變更設備的狀態，在大多數情況下，預期會在設備生命週期中執行一次，而且應該在設備上沒有流量時執行。  
  
## <a name="permissions"></a>權限  
 需要**系統管理員（sysadmin** ）固定資料庫角色中的成員資格，或**CONTROL SERVER**許可權。  
  
## <a name="example"></a>範例  
 下列範例會在設備上啟用 TDE。  
  
```sql  
EXEC sys.sp_pdw_database_encryption 1;  
```  
  
## <a name="see-also"></a>另請參閱  
 [sp_pdw_database_encryption_regenerate_system_keys &#40;SQL 資料倉儲&#41;](../../relational-databases/system-stored-procedures/sp-pdw-database-encryption-regenerate-system-keys-sql-data-warehouse.md)   
 [sp_pdw_log_user_data_masking &#40;SQL 資料倉儲&#41;](../../relational-databases/system-stored-procedures/sp-pdw-log-user-data-masking-sql-data-warehouse.md)  
  
  
