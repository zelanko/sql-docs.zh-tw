---
title: "sp_pdw_database_encryption （SQL 資料倉儲） |Microsoft 文件"
ms.custom: 
ms.date: 03/03/2017
ms.prod: 
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: 
ms.service: sql-data-warehouse
ms.component: system-stored-procedures
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
ms.assetid: f5ccb424-7a95-4557-b774-c69de33c1545
caps.latest.revision: "8"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5baf00f93d6105b4da137d4d8d6eff4035c6f2e4
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/02/2018
---
# <a name="sppdwdatabaseencryption-sql-data-warehouse"></a>sp_pdw_database_encryption （SQL 資料倉儲）
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  使用**sp_pdw_database_encryption**上啟用透明資料加密，如[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]應用裝置。 當**sp_pdw_database_encryption**設為 1，使用**ALTER DATABASE**陳述式，以使用 TDE 加密資料庫。  
  
## <a name="syntax"></a>語法  
  
```sql  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
sp_pdw_database_encryption [ [ @enabled = ] enabled ] ;  
```  
  
#### <a name="parameters"></a>參數  
 [  **@enabled=** ]*啟用*  
 判斷是否已啟用透明資料加密。 *啟用*是**int**，而且可以是下列值之一：  
  
-   0 = 已停用  
  
-   1 = 已啟用  
  
 執行**sp_pdw_database_encryption**沒有參數傳回做為純量結果集的應用裝置上的 TDE 的目前狀態： 啟用已停用、 0 或 1。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 當 TDE 啟用時使用**sp_pdw_database_encryption**，tempdb 資料庫卸除、 重新建立和加密。 基於這個原因，TDE 時，無法啟用應用裝置上沒有其他作用中的工作階段使用 tempdb。 啟用或停用 TDE 應用裝置上是預期要執行的應用裝置存留期間，在一次動作會變更狀態的應用裝置中，在大部分情況下，和應用裝置上沒有流量時應執行。  
  
## <a name="permissions"></a>Permissions  
 需要的成員資格**sysadmin**固定資料庫角色或**CONTROL SERVER**權限。  
  
## <a name="example"></a>範例  
 下列範例會啟用 TDE 應用裝置上。  
  
```sql  
EXEC sys.sp_pdw_database_encryption 1;  
```  
  
## <a name="see-also"></a>請參閱  
 [sp_pdw_database_encryption_regenerate_system_keys &#40;SQL 資料倉儲 &#41;](../../relational-databases/system-stored-procedures/sp-pdw-database-encryption-regenerate-system-keys-sql-data-warehouse.md)   
 [sp_pdw_log_user_data_masking &#40;SQL 資料倉儲 &#41;](../../relational-databases/system-stored-procedures/sp-pdw-log-user-data-masking-sql-data-warehouse.md)  
  
  
