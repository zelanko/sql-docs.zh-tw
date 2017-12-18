---
title: "檢視資料庫快照集的疏鬆檔案大小 (Transact-SQL) | Microsoft 文件"
ms.date: 07/28/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: databases
ms.reviewer: 
ms.suite: sql
ms.custom: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- snapshots [SQL Server database snapshots], sparse files
- space [SQL Server], sparse files
- sparse files [SQL Server]
- size [SQL Server], sparse files
- maximum sparse file size
- database snapshots [SQL Server], sparse files
- space [SQL Server], database snapshots
ms.assetid: 1867c5f8-d57c-46d3-933d-3642ab0a8e24
caps.latest.revision: "41"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b6434b5e98944ee48b51d3d1c06db0ba94fbda0e
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="view-the-size-of-the-sparse-file-of-a-database-snapshot-transact-sql"></a>檢視資料庫快照集的疏鬆檔案大小 (Transact-SQL)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] 本主題描述如何使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 來確認 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫檔案是疏鬆檔案，以及了解其實際和最大大小。 疏鬆檔案是 NTFS 檔案系統的功能，提供 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫快照集所使用。  
  
> [!NOTE]  
>  資料庫快照集建立期間，可以利用 CREATE DATABASE 陳述式中的檔案名稱，建立疏鬆檔案。 這些檔案名稱儲存在 **physical_name** 資料行的 **sys.master_files** 中。 在 **sys.database_files** (不管是在來源資料庫或快照集) 中， **physical_name** 資料行一律會包含來源資料庫檔案的名稱。  
  
## <a name="verify-that-a-database-file-is-a-sparse-file"></a>確認資料庫檔案是疏鬆檔案  
  
1.  在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的執行個體上：  
  
     從資料庫快照集的 **sys.database_files** 或從 **sys.master_files** 選取 **is_sparse**資料行。 值表示檔案是否為疏鬆檔案，如下所示：  
  
     1 = 檔案是疏鬆檔案。  
  
     0 = 檔案不是疏鬆檔案。  
  
## <a name="find-out-the-actual-size-of-a-sparse-file"></a>查明疏鬆檔案的實際大小  
  
> [!NOTE]  
>  疏鬆檔案是以每次遞增 64 KB 的方式成長；因此磁碟上的疏鬆檔案大小一律是 64 KB 的倍數。  
  
 若要檢視目前在磁碟上使用的快照集之每個疏鬆檔案的位元組數，請查詢 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][sys.dm_io_virtual_file_stats](../../relational-databases/system-dynamic-management-views/sys-dm-io-virtual-file-stats-transact-sql.md) 動態管理檢視的 **size_on_disk_bytes** 資料行。  
  
 若要檢視疏鬆檔案使用的磁碟空間，請以滑鼠右鍵按一下 Microsoft Windows 中的檔案，然後按一下 [內容]並查看 [磁碟大小] 值。  
  
## <a name="find-out-the-maximum-size-of-a-sparse-file"></a>查明疏鬆檔案的大小上限  
 疏鬆檔案的成長大小上限，為建立快照集時對應來源資料庫檔案的大小。 若要知道此大小，您可以使用以下其中一種方式：  
  
-   使用 Windows 命令提示字元：  
  
    1.  使用 Windows **dir** 命令。  
  
    2.  選取疏鬆檔案，在 Windows 中開啟該檔案的 **[內容]** 對話方塊，並查看 **[大小]** 的值。  
  
-   在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的執行個體上：  
  
     從資料庫快照集的 **sys.database_files** 或從 **sys.master_files** 選取 **size**資料行。 在 SQL 頁面中， **size** 資料行的值會反映出快照集可以使用的空間上限；此數值相當於 Windows 的 **[大小]** 欄位，只不過它代表檔案中的 SQL 頁面數；以位元組計算的大小如下：  
  
     ( *頁數* * 8192)  

## <a name="example"></a>範例
下列指令碼會顯示磁碟上每個疏鬆檔案的大小 (以 KB 為單位)。  此指令碼也會顯示疏鬆檔案所能成長的大小上限 (以 MB 為單位)。  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中執行 Transact-SQL 指令碼。

```tsql
SELECT  DB_NAME(sd.source_database_id) AS [SourceDatabase], 
        sd.name AS [Snapshot],
        mf.name AS [Filename], 
        size_on_disk_bytes/1024 AS [size_on_disk (KB)],
        mf2.size/128 AS [MaximumSize (MB)]
FROM sys.master_files mf
JOIN sys.databases sd
    ON mf.database_id = sd.database_id
JOIN sys.master_files mf2
    ON sd.source_database_id = mf2.database_id
    AND mf.file_id = mf2.file_id
CROSS APPLY sys.dm_io_virtual_file_stats(sd.database_id, mf.file_id)
WHERE mf.is_sparse = 1
AND mf2.is_sparse = 0
ORDER BY 1;
```
  
## <a name="see-also"></a>另請參閱  
 [資料庫快照集 &#40;SQL Server&#41;](../../relational-databases/databases/database-snapshots-sql-server.md)   
 [sys.fn_virtualfilestats &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-virtualfilestats-transact-sql.md)   
 [sys.database_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
 [sys.master_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)  
  
  
