---
title: "監視使用中的查詢 (SQL Server PDW)"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: sql-non-specified
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: analytics-platform-system
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/13/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bb73f790-0537-414b-8dc2-f1eb69b92362
caps.latest.revision: "7"
ms.openlocfilehash: b2975ef92cb3af808ea5698f1980af3f9d0996d1
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="monitoring-active-queries"></a>監視使用中的查詢
本主題示範如何使用管理主控台和 SQL Server PDW 系統檢視表來監視使用中的查詢。 請參閱[使用管理主控台來監視設備](monitor-the-appliance-by-using-the-admin-console.md)和[系統檢視表](tsql-system-views.md)如需這些工具。  
  
## <a name="prerequisites"></a>必要條件  
不論用來監視使用中查詢的方法，登入必須擁有 「 使用所有的系統管理員主控台 」 中所述的權限[授與權限可使用管理主控台](grant-permissions.md#grant-permissions-to-use-the-admin-console)。  
  
## <a name="PermsAdminConsole"></a>監視使用中的查詢  
系統管理員主控台和 SQL Server PDW 系統檢視表可用來監視使用中的查詢。 請遵循下列指示。  
  
### <a name="to-monitor-active-queries-by-using-the-admin-console"></a>若要使用管理主控台來監視使用中的查詢  
  
1.  登入系統管理員主控台。 請參閱[使用管理主控台來監視設備](monitor-the-appliance-by-using-the-admin-console.md)如需相關指示。  
  
2.  在上方功能表中，按一下 **查詢**。 您會看到具有最新的查詢的基本資訊的資料表上的應用裝置，包括登入提交的查詢、 查詢以及查詢的目前狀態的開始和結束時間。  
  
3.  若要查看 [查詢] 命令，請將滑鼠指標停留在該資料列左側的資料行中的查詢識別碼。  
  
    若要查看更詳細的特定查詢資訊，請按一下 查詢識別碼。 您會看到資訊，包括完整的查詢和查詢計畫，以針對查詢執行中的每個步驟的狀態資訊。 如果傳回任何錯誤，您也可以查看詳細的資訊的錯誤。 <!-- MISSING LINKS See [Understanding Query Plans &#40;SQL Server PDW&#41;](../sqlpdw/understanding-query-plans-sql-server-pdw.md) for information on how to interpret the query plan information available in the Admin Console.  -->
  
### <a name="to-monitor-active-queries-by-using-the-system-views"></a>若要使用系統檢視表來監視使用中的查詢  
用來監視查詢的主要系統檢視是[sys.dm_pdw_exec_requests](../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md)。 使用這個系統檢視表來尋找`request_id`作用中或新的查詢，根據查詢文字。  
  
例如，下列查詢會尋找`request_id`和目前`status`選取所有資料行，從任何查詢`memberAddresses`資料表。  
  
```sql  
SELECT request_id, command, status   
FROM sys.dm_pdw_exec_requests   
WHERE command   
LIKE ‘%SELECT * FROM db1..memberAddresses%’;  
```  
  
之後`request_id`已識別的查詢，使用中的其他資訊`dm_pdw_exec_requests`資料表若要了解在查詢的處理，或使用[sys.dm_pdw_request_steps](../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md)若要檢視個別查詢的狀態查詢執行的步驟。  
  
<!-- MISSING LINKS 
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  
