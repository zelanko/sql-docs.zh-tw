---
title: 監視載入
description: 流量分析平臺系統（AP）管理主控台或平行資料倉儲（PDW）系統檢視，監視作用中和最近的負載。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: b284fdcef506924c26e452196db6e9518faa1351
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "74400959"
---
# <a name="monitor-loads-into-parallel-data-warehouse"></a>監視載入平行處理資料倉儲
流量分析平臺系統（AP）管理主控台或平行處理資料倉儲（PDW）[系統檢視](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-reference-tsql-system-views/)，監視作用中和最近的[dwloader](dwloader.md)負載。 
  
> [!TIP]  
> 某些負載是使用 INSERT 語句或使用 SQL 語句來執行負載的商業智慧工具來起始。 

<!-- MISSING LINKS
To monitor this type of load, see [Monitoring Active Queries](monitor-active-queries.md).  
-->
  
## <a name="prerequisites"></a>Prerequisites  
不論用來監視負載的方法為何，登入都必須具有存取基礎資料來源的許可權。 

<!-- MISSING LINKS
For the permissions to grant, see "Use All of the Admin Console" in [Grant Permissions to Use the Admin Console](grant-permissions-admin-console.md). 

--> 
  
## <a name="monitoring-loads"></a>監視負載  
下列各節說明如何監視負載。  
  
### <a name="to-monitor-loads-by-using-the-admin-console"></a>使用管理主控台監視負載  
  
1.  登入管理主控台。 <!-- MISSING LINKS See [Monitor the Appliance by Using the Admin Console;](monitor-admin-console.md) for instructions. --> 
  
2.  在頂端功能表上，按一下 [**載入**]。 您會看到一個可排序的資料表，其中顯示所有最近和作用中的載入，以及額外的資訊，例如負載是否已完成或是否仍在作用中。 按一下資料行標頭，即可排序資料列。  
  
3.  若要查看特定負載的其他詳細資料，請按一下左欄中的 [載入**識別碼**]。 在詳細的視圖中，您可以看到每個負載步驟的進度。  
  
如需有關管理主控台中所顯示之負載的中繼資料資訊，請參閱這些系統檢視：  
  
-   [sys.dm_pdw_exec_requests](../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md)  
  
-   [sys.pdw_loader_run_stages](https://msdn.microsoft.com/library/mt203879.aspx)  
  
-   [sys.pdw_loader_backup_runs](../relational-databases/system-catalog-views/sys-pdw-loader-backup-runs-transact-sql.md)  
  
-   [sys.pdw_loader_backup_run_details](../relational-databases/system-catalog-views/sys-pdw-loader-backup-run-details-transact-sql.md)  
  
### <a name="to-monitor-loads-by-using-system-views"></a>若要使用系統檢視來監視負載  
若要使用 SQL Server PDW views 來監視作用中和最近的負載，請遵循下列步驟。 針對使用的每個系統檢視，請參閱該視圖的檔，以取得此視圖所傳回之資料行和可能值的相關資訊。  
  
1.  在此視圖的`command`資料行中尋找載入器命令列，以尋找 [ [sys. dm_pdw_exec_requests](../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md) ] 視圖中的負載。 `request_id`  
  
    例如，下列命令會傳回命令文字和目前狀態，加上`request_id`。  
  
    ```sql  
    SELECT request_id, status, command FROM sys.dm_pdw_exec_requests;  
    ```  
  
2.  使用`request_id`來取得負載的額外資訊，方法是使用[pdw_loader_run_stages](../relational-databases/system-catalog-views/sys-pdw-loader-run-stages-transact-sql.md)和[sys.databases pdw_loader_backup_run_details](../relational-databases/system-catalog-views/sys-pdw-loader-backup-run-details-transact-sql.md) views。 例如，下列查詢會傳回負載的`run_id`開始、結束和持續時間時間的和資訊，加上任何錯誤，以及所處理資料列數目的相關資訊：  
  
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
  
