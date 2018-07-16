---
title: 清除合併中繼資料 (複寫 Transact-SQL 程式設計) | Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- metadata [SQL Server replication]
- sp_mergemetadataretentioncleanup
ms.assetid: 9b88baea-b7c6-4e5d-88f9-93d6a0ff0368
caps.latest.revision: 32
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 4cf958cdd83858998b8b63bb58bf50d6da632aa9
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37324208"
---
# <a name="clean-up-merge-metadata-replication-transact-sql-programming"></a>清除合併中繼資料 (複寫 Transact-SQL 程式設計)
  合併式複寫中繼資料會由「合併代理程式」依據發行集的保留設定而定期清除。 這項作業會在 [MSmerge_genhistory](/sql/relational-databases/system-tables/msmerge-genhistory-transact-sql)、 [MSmerge_contents](/sql/relational-databases/system-tables/msmerge-contents-transact-sql)、 [MSmerge_tombstone](/sql/relational-databases/system-tables/msmerge-tombstone-transact-sql)、 [MSmerge_past_partition_mappings](/sql/relational-databases/system-tables/msmerge-past-partition-mappings-transact-sql)和 [MSmerge_current_partition_mappings](/sql/relational-databases/system-tables/msmerge-current-partition-mappings) 系統資料表的「發行者」和「訂閱者」端進行。 您也可以使用複寫預存程序，以程式設計方式清除這些資料表中的資料。  
  
### <a name="to-manually-clean-up-merge-metadata"></a>若要手動清除合併中繼資料  
  
1.  在發行集資料庫的「發行者」端，執行 [sp_mergemetadataretentioncleanup](/sql/relational-databases/system-stored-procedures/sp-mergemetadataretentioncleanup-transact-sql)。  
  
2.  (選擇性) 請注意在步驟 1 中從 [MSmerge_genhistory](/sql/relational-databases/system-tables/msmerge-genhistory-transact-sql)、 [MSmerge_contents](/sql/relational-databases/system-tables/msmerge-contents-transact-sql)和 [MSmerge_tombstone](/sql/relational-databases/system-tables/msmerge-tombstone-transact-sql) 系統資料表所移除的資料列數目 (分別以 **@num_genhistory_rows**、 **@num_contents_rows**和 **@num_tombstone_rows** 輸出參數傳回)。  
  
3.  在「訂閱者」端重複步驟 1 和 2，以清除訂閱者資料庫上的中繼資料。  
  
## <a name="see-also"></a>另請參閱  
 [訂閱逾期與停用](../subscription-expiration-and-deactivation.md)  
  
  
