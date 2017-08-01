---
title: MSSQLSERVER_2814 | Microsoft Docs
ms.custom: 
ms.date: 07/11/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 2814 (Database Engine error)
ms.assetid: 22800748-9be9-4511-9428-6b8b40e5bef9
caps.latest.revision: 14
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 109b5a18604b2111f3344ba216a6d3d98131d116
ms.openlocfilehash: 3bca883d9f5b13b81e021014193df43fc3f5f6e3
ms.contentlocale: zh-tw
ms.lasthandoff: 07/31/2017

---
# <a name="mssqlserver2814"></a>MSSQLSERVER_2814
  
## <a name="details"></a>詳細資料  
  
|||  
|-|-|  
|產品名稱|SQL Server|  
|事件識別碼|2814|  
|事件來源|MSSQLSERVER|  
|元件|SQLEngine|  
|符號名稱|PR_POSSIBLE_INFINITE_RECOMPILE|  
|訊息文字|偵測到 SQLHANDLE %hs、PlanHandle %hs、起始位移 %d、結尾位移 %d 可能發生無限重新編譯。 上次重新編譯的原因是 %d。|  
  
## <a name="explanation"></a>說明  
一個或多個陳述式導致此查詢批次重新編譯至少 50 次。 為了避免進一步重新編譯，您應該更正指定的陳述式。  
  
下表列出重新編譯的原因。  
  
|原因代碼|Description|  
|---------------|---------------|  
|1|結構描述已變更|  
|2|統計資料已變更|  
|3|延遲編譯|  
|4|Set 選項已變更|  
|5|Temp 資料表已變更|  
|6|遠端資料列集已變更|  
|7|For Browse 權限已變更|  
|8|查詢通知環境已變更|  
|9|分割區檢視已變更|  
|10|資料指標選項已變更|  
|11|已要求選項 (重新編譯)|  
  
## <a name="user-action"></a>使用者動作  
  
1.  您可以執行下列查詢來檢視導致重新編譯的陳述式。 請將 *sql_handle*、*starting_offset*、*ending_offset* 和 *plan_handle* 預留位置取代成錯誤訊息中指定的值。 針對隨選和備妥的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式，**database_name** 和 **object_name** 資料行為 NULL。  
  
    ```sql   
    SELECT DB_NAME(st.dbid) AS database_name,  
        OBJECT_NAME(st.objectid) AS object_name,  
        st.text  
    FROM sys.dm_exec_query_stats AS qs  
    CROSS APPLY sys.dm_exec_sql_text (*sql_handle*) AS st  
    WHERE qs.statement_start_offset = *starting_offset*  
    AND qs.statement_end_offset = *ending_offset*  
    AND qs.plan_handle = *plan_handle*;
    ```
  
2.  為了避免重新編譯，請根據原因代碼的說明，修改陳述式、批次或程序。 例如，一個預存程序可能會包含一個或多個 SET 陳述式。 您應該從此程序中移除這些陳述式。 如需重新編譯原因和解決方案的其他範例，請參閱 [Batch Compilation, Recompilation, and Plan Caching Issues in SQL Server 2005](http://go.microsoft.com/fwlink/?LinkId=69175)(SQL Server 2005 中的批次編譯、重新編譯及計畫快取問題)。  
  
3.  如果持續發生問題，請連絡 Microsoft 客戶支援服務。  
  
## <a name="see-also"></a>另請參閱  
[SQL:StmtRecompile 事件類別](../event-classes/sql-stmtrecompile-event-class.md)  
  

