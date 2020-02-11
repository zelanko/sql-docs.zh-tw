---
title: 監視使用中查詢
description: 使用管理主控台和平行處理資料倉儲系統檢視來監視分析平臺系統上的使用中查詢。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 9157db745b999711966f0019747ba1d61823569e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "74400917"
---
# <a name="monitoring-active-queries---parallel-data-warehouse"></a>監視使用中查詢-平行處理資料倉儲
本文說明如何使用管理主控台和 SQL Server PDW 系統檢視來監視作用中的查詢。 如需這些工具的資訊，請參閱[使用管理主控台](monitor-the-appliance-by-using-the-admin-console.md)和[系統檢視](tsql-system-views.md)來監視設備。  
  
## <a name="prerequisites"></a>Prerequisites  
不論用來監視作用中查詢的方法為何，登入都必須具有[授與許可權以使用管理主控台](grant-permissions.md#grant-permissions-to-use-the-admin-console)中的「使用所有管理主控台」中所述的許可權。  
  
## <a name="PermsAdminConsole"></a>監視使用中查詢  
管理主控台和 SQL Server PDW 系統檢視都可用來監視使用中的查詢。 請遵循下列指示：  
  
### <a name="to-monitor-active-queries-by-using-the-admin-console"></a>使用管理主控台監視作用中的查詢  
  
1.  登入管理主控台。 如需相關指示，請參閱[使用管理主控台來監視設備](monitor-the-appliance-by-using-the-admin-console.md)。  
  
2.  在頂端功能表上，按一下 [**查詢**]。 您會看到一個資料表，其中包含設備上最近查詢的基本資訊，包括提交查詢的登入、查詢的開始和結束時間，以及查詢的目前狀態。  
  
3.  若要查看查詢命令，請將滑鼠指標停留在該資料列左側資料行中的查詢識別碼上。  
  
    若要查看特定查詢的詳細資訊，請按一下查詢識別碼。 您會看到包含完整查詢和查詢計劃的資訊，以及查詢執行中每個步驟的狀態資訊。 如果傳回任何錯誤，您也可以查看錯誤的詳細資訊。 <!-- MISSING LINKS See [Understanding Query Plans &#40;SQL Server PDW&#41;](../sqlpdw/understanding-query-plans-sql-server-pdw.md) for information on how to interpret the query plan information available in the Admin Console.  -->
  
### <a name="to-monitor-active-queries-by-using-the-system-views"></a>若要使用系統檢視來監視作用中的查詢  
用來監視查詢的主要系統檢視是[sys. dm_pdw_exec_requests](../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md)。 使用此系統檢視，根據查詢`request_id`文字尋找作用中或最近查詢的。  
  
例如，下列查詢會針對從`request_id` `status` `memberAddresses`資料表中選取所有資料行的任何查詢，尋找和目前的。  
  
```sql  
SELECT request_id, command, status   
FROM sys.dm_pdw_exec_requests   
WHERE command   
LIKE '%SELECT * FROM db1..memberAddresses%';  
```  
  
`request_id`識別查詢的之後，請使用`dm_pdw_exec_requests`資料表中的其他資訊來瞭解查詢的處理方式，或使用[dm_pdw_request_steps sys.databases](../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md)來查看查詢執行之個別查詢步驟的狀態。  
  
<!-- MISSING LINKS 
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  
