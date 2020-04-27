---
title: 大量匯入採用最低限度記錄的必要條件 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- minimal logging [SQL Server]
- logged bulk copy [SQL Server]
- logs [SQL Server], minimal logging
- minimally logged operations [SQL Server]
- bulk importing [SQL Server], minimal logging
ms.assetid: bd1dac6b-6ef8-4735-ad4e-67bb42dc4f66
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ccb9642982b8680e4111346298e7a70bbc606dbb
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/26/2020
ms.locfileid: "66011892"
---
# <a name="prerequisites-for-minimal-logging-in-bulk-import"></a>大量匯入中最低限度記錄的先決條件
  如果是完整復原模式之下的資料庫，則大量匯入執行的所有資料列插入作業，都會完整記錄在交易記錄中。 若使用完整復原模式，大型的資料匯入作業可能會使交易記錄檔很快就填滿。 相較之下，在簡單復原模式或大量記錄復原模式之下，大量匯入作業的最少記錄會減少大量匯入作業填滿記錄空間的機會。 最低限度記錄也比完整記錄更有效率。  
  
> [!NOTE]  
>  大量記錄復原模式的設計目的，是要在大量匯入作業期間暫時取代完整復原模式。  
  
## <a name="table-requirements-for-minimally-logging-bulk-import-operations"></a>最低限度記錄大量匯入作業的資料表需求  
 使用最低限度記錄時，目標資料表必須符合下列條件：  
  
-   資料表未被複寫。  
  
-   已指定資料表鎖定 (使用 TABLOCK)。  
  
    > [!NOTE]  
    >  雖然在最低限度記錄的大量匯入作業期間，交易記錄檔中不會記錄資料插入，但每當有新的範圍配置到資料表時， [!INCLUDE[ssDE](../../includes/ssde-md.md)] 仍會記錄範圍配置。  
  
-   資料表不是記憶體最佳化資料表。  
  
 資料表是否能產生最低限度記錄，還需視資料表是否已建立索引而定，若已建立索引，則需考量資料表是否為空白：  
  
-   若資料表沒有索引，則資料頁會使用最低限度記錄。  
  
-   若資料表沒有叢集索引，但有一或多個非叢集索引，則資料頁會一律使用最低限度記錄。 但索引頁的記錄方式，則取決於資料表是否空白：  
  
    -   若資料表空白，則索引頁會使用最低限度記錄。  
  
    -   若資料表不是空白，則索引頁會使用完整記錄。  
  
        > [!NOTE]  
        >  若一開始您以空白資料表與多個批次來進行大量匯入資料，則在第一個批次中，索引頁與資料頁都會使用最低限度記錄，但從第二個批次開始，就只有資料頁會使用最低限度記錄。  
  
-   若資料表有叢集索引但為空白，則資料頁與索引頁都會使用最低限度記錄。 相對地，若資料表有叢集索引且並非空白，則不論復原模式為何，資料頁與索引頁都會使用完整記錄。  
  
    > [!NOTE]  
    >  若一開始您以空白資料表與批次來進行大量匯入資料，則在第一個批次中，索引頁與資料頁都會使用最低限度記錄，但從第二個批次開始，只有資料頁會使用大量記錄。  
  
> [!NOTE]  
>  啟用異動複寫時，即使在大量記錄復原模式下也會完整記錄 BULK INSERT 作業。  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> 相關工作  
  
-   [檢視或變更資料庫的復原模式 &#40;SQL Server&#41;](../backup-restore/view-or-change-the-recovery-model-of-a-database-sql-server.md)  
  

  
## <a name="see-also"></a>另請參閱  
 [復原模式 &#40;SQL Server&#41;](../backup-restore/recovery-models-sql-server.md)   
 [bcp 公用程式](../../tools/bcp-utility.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql)   
 [OPENROWSET &#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql)   
 [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)   
 [資料表提示 &#40;Transact-SQL&#41;](/sql/t-sql/queries/hints-transact-sql-table)   
 [INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/insert-transact-sql)  
  
  
