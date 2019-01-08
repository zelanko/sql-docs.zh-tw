---
title: 針對平行處理資料倉儲中監視載入 |Microsoft Docs
description: 監視作用中和最近的載入藉由分析平台 System (APS) 系統管理員主控台或平行資料倉儲 (PDW) 系統檢視表。 」
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: cb840c64c2235a2f3902c45633aa5471655482dc
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/27/2018
ms.locfileid: "52413515"
---
# <a name="monitor-loads-into-parallel-data-warehouse"></a>監視載入平行處理資料倉儲
監視作用中和最近[dwloader](dwloader.md)使用 Analytics Platform System (APS) 管理主控台或 Parallel Data Warehouse (PDW) 載入[系統檢視表](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-reference-tsql-system-views/)。 
  
> [!TIP]  
> 某些負載會使用 INSERT 陳述式或使用 SQL 陳述式來執行載入的商業智慧工具來起始。 

<!-- MISSING LINKS
To monitor this type of load, see [Monitoring Active Queries](monitor-active-queries.md).  
-->
  
## <a name="prerequisites"></a>先決條件  
不論用來監視負載的方法，登入必須擁有存取基礎資料來源的權限。 

<!-- MISSING LINKS
For the permissions to grant, see "Use All of the Admin Console" in [Grant Permissions to Use the Admin Console](grant-permissions-admin-console.md). 

--> 
  
## <a name="monitoring-loads"></a>監視載入  
下列各節說明如何監視載入。  
  
### <a name="to-monitor-loads-by-using-the-admin-console"></a>若要使用管理主控台中監視載入  
  
1.  登入系統管理員主控台。 <!-- MISSING LINKS See [Monitor the Appliance by Using the Admin Console;](monitor-admin-console.md) for instructions. --> 
  
2.  在上方功能表中，按一下 **載入**。 您會看到一個可排序的表格，顯示所有最近使用中載入以及其他資訊，例如負載是否已完成，或仍在作用中。 按一下欄標題來排序資料列。  
  
3.  若要檢視特定負載的其他詳細資訊，請按一下 負載**識別碼**左側資料行中。 在詳細檢視中，您可以看到負載的每個步驟的進度。  
  
顯示系統管理員主控台中的負載的相關中繼資料，請參閱這些資訊的系統檢視表：  
  
-   [sys.dm_pdw_exec_requests](../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md)  
  
-   [sys.pdw_loader_run_stages](https://msdn.microsoft.com/library/mt203879.aspx)  
  
-   [sys.pdw_loader_backup_runs](../relational-databases/system-catalog-views/sys-pdw-loader-backup-runs-transact-sql.md)  
  
-   [sys.pdw_loader_backup_run_details](../relational-databases/system-catalog-views/sys-pdw-loader-backup-run-details-transact-sql.md)  
  
### <a name="to-monitor-loads-by-using-system-views"></a>若要使用系統檢視表來監視負載  
若要使用 SQL Server PDW 檢視監視作用中和最近的載入，請遵循下列步驟。 使用每份系統檢視，如該檢視的資訊的文件上的資料行和檢視所傳回的可能值。  
  
1.  尋找`request_id`中的負載[sys.dm_pdw_exec_requests](../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md)檢視中的載入器命令列，找出`command`此檢視的資料行。  
  
    例如，下列命令會傳回命令文字和目前狀態，再加上`request_id`。  
  
    ```sql  
    SELECT request_id, status, command FROM sys.dm_pdw_exec_requests;  
    ```  
  
2.  使用`request_id`來擷取所使用的負載所需的詳細資訊[sys.pdw_loader_run_stages](../relational-databases/system-catalog-views/sys-pdw-loader-run-stages-transact-sql.md) ，以及[sys.pdw_loader_backup_run_details](../relational-databases/system-catalog-views/sys-pdw-loader-backup-run-details-transact-sql.md)檢視。 例如，下列查詢會傳回`run_id`有關開始、 結束時間和持續時間的負載，加上任何錯誤，並處理資料列數目的詳細資訊：  
  
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
  
