---
title: sp_create_plan_guide_from_handle (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_create_plan_guide_from_handle_TSQL
- sp_create_plan_guide_from_handle
dev_langs:
- TSQL
helpviewer_keywords:
- sp_create_plan_guide_from_handle
ms.assetid: 02cfb76f-a0f9-4b42-a880-1c3e7d64fe41
caps.latest.revision: 34
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: c57ad0976f2079fb1f5129b1cea59817157af01a
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
ms.locfileid: "33239378"
---
# <a name="spcreateplanguidefromhandle-transact-sql"></a>sp_create_plan_guide_from_handle (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  從計畫快取中的查詢計畫建立一個或多個計畫指南。 您可以使用這個預存程序來確保查詢最佳化工具永遠針對指定的查詢，使用特定的查詢計畫。 如需有關計畫指南的詳細資訊，請參閱 [計畫指南](../../relational-databases/performance/plan-guides.md)。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_create_plan_guide_from_handle [ @name = ] N'plan_guide_name'  
    , [ @plan_handle = ] plan_handle  
    , [ [ @statement_start_offset = ] { statement_start_offset | NULL } ]  
```  
  
## <a name="arguments"></a>引數  
 [ @name =] N'*plan_guide_name*'  
 計畫指南的名稱。 計畫指南名稱僅限於目前的資料庫。 *plan_guide_name*必須遵守的規則[識別碼](../../relational-databases/databases/database-identifiers.md)而且開頭不能是數字符號 （#）。 最大長度*plan_guide_name*為 124 個字元。  
  
 [ @plan_handle =] *plan_handle*  
 識別工作負載中的批次。 *plan_handle*是**varbinary(64)**。 *plan_handle*可以取自[sys.dm_exec_query_stats](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)動態管理檢視。  
  
 [ @statement_start_offset =] { *statement_start_offset* |NULL}]  
 識別指定的批次內之陳述式的開始位置*plan_handle*。 *statement_start_offset*是**int**，預設值是 NULL。  
  
 陳述式位移會對應到中的 statement_start_offset 資料行[sys.dm_exec_query_stats](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)動態管理檢視。  
  
 指定 NULL 時，或者未指定陳述式位移時，系統會使用指定之計畫控制代碼的查詢計畫，在批次中建立每個陳述式的計畫指南。 所產生之計畫指南相當於使用 USE PLAN 查詢提示強制使用特定之計畫的計畫指南。  
  
## <a name="remarks"></a>備註  
 並非所有陳述式類型都可以建立計畫指南。 如果無法在批次中建立陳述式的計畫指南，預存程序會忽略該陳述式，並繼續批次中的下一個陳述式。 如果有陳述式在相同批次中多次發生，會啟用最後發生之陳述式的計畫，而且會停用該陳述式之前的計畫。 如果批次中沒有陳述式可用於計畫指南，則會發生錯誤 10532，而且陳述式將會失敗。 建議您一律從 sys.dm_exec_query_stats 動態管理檢視取得計畫控制代碼以防止發生這個錯誤的可能性。  
  
> [!IMPORTANT]  
>  sp_create_plan_guide_from_handle 會根據出現在計畫快取中的計畫，建立計畫指南。 也就是說，批次文字、[!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式與 XML 執行程序表都是從計畫快取逐字元取得 (包括傳遞至查詢的任何常值)，並放入所產生的計畫指南中。 這些文字字串可能包含之後會儲存到資料庫之中繼資料中的機密資訊。 具有適當的權限的使用者可以使用 sys.plan_guides 目錄檢視，檢視這項資訊和**計畫指南屬性** 對話方塊中的[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。 為確保機密資訊不會透過計畫指南而遭到揭露，建議您檢閱從計畫快取建立的計畫指南。  
  
## <a name="creating-plan-guides-for-multiple-statements-within-a-query-plan"></a>針對查詢計畫內的多個陳述式建立計畫指南  
 諸如 sp_create_plan_guide、sp_create_plan_guide_from_handle 等會從計畫快取移除目標批次或模組的快取計畫。 這個動作的目的在於確保所有使用者都開始使用新的計畫指南。 針對單一查詢計畫內的多個陳述式建立計畫指南時，您可以在明確交易中建立所有計畫指南，藉以延後移除快取中的計畫。 此方法可讓計畫保留在快取中，直到異動完成並建立每個指定陳述式的計畫指南為止。 請參閱範例 B。  
  
## <a name="permissions"></a>Permissions  
 需要 VIEW SERVER STATE 權限。 此外，使用 sp_create_plan_guide_from_handle 建立的每個計畫指南都需要個別的權限。 若要建立類型為 OBJECT 的計畫指南，需要所參考物件的 ALTER 權限。 若要建立類型為 SQL 或 TEMPLATE 的計畫指南，需要目前資料庫的 ALTER 權限。 若要判斷將要建立的計畫指南類型，請執行下列查詢：  
  
```  
SELECT cp.plan_handle, sql_handle, st.text, objtype   
FROM sys.dm_exec_cached_plans AS cp  
JOIN sys.dm_exec_query_stats AS qs ON cp.plan_handle = qs.plan_handle  
CROSS APPLY sys.dm_exec_sql_text(sql_handle) AS st;  
```  
  
 在包含您要為其建立計畫指南之陳述式的資料列中，檢查結果集中的 `objtype` 資料行。 值為 `Proc` 時，表示計畫指南的類型為 OBJECT。 諸如 `AdHoc` 或 `Prepared` 的其他值則表示計畫指南的類型為 SQL。  
  
## <a name="examples"></a>範例  
  
### <a name="a-creating-a-plan-guide-from-a-query-plan-in-the-plan-cache"></a>A. 從工作快取的查詢計畫建立計畫指南  
 下列範例會從計畫快取指定查詢計畫，藉以建立單一 SELECT 陳述式的計畫指南。 範例一開始會執行簡單的 `SELECT` 陳述式，藉以建立計畫指南。 此查詢的計畫會透過 `sys.dm_exec_sql_text` 和 `sys.dm_exec_text_query_plan` 動態管理檢視加以檢查。 然後會在與該查詢相關聯之計畫快取中指定查詢計畫，便可建立該查詢的計畫指南。 範例中的最後一個陳述式會確認該計畫指南是否存在。  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT WorkOrderID, p.Name, OrderQty, DueDate  
FROM Production.WorkOrder AS w   
JOIN Production.Product AS p ON w.ProductID = p.ProductID  
WHERE p.ProductSubcategoryID > 4  
ORDER BY p.Name, DueDate;  
GO  
-- Inspect the query plan by using dynamic management views.  
SELECT * FROM sys.dm_exec_query_stats AS qs  
CROSS APPLY sys.dm_exec_sql_text(sql_handle)  
CROSS APPLY sys.dm_exec_text_query_plan(qs.plan_handle, qs.statement_start_offset, qs.statement_end_offset) AS qp  
WHERE text LIKE N'SELECT WorkOrderID, p.Name, OrderQty, DueDate%';  
GO  
-- Create a plan guide for the query by specifying the query plan in the plan cache.  
DECLARE @plan_handle varbinary(64);  
DECLARE @offset int;  
SELECT @plan_handle = plan_handle, @offset = qs.statement_start_offset  
FROM sys.dm_exec_query_stats AS qs  
CROSS APPLY sys.dm_exec_sql_text(sql_handle) AS st  
CROSS APPLY sys.dm_exec_text_query_plan(qs.plan_handle, qs.statement_start_offset, qs.statement_end_offset) AS qp  
WHERE text LIKE N'SELECT WorkOrderID, p.Name, OrderQty, DueDate%';  
  
EXECUTE sp_create_plan_guide_from_handle   
    @name =  N'Guide1',  
    @plan_handle = @plan_handle,  
    @statement_start_offset = @offset;  
GO  
-- Verify that the plan guide is created.  
SELECT * FROM sys.plan_guides  
WHERE scope_batch LIKE N'SELECT WorkOrderID, p.Name, OrderQty, DueDate%';  
GO  
```  
  
### <a name="b-creating-multiple-plan-guides-for-a-multistatement-batch"></a>B. 建立多項多重陳述式的計畫指南  
 下列範例會針對多重陳述式批次內的兩個陳述式，建立計畫指南。 在明確交易內建立計畫指南，如此一來，在建立第一個計畫指南後，就不會從計畫快取中移除該批次的查詢計畫。 範例一開始會執行多重陳述式批次。 批次的計畫會透過動態管理檢視加以檢查。 請注意，系統會傳回批次中每個陳述式的資料列。 然後藉由指定 `@statement_start_offset` 參數，便會針對批次中的第一個和第三個陳述式建立計畫指南。 範例中的最後一個陳述式會確認這些計畫指南是否存在。  
  
 [!code-sql[PlanGuides#Create_From_Handle2](../../relational-databases/system-stored-procedures/codesnippet/tsql/sp-create-plan-guide-fro_1.sql)]  
  
## <a name="see-also"></a>另請參閱  
 [Database Engine 預存程序&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [sys.dm_exec_query_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)   
 [計畫指南](../../relational-databases/performance/plan-guides.md)   
 [sp_create_plan_guide &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)   
 [sys.dm_exec_sql_text &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md)   
 [sys.dm_exec_text_query_plan &#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-text-query-plan-transact-sql.md)   
 [sp_control_plan_guide &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-control-plan-guide-transact-sql.md)  
  
  
