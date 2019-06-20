---
title: 監視作用中查詢-Parallel Data Warehouse |Microsoft Docs
description: 您可以使用管理主控台和平行處理資料倉儲系統檢視表來監視 Analytics Platform System 上的作用中查詢。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: d2b1ee84b2ae738d7790e1238176331a221ac473
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62640013"
---
# <a name="monitoring-active-queries---parallel-data-warehouse"></a>監視作用中查詢的平行處理資料倉儲
這篇文章會示範如何使用管理主控台和 SQL Server PDW 系統檢視表來監視使用中的查詢。 請參閱[使用管理主控台來監視設備](monitor-the-appliance-by-using-the-admin-console.md)並[系統檢視表](tsql-system-views.md)如需這些工具。  
  
## <a name="prerequisites"></a>先決條件  
不論用來監視使用中查詢的方法，登入必須擁有 「 使用所有的系統管理員主控台 」 中所述的權限[授與權限，才能使用系統管理員主控台](grant-permissions.md#grant-permissions-to-use-the-admin-console)。  
  
## <a name="PermsAdminConsole"></a>監視作用中的查詢  
在管理主控台和 SQL Server PDW 系統檢視表可用來監視使用中的查詢。 請遵循下列指示。  
  
### <a name="to-monitor-active-queries-by-using-the-admin-console"></a>若要使用管理主控台來監視使用中的查詢  
  
1.  登入系統管理員主控台。 請參閱[使用管理主控台來監視設備](monitor-the-appliance-by-using-the-admin-console.md)如需相關指示。  
  
2.  在上方功能表中，按一下 **查詢**。 您會看到具有最新的查詢的基本資訊的資料表上的應用裝置，包括提交的查詢、 查詢和查詢的目前狀態的開始和結束時間的登入。  
  
3.  若要查看查詢命令時，滑鼠指標停留在該資料列左側資料行中的查詢識別碼。  
  
    若要查看更詳細的特定查詢的資訊，請按一下 查詢識別碼。 您會看到資訊，包括完整的查詢和查詢計畫，以針對查詢執行中的每個步驟的狀態資訊。 如果傳回任何錯誤，您也可以查看錯誤的詳細的資訊。 <!-- MISSING LINKS See [Understanding Query Plans &#40;SQL Server PDW&#41;](../sqlpdw/understanding-query-plans-sql-server-pdw.md) for information on how to interpret the query plan information available in the Admin Console.  -->
  
### <a name="to-monitor-active-queries-by-using-the-system-views"></a>若要使用的系統檢視表來監視使用中的查詢  
用來監視查詢的主要系統檢視[sys.dm_pdw_exec_requests](../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md)。 使用此系統檢視表來尋找`request_id`作用中或新的查詢，根據 查詢文字。  
  
例如，下列查詢找出`request_id`和目前`status`針對選取的所有資料行的任何查詢`memberAddresses`資料表。  
  
```sql  
SELECT request_id, command, status   
FROM sys.dm_pdw_exec_requests   
WHERE command   
LIKE '%SELECT * FROM db1..memberAddresses%';  
```  
  
之後`request_id`已識別的查詢，使用中的其他資訊`dm_pdw_exec_requests`資料表，以了解有關在查詢的處理，或使用[sys.dm_pdw_request_steps](../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md)若要檢視個別查詢的狀態查詢執行的步驟。  
  
<!-- MISSING LINKS 
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  
