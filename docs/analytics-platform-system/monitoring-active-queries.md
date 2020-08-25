---
title: 監視使用中的查詢
description: 使用管理主控台和平行處理資料倉儲系統檢視，來監視 Analytics Platform System 上的作用中查詢。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 9157db745b999711966f0019747ba1d61823569e
ms.sourcegitcommit: 33e774fbf48a432485c601541840905c21f613a0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/25/2020
ms.locfileid: "74400917"
---
# <a name="monitoring-active-queries---parallel-data-warehouse"></a>監視主動式查詢-平行處理資料倉儲
本文說明如何使用管理主控台和 SQL Server PDW 系統檢視來監視使用中的查詢。 如需這些工具的詳細資訊，請參閱 [使用管理主控台](monitor-the-appliance-by-using-the-admin-console.md) 和 [系統檢視](tsql-system-views.md) 來監視設備。  
  
## <a name="prerequisites"></a>先決條件  
無論使用哪一種方法來監視使用中的查詢，登入都必須具備 [授與許可權以使用管理主控台](grant-permissions.md#grant-permissions-to-use-the-admin-console)的 [使用所有管理主控台] 中所述的許可權。  
  
## <a name="monitor-active-queries"></a><a name="PermsAdminConsole"></a>監視使用中的查詢  
系統管理主控台和 SQL Server PDW 系統檢視都可用來監視使用中的查詢。 請遵循下列指示：  
  
### <a name="to-monitor-active-queries-by-using-the-admin-console"></a>使用管理主控台監視使用中的查詢  
  
1.  登入管理主控台。 如需相關指示，請參閱 [使用管理主控台監視設備](monitor-the-appliance-by-using-the-admin-console.md) 。  
  
2.  在頂端功能表上，按一下 [ **查詢**]。 您會看到一份資料表，其中包含設備上最近查詢的基本資訊，包括提交查詢的登入、查詢的開始和結束時間，以及查詢的目前狀態。  
  
3.  若要查看查詢命令，請將滑鼠指標暫留在該資料列左側資料行中的查詢識別碼上方。  
  
    若要查看特定查詢的詳細資訊，請按一下 [查詢識別碼]。 您將會看到包含完整查詢和查詢計劃的資訊，以及查詢執行中每個步驟的狀態資訊。 如果傳回任何錯誤，您也可以查看錯誤的詳細資訊。 <!-- MISSING LINKS See [Understanding Query Plans &#40;SQL Server PDW&#41;](../sqlpdw/understanding-query-plans-sql-server-pdw.md) for information on how to interpret the query plan information available in the Admin Console.  -->
  
### <a name="to-monitor-active-queries-by-using-the-system-views"></a>使用系統檢視來監視使用中的查詢  
用來監視查詢的主要系統檢視是 [sys. dm_pdw_exec_requests](../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md)。 您可以使用這個系統檢視 `request_id` ，根據查詢文字來尋找使用中或最近的查詢。  
  
例如，下列查詢 `request_id` `status` 會尋找從資料表中選取所有資料行之查詢的和目前 `memberAddresses` 。  
  
```sql  
SELECT request_id, command, status   
FROM sys.dm_pdw_exec_requests   
WHERE command   
LIKE '%SELECT * FROM db1..memberAddresses%';  
```  
  
在 `request_id` 識別出查詢之後，請使用資料表中的其他資訊來瞭解 `dm_pdw_exec_requests` 查詢的處理方式，或使用 [sys. dm_pdw_request_steps](../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md) 來查看查詢執行之個別查詢步驟的狀態。  
  
<!-- MISSING LINKS 
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  
