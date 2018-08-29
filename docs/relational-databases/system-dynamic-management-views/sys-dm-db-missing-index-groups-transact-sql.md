---
title: sys.dm_db_missing_index_groups (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_db_missing_index_groups
- sys.dm_db_missing_index_groups_TSQL
- dm_db_missing_index_groups
- dm_db_missing_index_groups_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_missing_index_groups dynamic management view
- missing indexes feature [SQL Server], sys.dm_db_missing_index_groups dynamic management view
ms.assetid: 9cc00acd-d83d-49f8-be72-5b2aebed246b
caps.latest.revision: 39
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: a6bb53e0f67c6db6f9ca0e5f6260812abfdac4c1
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2018
ms.locfileid: "43066820"
---
# <a name="sysdmdbmissingindexgroups-transact-sql"></a>sys.dm_db_missing_index_groups (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  這個 DMV 會傳回有關遺漏特定索引群組中，除了空間索引的索引的資訊。 
  
 在 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]，動態管理檢視不可以公開可能會影響資料庫內含項目的資訊或公開有關使用者可存取之其他資料庫的資訊。 為了避免公開此資訊，包含不屬於連接租用戶之資料的每個資料列都會被篩選出來。  
   
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**index_group_handle**|**int**|識別遺漏索引群組。|  
|**index_handle**|**int**|識別遺漏索引屬於所指定的群組**index_group_handle**。<br /><br /> 一個索引群組僅能包含一個索引。|  
  
## <a name="remarks"></a>備註  
 所傳回的資訊**sys.dm_db_missing_index_groups**會更新查詢最佳化，查詢最佳化工具，而不會保存。 遺漏索引資訊只會保留到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 重新啟動為止。 如果資料庫管理員想要在伺服器回收之後保留遺漏索引資訊，應該定期製作該項資訊的備份副本。  
  
 輸出結果集的任何一個資料行都不是索引鍵，但這些資料行結合在一起便形成一個索引鍵。  

  >[!NOTE]
  >結果集中的此 DMV 會限制為 600 的資料列。 每個資料列都包含一個遺漏的索引。 如果您有多個遺漏索引的 600 時，您應該先處理現有的遺漏索引，因此您可以檢視較新的。
  
## <a name="permissions"></a>Permissions  
 若要查詢此動態管理檢視，使用者必須取得 VIEW SERVER STATE 權限或隱含 VIEW SERVER STATE 權限的任何權限。  
  
## <a name="see-also"></a>另請參閱  
 [sys.dm_db_missing_index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-columns-transact-sql.md)   
 [sys.dm_db_missing_index_details &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-details-transact-sql.md)   
 [sys.dm_db_missing_index_group_stats &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-group-stats-transact-sql.md)  
  
  
