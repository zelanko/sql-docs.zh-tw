---
title: SQL 資料倉儲預存程式 |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.service: sql-data-warehouse
ms.subservice: design
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 02e04dfe-d565-4e45-b427-b8e89c958ba3
author: ronortloff
ms.author: rortloff
monikerRange: = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: 7aa82ee5c5a617c3564ac9246f2e42bebcab220e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "73844357"
---
# <a name="sql-data-warehouse-stored-procedures"></a>SQL 資料倉儲預存程式
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

  [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]提供內建的程式，可讓您用來執行與資料庫角色相關的作業。 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]包括下列系統程式：  
  
##  <a name="AggregateFunctions"></a>[sp_datatype_info_90 &#40;SQL 資料倉儲&#41;](../../relational-databases/system-stored-procedures/sp-datatype-info-90-sql-data-warehouse.md)  
  
 [sp_pdw_add_network_credentials &#40;SQL 資料倉儲&#41;](../../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md)  
  
 [sp_pdw_database_encryption &#40;SQL 資料倉儲&#41;](../../relational-databases/system-stored-procedures/sp-pdw-database-encryption-sql-data-warehouse.md)  
  
 [sp_pdw_database_encryption_regenerate_system_keys &#40;SQL 資料倉儲&#41;](../../relational-databases/system-stored-procedures/sp-pdw-database-encryption-regenerate-system-keys-sql-data-warehouse.md)  
  
 [sp_pdw_log_user_data_masking &#40;SQL 資料倉儲&#41;](../../relational-databases/system-stored-procedures/sp-pdw-log-user-data-masking-sql-data-warehouse.md)  
  
 [sp_pdw_remove_network_credentials &#40;SQL 資料倉儲&#41;](../../relational-databases/system-stored-procedures/sp-pdw-remove-network-credentials-sql-data-warehouse.md)  
  
 [sp_special_columns_100 &#40;SQL 資料倉儲&#41;](../../relational-databases/system-stored-procedures/sp-special-columns-100-sql-data-warehouse.md)  
  
> [!NOTE]  
>  有些額外的系統預存程式只會在的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]實例或透過用戶端 api 使用，而非供一般客戶使用。 這些程式列于[系統預存程式（transact-sql）](https://msdn.microsoft.com/library/ms187961.aspx)。 這些程式可能會變更，而且不保證相容性。 清單中的所有程式都無法在中[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]使用。  
  
## <a name="see-also"></a>另請參閱  
 [系統預存函數 &#40;Transact-sql&#41;](~/relational-databases/system-functions/system-functions-category-transact-sql.md)   
 [資料類型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
  
  
