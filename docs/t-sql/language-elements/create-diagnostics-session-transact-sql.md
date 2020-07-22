---
title: CREATE DIAGNOSTICS SESSION (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 662d019e-f217-49df-9e2f-b5662fa0342d
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 1c7d3419d7dfe087dfbae8ce11d8afd68f461892
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/22/2020
ms.locfileid: "86914044"
---
# <a name="create-diagnostics-session-transact-sql"></a>CREATE DIAGNOSTICS SESSION (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  診斷工作階段可讓您儲存關於系統或查詢效能的使用者定義詳細診斷資訊。  
  
 診斷工作階段通常是用來進行特定查詢的效能偵錯，或在應用裝置作業期間監視特定應用裝置元件的行為。  
  
> [!NOTE]  
>  您應該熟悉 XML 以使用診斷工作階段。  
  
## <a name="syntax"></a>語法  
  
```syntaxsql
Creating a new diagnostics session:  
CREATE DIAGNOSTICS SESSION diagnostics_name AS N'{<session_xml>}';  
  
<session_xml>::  
<Session>  
   [ <MaxItemCount>max_item_count_num</MaxItemCount> ]  
   <Filter>  
      { \<Event Name="event_name"/>  
         [ <Where>\<filter_property_name Name="value" ComparisonType="comp_type"/></Where> ] [ ,...n ]  
      } [ ,...n ]  
   </Filter> ]   
   <Capture>  
      \<Property Name="property_name"/> [ ,...n ]  
   </Capture>  
<Session>  
  
Retrieving results for a diagnostics session:  
SELECT * FROM master.sysdiag.diagnostics_name ;  
  
Removing results for a diagnostics session:  
DROP DIAGNOSTICS SESSION diagnostics_name ;  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引數
 *diagnostics_name*  
 診斷工作階段的名稱。 診斷工作階段名稱只能包含字元 a-z、A-Z 和 0-9。 此外，診斷工作階段名稱必須以字元作為開頭。 *diagnostics_name* 限制為 127 個字元。  
  
 *max_item_count_num*  
 要保存於檢視中的事件數目。 例如，如果指定 100，系統將在診斷工作階段中保存最近 100 個符合篩選準則的事件。 如果找到的相符事件少於 100 個，診斷工作階段將會包含少於 100 個事件。 *max_item_count_num* 必須至少為 100 且小於或等於 100,000。  
  
 *event_name*  
 定義要在診斷工作階段中收集的實際事件。  *event_name* 是列於 [sys.pdw_diag_events](../../relational-databases/system-catalog-views/sys-pdw-diag-events-transact-sql.md) \(英文\) 中且為 `sys.pdw_diag_events.is_enabled='True'` 的其中一個事件。  
  
 *filter_property_name*  
 要限制結果之屬性的名稱。 例如，如果您想要根據工作階段識別碼進行限制，*filter_property_name* 便應該是 *SessionId*。 如需 *filter_property_name* 的可能值清單，請參閱下方的＜*property_name*＞。  
  
 *value*  
 要針對 *filter_property_name* 進行評估的值。 值類型必須與屬性類型相符。 例如，如果屬性類型是 decimal，*value* 的類型就必須是 decimal。  
  
 *comp_type*  
 比較類型。 可能的值為：Equals、EqualsOrGreaterThan、EqualsOrLessThan、GreaterThan、LessThan、NotEquals、Contains、RegEx  
  
 *property_name*  
 與事件相關的屬性。  屬性名稱可以是擷取標記的一部分，或用來作為篩選準則的一部分。  
  
|屬性名稱|描述|  
|-------------------|-----------------|  
|UserName|使用者 (登入) 名稱。|  
|SessionId|工作階段識別碼。|  
|QueryId|查詢識別碼。|  
|CommandType|命令類型。|  
|CommandText|所處理之命令內的文字。|  
|OperationType|事件的作業類型。|  
|Duration|事件的持續時間。|  
|SPID|服務處理序識別碼。|  
  
## <a name="remarks"></a>備註  
 允許每位使用者最多 10 個並行診斷工作階段。 如需目前工作階段的清單，請參閱 [sys.pdw_diag_sessions](../../relational-databases/system-catalog-views/sys-pdw-diag-sessions-transact-sql.md) \(英文\)，並使用 `DROP DIAGNOSTICS SESSION` 卸除任何不需要的工作階段。  
  
 診斷工作階段將繼續收集中繼資料，直到被卸除為止。  
  
## <a name="permissions"></a>權限  
 需要 **ALTER SERVER STATE** 權限。  
  
## <a name="locking"></a>鎖定  
 採用診斷工作階段資料表上的共用鎖定。  
  
## <a name="examples"></a>範例  
  
### <a name="a-creating-a-diagnostics-session"></a>A. 建立診斷工作階段  
 此範例會建立診斷工作階段，來記錄資料庫引擎效能的計量。 範例會建立能接聽引擎查詢的執行/結束事件及封鎖 DMS 事件的診斷工作階段。 傳回的內容是命令文字、電腦名稱、要求識別碼 (查詢識別碼)，以及建立事件的工作階段。  
  
```  
CREATE DIAGNOSTICS SESSION MYDIAGSESSION AS N'  
<Session>  
   <MaxItemCount>100</MaxItemCount>  
   <Filter>  
      <Event Name="EngineInstrumentation:EngineQueryRunningEvent" />  
      <Event Name="DmsCoreInstrumentation:DmsBlockingQueueEnqueueBeginEvent" />  
      <Where>  
         <SessionId Value="381" ComparisonType="NotEquals" />  
      </Where>  
   </Filter>  
   <Capture>  
      <Property Name="Query.CommandText" />  
      <Property Name="MachineName" />  
      <Property Name="Query.QueryId" />  
      <Property Name="Alias" />  
      <Property Name="Duration" />  
      <Property Name="Session.SessionId" />  
   </Capture>  
</Session>';  
```  
  
 在建立診斷工作階段之後，會執行查詢。  
  
```  
SELECT COUNT(EmployeeKey) FROM AdventureWorksPDW2012..FactSalesQuota;  
```  
  
 接著，會從 sysdiag 結構描述中選取診斷工作階段結果，以進行檢視。  
  
```  
SELECT * FROM master.sysdiag.MYDIAGSESSION;  
```  
  
 注意到 sysdiag 結構描述會包含以您診斷工作階段名稱命名的檢視。  
  
 若只要查看您連線的活動，請加入 `Session.SPID` 屬性並將 `WHERE [Session.SPID] = @@spid;` 加入至查詢。  
  
 當您完成診斷工作階段之後，請使用 **DROP DIAGNOSTICS** 命令來卸除它。  
  
```  
DROP DIAGNOSTICS SESSION MYDIAGSESSION;  
```  
  
### <a name="b-alternative-diagnostic-session"></a>B. 替代的診斷工作階段  
 含有些許不同屬性的第二個範例。  
  
```  
-- Determine the session_id of your current session  
SELECT TOP 1 session_id();  
-- Replace \<*session_number*> in the code below with the numbers in your session_id  
CREATE DIAGNOSTICS SESSION PdwOptimizationDiagnostics AS N'  
<Session>  
   <MaxItemCount>100</MaxItemCount>  
   <Filter>  
      <Event Name="EngineInstrumentation:MemoGenerationBeginEvent" />  
      <Event Name="EngineInstrumentation:MemoGenerationEndEvent" />  
      <Event Name="DSQLInstrumentation:OptimizationBeginEvent" />  
      <Event Name="DSQLInstrumentation:OptimizationEndEvent" />  
      <Event Name="DSQLInstrumentation:BuildRelOpContextTreeBeginEvent" />  
      <Event Name="DSQLInstrumentation:PostPlanGenModifiersEndEvent" />  
      <Where>  
         <SessionId Value="\<*session_number*>" ComparisonType="Equals" />  
      </Where>  
   </Filter>  
   <Capture>  
      <Property Name="Session.SessionId" />  
      <Property Name="Query.QueryId" />  
      <Property Name="Query.CommandText" />  
      <Property Name="Name" />  
      <Property Name="DateTimePublished" />  
      <Property Name="DateTimePublished.Ticks" />  
  </Capture>  
</Session>';  
```  
  
 執行查詢，例如：  
  
```  
USE ssawPDW;  
GO  
SELECT * FROM dbo.FactFinance;  
```  
  
 下列查詢會傳回授權時機：  
  
```  
SELECT *   
FROM master.sysdiag.PdwOptimizationDiagnostics   
ORDER BY DateTimePublished;  
```  
  
 當您完成診斷工作階段之後，請使用 **DROP DIAGNOSTICS** 命令來卸除它。  
  
```  
DROP DIAGNOSTICS SESSION PdwOptimizationDiagnostics;  
```  
  
  
