---
title: 監視載入
description: 使用 Analytics Platform System (AP) 管理主控台或平行資料倉儲 (PDW) 系統檢視），來監視作用中和最近的負載。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 6bc64949b0e636a6c64e7b0ef576613f6e02c5c2
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88777717"
---
# <a name="monitor-loads-into-parallel-data-warehouse"></a>監視負載至平行處理資料倉儲
使用 Analytics Platform System (AP) 管理主控台或平行資料倉儲 (PDW) [系統檢視](/azure/synapse-analytics/sql-data-warehouse/sql-data-warehouse-reference-tsql-system-views)，來監視作用中和最近的[dwloader](dwloader.md)負載。 
  
> [!TIP]  
> 某些負載是利用 INSERT 語句或使用 SQL 語句來執行負載的商業智慧工具來起始。 

<!-- MISSING LINKS
To monitor this type of load, see [Monitoring Active Queries](monitor-active-queries.md).  
-->
  
## <a name="prerequisites"></a>必要條件  
無論用來監視負載的方法為何，登入都必須具有存取基礎資料來源的許可權。 

<!-- MISSING LINKS
For the permissions to grant, see "Use All of the Admin Console" in [Grant Permissions to Use the Admin Console](grant-permissions-admin-console.md). 

--> 
  
## <a name="monitoring-loads"></a>監視負載  
下列各節說明如何監視負載。  
  
### <a name="to-monitor-loads-by-using-the-admin-console"></a>使用管理主控台監視負載  
  
1.  登入管理主控台。 <!-- MISSING LINKS See [Monitor the Appliance by Using the Admin Console;](monitor-admin-console.md) for instructions. --> 
  
2.  在頂端功能表上，按一下 [ **載入**]。 您會看到一個可排序的表格，其中會顯示所有最近和作用中的負載，以及額外的資訊，例如負載是否已完成或仍在使用中。 按一下資料行標頭來排序資料列。  
  
3.  若要查看特定負載的其他詳細資料，請按一下左側資料行中的 [載入 **識別碼** ]。 在詳細的觀點，您可以在負載的每個步驟中看到進度。  
  
如需有關管理主控台中所顯示負載的中繼資料資訊，請參閱這些系統檢視：  
  
-   [sys.dm_pdw_exec_requests](../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md)  
  
-   [sys.pdw_loader_run_stages](../relational-databases/system-catalog-views/sys-pdw-loader-run-stages-transact-sql.md?view=aps-pdw-2016-au7)  
  
-   [sys.pdw_loader_backup_runs](../relational-databases/system-catalog-views/sys-pdw-loader-backup-runs-transact-sql.md)  
  
-   [sys.pdw_loader_backup_run_details](../relational-databases/system-catalog-views/sys-pdw-loader-backup-run-details-transact-sql.md)  
  
### <a name="to-monitor-loads-by-using-system-views"></a>使用系統檢視來監視負載  
若要使用 SQL Server PDW views 來監視使用中和最近的負載，請依照下列步驟執行。 針對所使用的每個系統檢視，請參閱該視圖的檔，以取得有關此視圖所傳回之資料行和潛在值的詳細資訊。  
  
1.  在 `request_id` 此視圖的資料行中尋找載入器命令列，以找出 [sys. dm_pdw_exec_requests](../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md) view 中的負載 `command` 。  
  
    例如，下列命令會傳回命令文字和目前的狀態，以及 `request_id` 。  
  
    ```sql  
    SELECT request_id, status, command FROM sys.dm_pdw_exec_requests;  
    ```  
  
2.  使用 `request_id` 來取得負載的額外資訊，方法是使用 [sys. pdw_loader_run_stages](../relational-databases/system-catalog-views/sys-pdw-loader-run-stages-transact-sql.md) 和 [sys. pdw_loader_backup_run_details](../relational-databases/system-catalog-views/sys-pdw-loader-backup-run-details-transact-sql.md) views。 例如，下列查詢會傳回負載的 `run_id` 開始時間、結束時間和持續時間的相關資訊，以及任何錯誤，以及處理的資料列數目相關資訊：  
  
    ```sql  
    SELECT lbr.run_id,   
    er.submit_time, er.end_time, er.total_elapsed_time, er.error_id, lbr.rows_processed, lbr.rows_rejected, lbr.rows_inserted   
    FROM sys.dm_pdw_exec_requests er   
    LEFT OUTER JOIN   
    sys.pdw_loader_backup_runs lbr   
    ON (er.request_id=lbr.requst_id)   
    WHERE er.request_id='12738';  
    ```  
  
<!-- MISSING LINKS

## See Also  
[Common metadata query examples](metadata-query-examples.md)
-->  
