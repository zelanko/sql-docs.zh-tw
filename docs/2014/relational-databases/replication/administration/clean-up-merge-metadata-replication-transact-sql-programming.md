---
title: 清除合併中繼資料 (複寫 Transact-SQL 程式設計) | Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: 384b5cc158600848dbca6528a4c8c39250a23908
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "62629176"
---
# <a name="clean-up-merge-metadata-replication-transact-sql-programming"></a>清除合併中繼資料 (複寫 Transact-SQL 程式設計)
  合併式複寫中繼資料會由「合併代理程式」依據發行集的保留設定而定期清除。 這項作業會在 [MSmerge_genhistory](/sql/relational-databases/system-tables/msmerge-genhistory-transact-sql)、 [MSmerge_contents](/sql/relational-databases/system-tables/msmerge-contents-transact-sql)、 [MSmerge_tombstone](/sql/relational-databases/system-tables/msmerge-tombstone-transact-sql)、 [MSmerge_past_partition_mappings](/sql/relational-databases/system-tables/msmerge-past-partition-mappings-transact-sql)和 [MSmerge_current_partition_mappings](/sql/relational-databases/system-tables/msmerge-current-partition-mappings) 系統資料表的「發行者」和「訂閱者」端進行。 您也可以使用複寫預存程序，以程式設計方式清除這些資料表中的資料。  
  
### <a name="to-manually-clean-up-merge-metadata"></a>若要手動清除合併中繼資料  
  
1.  在發行集資料庫的「發行者」端，執行 [sp_mergemetadataretentioncleanup](/sql/relational-databases/system-stored-procedures/sp-mergemetadataretentioncleanup-transact-sql)。  
  
2.  選擇性請注意在步驟1中從[MSmerge_genhistory](/sql/relational-databases/system-tables/msmerge-genhistory-transact-sql)、 [MSmerge_contents](/sql/relational-databases/system-tables/msmerge-contents-transact-sql)和[MSmerge_tombstone](/sql/relational-databases/system-tables/msmerge-tombstone-transact-sql)系統資料表中移除的資料列數目，分別**@num_genhistory_rows**在、 **@num_contents_rows**和**@num_tombstone_rows**輸出參數中傳回。  
  
3.  在「訂閱者」端重複步驟 1 和 2，以清除訂閱者資料庫上的中繼資料。  
  
## <a name="see-also"></a>另請參閱  
 [訂閱逾期與停用](../subscription-expiration-and-deactivation.md)  
  
  
