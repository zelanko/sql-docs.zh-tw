---
title: 清除合併中繼資料 (複寫 Transact-SQL 程式設計) | Microsoft 文件
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- metadata [SQL Server replication]
- sp_mergemetadataretentioncleanup
ms.assetid: 9b88baea-b7c6-4e5d-88f9-93d6a0ff0368
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 972e250e97e8f94b3de3a453137c21cc9fc099c2
ms.sourcegitcommit: 8732161f26a93de3aa1fb13495e8a6a71519c155
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2019
ms.locfileid: "71710439"
---
# <a name="clean-up-merge-metadata-replication-transact-sql-programming"></a>清除合併中繼資料 (複寫 Transact-SQL 程式設計)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  合併式複寫中繼資料會由「合併代理程式」依據發行集的保留設定而定期清除。 這項作業會在 [MSmerge_genhistory](../../../relational-databases/system-tables/msmerge-genhistory-transact-sql.md)、 [MSmerge_contents](../../../relational-databases/system-tables/msmerge-contents-transact-sql.md)、 [MSmerge_tombstone](../../../relational-databases/system-tables/msmerge-tombstone-transact-sql.md)、 [MSmerge_past_partition_mappings](../../../relational-databases/system-tables/msmerge-past-partition-mappings-transact-sql.md)和 [MSmerge_current_partition_mappings](../../../relational-databases/system-tables/msmerge-current-partition-mappings.md) 系統資料表的「發行者」和「訂閱者」端進行。 您也可以使用複寫預存程序，以程式設計方式清除這些資料表中的資料。  
  
### <a name="to-manually-clean-up-merge-metadata"></a>若要手動清除合併中繼資料  
  
1.  在發行集資料庫的「發行者」端，執行 [sp_mergemetadataretentioncleanup](../../../relational-databases/system-stored-procedures/sp-mergemetadataretentioncleanup-transact-sql.md)。  
  
2.  (選擇性) 請注意在步驟 1 中從 [MSmerge_genhistory](../../../relational-databases/system-tables/msmerge-genhistory-transact-sql.md)、[MSmerge_contents](../../../relational-databases/system-tables/msmerge-contents-transact-sql.md) 和 [MSmerge_tombstone](../../../relational-databases/system-tables/msmerge-tombstone-transact-sql.md) 系統資料表所移除的資料列數目 (分別以 `@num_genhistory_rows`、`@num_contents_rows` 和 `@num_tombstone_rows` 輸出參數傳回)。  
  
3.  在「訂閱者」端重複步驟 1 和 2，以清除訂閱者資料庫上的中繼資料。  
  
## <a name="see-also"></a>另請參閱  
 [訂閱逾期與停用](../../../relational-databases/replication/subscription-expiration-and-deactivation.md)  
  
  
