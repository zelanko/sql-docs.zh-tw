---
title: "計畫指南 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-plan-guides
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- TEMPLATE plan guide
- SQL plan guides
- OPTIMIZE FOR query hint
- RECOMPILE query hint
- OBJECT plan guide
- plan guides [SQL Server], about plan guides
- OPTION clause
- plan guides [SQL Server]
- USE PLAN query hint
ms.assetid: bfc97632-c14c-4768-9dc5-a9c512f6b2bd
caps.latest.revision: 52
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: e3c1733219769d0a2d08996db9a25e3dd08a1e86
ms.contentlocale: zh-tw
ms.lasthandoff: 04/11/2017

---
# <a name="plan-guides"></a>計畫指南
  當您無法或不想要在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]中直接變更實際查詢的文字時，您可以使用計畫指南來最佳化查詢的效能。 計畫指南是將查詢提示或固定的查詢計畫附加至查詢，藉以影響查詢的最佳化。 當協力廠商所提供的資料庫應用程式中有少量查詢子集的執行情況不如預期時，使用計畫指南會非常有用。 在計畫指南中，指定您要最佳化的 Transact-SQL 陳述式以及包含您想要使用之查詢提示的 OPTION 子句，或者是您想要用來將查詢進行最佳化的特定查詢計畫。 執行查詢時， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會比對 Transact-SQL 陳述式與計畫指南，然後在執行階段中，將 OPTION 子句附加至查詢或使用指定的查詢計畫。  
  
 您可以建立的計畫指南總數僅限於可用的系統資源。 因此，您應該限制計畫指南，只用於可改善或穩定效能的關鍵任務查詢。 計畫指南不應用來影響已部署之應用程式的大部分查詢負載。  
  
> [!NOTE]  
>  並非每個 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]版本都可使用計劃指南。 如需 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]版本支援的功能清單，請參閱 [SQL Server 2016 版本支援的功能](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)。 在任何版本中都可以看到計畫指南。 您也可以將包含計畫指南的資料庫附加到任何版本中。 當您將資料庫還原或附加至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的升級版本時，計畫指南仍維持不變。  
  
## <a name="types-of-plan-guides"></a>計畫指南的類型  
 您可以建立下列類型的計畫指南。  
  
 OBJECT 計畫指南  
 OBJECT 計畫指南可搭配在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 預存程序、純量使用者定義函數、多個陳述式資料表值使用者定義函數以及 DML 觸發程序內容中執行的查詢。  
  
 假設下列採用 `@Country`_`region` 參數的預存程序位於針對 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫所部署的資料庫應用程式中：  
  
```  
CREATE PROCEDURE Sales.GetSalesOrderByCountry (@Country_region nvarchar(60))  
AS  
BEGIN  
    SELECT *  
    FROM Sales.SalesOrderHeader AS h, Sales.Customer AS c,   
        Sales.SalesTerritory AS t  
    WHERE h.CustomerID = c.CustomerID  
        AND c.TerritoryID = t.TerritoryID  
        AND CountryRegionCode = @Country_region  
END;  
```  
  
 假設此預存程序已針對 `@Country`_`region = N'AU'` (澳洲) 編譯及最佳化。 不過，由於來自澳洲的銷售訂單相當少，因此當查詢在多個銷售訂單上使用國家 (地區) 的參數值執行時，效能就會降低。 由於大部分的銷售訂單都是來自美國，所以針對 `@Country`\_`region = N'US'` 所產生的查詢計劃可能會比 `@Country`\_`region` 參數的所有可能值具有更好的執行效能。  
  
 您可以修改預存程序並將 `OPTIMIZE FOR` 查詢提示加入查詢以處理此問題。 不過，因為預存程序是在已部署的應用程式中，所以您無法直接修改應用程式的程式碼。 您只能在 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫中建立下列計畫指南。  
  
```  
sp_create_plan_guide   
@name = N'Guide1',  
@stmt = N'SELECT *FROM Sales.SalesOrderHeader AS h,  
        Sales.Customer AS c,  
        Sales.SalesTerritory AS t  
        WHERE h.CustomerID = c.CustomerID   
            AND c.TerritoryID = t.TerritoryID  
            AND CountryRegionCode = @Country_region',  
@type = N'OBJECT',  
@module_or_batch = N'Sales.GetSalesOrderByCountry',  
@params = NULL,  
@hints = N'OPTION (OPTIMIZE FOR (@Country_region = N''US''))';  
```  
  
 執行在 `sp_create_plan_guide` 陳述式中指定的查詢時，在最佳化前會先修改查詢以包含 `OPTIMIZE FOR (@Country = N''US'')` 子句。  
  
 SQL 計畫指南  
 SQL 計畫指南可搭配在不屬於資料庫物件的獨立 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式與批次內容中執行的查詢。 以 SQL 為基礎的計畫指南可用以搭配參數化為指定形式的查詢。 SQL 計畫指南會套用至獨立 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式和批次。 這些陳述式通常是由應用程式使用 [sp_executesql](../../relational-databases/system-stored-procedures/sp-executesql-transact-sql.md) 系統預存程序進行提交。 例如，請考慮下列獨立批次：  
  
```  
SELECT TOP 1 * FROM Sales.SalesOrderHeader ORDER BY OrderDate DESC;  
```  
  
 若要防止這項查詢產生平行執行計畫，請建立下列計畫指南並將 `MAXDOP` 參數中的 `1` 查詢提示設定為 `@hints` 。  
  
```  
sp_create_plan_guide   
@name = N'Guide2',   
@stmt = N'SELECT TOP 1 * FROM Sales.SalesOrderHeader ORDER BY OrderDate DESC',  
@type = N'SQL',  
@module_or_batch = NULL,   
@params = NULL,   
@hints = N'OPTION (MAXDOP 1)';  
```  
  
> [!IMPORTANT]  
>  針對 `@module_or_batch` 陳述式的 `@params` 與 `sp_create_plan guide` 引數所提供的值必須符合在實際查詢中所提交的對應文字。 如需詳細資訊，請參閱 [sp_create_plan_guide &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md) 陳述式的 [使用 SQL Server Profiler 建立及測試計畫指南](../../relational-databases/performance/use-sql-server-profiler-to-create-and-test-plan-guides.md)中直接變更實際查詢的文字時，您可以使用計畫指南來最佳化查詢的效能。  
  
 當 PARAMETERIZATION 資料庫選項 SET 為 FORCED 時，或是當建立 TEMPLATE 計畫指南以指定要參數化的查詢類別時，SQL 計畫指南也可在參數化為相同形式的查詢上建立 SQL 計畫指南。  
  
 TEMPLATE 計畫指南  
 TEMPLATE 計畫指南可搭配參數化為指定形式的獨立查詢。 這些計畫指南可用以針對查詢類別，覆寫資料庫目前的 PARAMETERIZATION 資料庫 SET 選項。  
  
 您可以在下列其中一種情況下建立 TEMPLATE 計畫指南：  
  
-   PARAMETERIZATION 資料庫選項設定成 FORCED，但有一些要根據簡單參數化規則編譯的查詢。  
  
-   PARAMETERIZATION 資料庫選項設定成 SIMPLE (預設值)，但是您要在某個查詢類別嘗試強制參數化。  
  
## <a name="plan-guide-matching-requirements"></a>計畫指南比對需求  
 計畫指南的範圍僅限於建立它們的資料庫。 因此，當查詢執行時，只有位於目前資料庫中的計畫指南才可以配合查詢。 例如，如果 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 是目前的資料庫且執行下列查詢：  
  
 `SELECT FirstName, LastName FROM Person.Person;`  
  
 只有在 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 資料庫中的計畫指南能夠配合此查詢。 不過，如果 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 是目前的資料庫且執行下列陳述式：  
  
 `USE DB1;`  
  
 `SELECT FirstName, LastName FROM Person.Person;`  
  
 只有 `DB1` 中的計畫指南才能夠配合查詢，因為查詢是在 `DB1`的內容中執行。  
  
 對於以 SQL 或 TEMPLATE 為基礎的計畫指南而言，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 會逐字元比較查詢的 @module_or_batch 和 @params 引數值，使兩個值相符。 這表示您必須提供與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在實際批次中所收到的文字完全相符的文字。  
  
 @type = 'SQL' 且 @module_or_batch 設定為 NULL 時，@module_or_batch 的值會設定為值 @stmt。 這表示，提供的 *statement_text* 值必須與提交給 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的值採用相同的格式 (逐字元)。 不會執行內部轉換來簡化這個比對作業。  
  
 當一般 (SQL 或 OBJECT) 計畫指南和 TEMPLATE 計畫指南都適用於陳述式時，只會使用一般計畫指南。  
  
> [!NOTE]  
>  在包含要建立計劃指南的陳述式之批次中，將無法包含 USE *database* 陳述式。  
  
## <a name="plan-guide-effect-on-the-plan-cache"></a>計畫指南對於計畫快取的影響  
 針對某個模組建立計畫指南時，就會從計畫快取中移除該模組的查詢計畫。 針對某個批次建立 OBJECT 或 SQL 類型的計畫指南時，就會移除具有相同雜湊值之批次的查詢計畫。 建立 TEMPLATE 類型的計畫指南時，就會從該資料庫內部的計畫快取中移除所有單一陳述式批次。  
  
## <a name="related-tasks"></a>相關工作  
  
|工作|主題|  
|----------|-----------|  
|描述如何建立計畫指南。|[建立新的計畫指南](../../relational-databases/performance/create-a-new-plan-guide.md)|  
|描述如何建立參數化查詢的計畫指南。|[建立參數化查詢的計畫指南](../../relational-databases/performance/create-a-plan-guide-for-parameterized-queries.md)|  
|描述如何使用計畫指南控制查詢參數化行為。|[使用計畫指南指定查詢參數化行為](../../relational-databases/performance/specify-query-parameterization-behavior-by-using-plan-guides.md)|  
|描述如何將固定的查詢計畫併入計畫指南。|[將固定的查詢計畫套用至計畫指南](../../relational-databases/performance/apply-a-fixed-query-plan-to-a-plan-guide.md)|  
|描述如何在計畫指南中指定查詢提示。|[將查詢提示附加至計畫指南](../../relational-databases/performance/attach-query-hints-to-a-plan-guide.md)|  
|描述如何檢視計畫指南屬性。|[檢視計畫指南屬性](../../relational-databases/performance/view-plan-guide-properties.md)|  
|描述如何使用 SQL Server Profiler 建立和測試計畫指南。|[使用 SQL Server Profiler 建立及測試計畫指南](../../relational-databases/performance/use-sql-server-profiler-to-create-and-test-plan-guides.md)|  
|描述如何驗證計畫指南。|[升級之後驗證計畫指南](../../relational-databases/performance/validate-plan-guides-after-upgrade.md)|  
  
## <a name="see-also"></a>另請參閱  
 [sp_create_plan_guide &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)   
 [sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md)   
 [sp_control_plan_guide &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-control-plan-guide-transact-sql.md)   
 [sys.plan_guides &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-plan-guides-transact-sql.md)   
 [sys.fn_validate_plan_guide &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-validate-plan-guide-transact-sql.md)  
  
  

