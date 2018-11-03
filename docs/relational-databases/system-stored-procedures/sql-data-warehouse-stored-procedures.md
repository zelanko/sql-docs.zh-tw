---
title: SQL 資料倉儲預存程序 |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.service: sql-data-warehouse
ms.component: design
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 02e04dfe-d565-4e45-b427-b8e89c958ba3
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: 3369dfd653f1a0485f60145779b5691e200493a3
ms.sourcegitcommit: b29745051be2326268f165cf72f5eb95dc893564
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/31/2018
ms.locfileid: "50254404"
---
# <a name="sql-data-warehouse-stored-procedures"></a>SQL 資料倉儲預存程序
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

  [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 提供內建的程序，可供您執行與資料庫角色相關的作業。 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 包含下列的系統程序：  
  
##  <a name="AggregateFunctions"></a> [sp_datatype_info_90 &#40;SQL 資料倉儲&#41;](../../relational-databases/system-stored-procedures/sp-datatype-info-90-sql-data-warehouse.md)  
  
 [sp_pdw_add_network_credentials &#40;SQL 資料倉儲&#41;](../../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md)  
  
 [sp_pdw_database_encryption &#40;SQL 資料倉儲&#41;](../../relational-databases/system-stored-procedures/sp-pdw-database-encryption-sql-data-warehouse.md)  
  
 [sp_pdw_database_encryption_regenerate_system_keys &#40;SQL 資料倉儲&#41;](../../relational-databases/system-stored-procedures/sp-pdw-database-encryption-regenerate-system-keys-sql-data-warehouse.md)  
  
 [sp_pdw_log_user_data_masking &#40;SQL 資料倉儲&#41;](../../relational-databases/system-stored-procedures/sp-pdw-log-user-data-masking-sql-data-warehouse.md)  
  
 [sp_pdw_remove_network_credentials &#40;SQL 資料倉儲&#41;](../../relational-databases/system-stored-procedures/sp-pdw-remove-network-credentials-sql-data-warehouse.md)  
  
 [sp_special_columns_100 &#40;SQL 資料倉儲&#41;](../../relational-databases/system-stored-procedures/sp-special-columns-100-sql-data-warehouse.md)  
  
> [!NOTE]  
>  某些額外的系統預存程序，只能用在執行個體[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或透過 Api 並不供一般客戶的用戶端使用。 這些程序會列在[系統預存程序 & Amp;#40;transact-SQL&AMP;#41;](http://msdn.microsoft.com/library/ms187961.aspx)。 這些程序會受到變更，而且不保證相容性。 在清單上的所有程序不適用於[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]。  
  
## <a name="see-also"></a>另請參閱  
 [系統預存函式&#40;Transact SQL&#41;](~/relational-databases/system-functions/system-functions-for-transact-sql.md)   
 [資料類型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
  
  
