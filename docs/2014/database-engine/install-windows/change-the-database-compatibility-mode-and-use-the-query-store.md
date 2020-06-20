---
title: 遷移查詢計劃 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- query plans [SQL Server], migrating
- upgrading SQL Server, migrating query plans
- plan guides [SQL Server], migrating query plans
ms.assetid: 7e02a137-6867-4f6a-a45a-2b02674f7e65
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: dafd3a5f8a460bb08e63919c2cb853ad74dc2f1f
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/17/2020
ms.locfileid: "84932755"
---
# <a name="migrate-query-plans"></a>移轉查詢計劃
  在大多數的情況下，將資料庫升級到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的最新版，可提升查詢效能。 但是，如果您的關鍵任務查詢已針對效能謹慎地加以微調，您可能會想要在升級之前為這些查詢保留查詢計劃，透過的方式是為每一個查詢建立計畫指南。 如果在升級之後，查詢最佳化工具針對一個或多個查詢選擇比較沒有效率的計畫，您可啟用計畫指南，並強制查詢最佳化工具使用升級前計畫。  
  
 若要在升級之前建立計畫指南，請遵循以下步驟：  
  
1.  使用[sp_create_plan_guide](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql)預存程式，並在 USE plan 查詢提示中指定查詢計劃，記錄每個任務關鍵性查詢的目前計畫。  
  
2.  確認此計畫指南已套用到查詢。  
  
3.  將資料庫升級為新版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
     計畫會保存在升級資料庫的計畫指南中，而且會在升級之後的計畫退步情況下當做後援。  
  
     我們建議您在升級之後不要啟用計畫指南，因為您可能會因為更新的統計資料，而遺失在新版中擁有更佳計畫或有幫助的重新編譯機會。  
  
4.  如果在升級之後選擇了比較沒有效率的計畫，請啟動計畫指南的全部或子集來覆寫新的計畫。  
  
## <a name="example"></a>範例  
 下列範例會示範如何藉由建立計畫指南來為查詢記錄升級前計畫。  
  
### <a name="step-1-collect-the-plan"></a>步驟 1：收集計畫  
 計畫指南中所記錄的查詢計劃必須使用 XML 格式。 XML 格式的查詢計劃可透過下列方式來產生：  
  
-   [SET SHOWPLAN_XML](/sql/t-sql/statements/set-showplan-xml-transact-sql)  
  
-   [SET STATISTICS XML](/sql/t-sql/statements/set-statistics-xml-transact-sql)  
  
-   查詢[sys.databases dm_exec_query_plan](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-transact-sql)動態管理函數的 query_plan 資料行。  
  
-   [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)][查詢編譯](../../relational-databases/event-classes/showplan-xml-for-query-compile-event-class.md)事件類別的執行程式表[xml](../../relational-databases/event-classes/showplan-xml-event-class.md)、執行程式表 xml[統計資料設定檔](../../relational-databases/event-classes/showplan-xml-statistics-profile-event-class.md)和顯示計畫 xml。  
  
 下列範例會藉由查詢動態管理檢視來為 `SELECT City, StateProvinceID, PostalCode FROM Person.Address ORDER BY PostalCode DESC;` 陳述式收集查詢計畫。  
  
```  
USE AdventureWorks;  
GO  
SELECT query_plan  
    FROM sys.dm_exec_query_stats AS qs   
    CROSS APPLY sys.dm_exec_sql_text(qs.sql_handle) AS st  
    CROSS APPLY sys.dm_exec_text_query_plan(qs.plan_handle, DEFAULT, DEFAULT) AS qp  
    WHERE st.text LIKE N'SELECT City, StateProvinceID, PostalCode FROM Person.Address ORDER BY PostalCode DESC;%';  
GO  
```  
  
### <a name="step-2-create-the-plan-guide-to-force-the-plan"></a>步驟 2：建立計畫指南以強制計畫  
 在計畫指南中使用 XML 格式的查詢計畫 (由上述的任何一個方法取得)，可在 sp_create_plan_guide 的 OPTION 子句中所指定的 USE PLAN 查詢提示內，以字串常值的形式複製並貼上查詢計畫。  
  
 在 XML 計畫本身內，以第二個引號逸出計畫中所出現的引號 (')，然後再建立計畫指南。 例如，含有 `WHERE A.varchar = 'This is a string'` 的計畫必須將程式碼修改為 `WHERE A.varchar = ''This is a string''` 而加以逸出。  
  
 下列範例會針對步驟 1 收集的查詢計劃建立計畫指南，並將此查詢的 XML 執行程序表插入 `@hints` 參數內。 為了簡潔起見，只有部分的執行程序表輸出包含在此範例中。  
  
```  
EXECUTE sp_create_plan_guide   
@name = N'Guide1',  
@stmt = N'SELECT City, StateProvinceID, PostalCode FROM Person.Address ORDER BY PostalCode DESC;',  
@type = N'SQL',  
@module_or_batch = NULL,  
@params = NULL,  
@hints = N'OPTION(USE PLAN N''<ShowPlanXML xmlns=''''https://schemas.microsoft.com/sqlserver/2004/07/showplan''''   
    Version=''''0.5'''' Build=''''9.00.1116''''>  
    <BatchSequence><Batch><Statements><StmtSimple>  
    ...  
    </StmtSimple></Statements></Batch>  
    </BatchSequence></ShowPlanXML>'')';  
GO  
```  
  
### <a name="step-3-verify-that-the-plan-guide-is-applied-to-the-query"></a>步驟 3：確認此計畫指南已套用到查詢  
 再次執行此查詢，並檢查所產生的查詢計劃。 您應該會發現此計畫符合您在計畫指南中所指定的計畫。  
  
## <a name="see-also"></a>另請參閱  
 [sp_create_plan_guide &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql)   
 [查詢提示 &#40;Transact-SQL&#41;](/sql/t-sql/queries/hints-transact-sql-query)   
 [計畫指南](../../relational-databases/performance/plan-guides.md)  
  
  
