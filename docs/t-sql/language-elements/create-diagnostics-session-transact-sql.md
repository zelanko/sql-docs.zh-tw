---
title: "建立診斷工作階段 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 662d019e-f217-49df-9e2f-b5662fa0342d
caps.latest.revision: 9
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 71f3463ad4d91bd117c322e9e63c0b331b07ca9f
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="create-diagnostics-session-transact-sql"></a>建立診斷工作階段 (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw_md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  診斷工作階段可讓您儲存對系統或查詢效能的詳細的使用者定義的診斷資訊。  
  
 偵錯效能，為特定的查詢，或是用來監視特定的應用裝置元件行為應用裝置作業期間，通常會使用的診斷工作階段。  
  
> [!NOTE]  
>  您應該熟悉 XML 若要使用的診斷工作階段。  
  
## <a name="syntax"></a>語法  
  
```  
Creating a new diagnostics session:  
CREATE DIAGNOSTICS SESSION diagnostics_name AS N’{<session_xml>}’;  
  
<session_xml>::  
<Session>  
   [ <MaxItemCount>max_item_count_num</MaxItemCount> ]  
   <Filter>  
      { \<Event Name=”event_name”/>  
         [ <Where>\<filter_property_name Name=”value” ComparisonType="comp_type"/></Where> ] [ ,...n ]  
      } [ ,...n ]  
   </Filter> ]   
   <Capture>  
      \<Property Name=”property_name”/> [ ,...n ]  
   </Capture>  
<Session>  
  
Retrieving results for a diagnostics session:  
SELECT * FROM master.sysdiag.diagnostics_name ;  
  
Removing results for a diagnostics session:  
DROP DIAGNOSTICS SESSION diagnostics_name ;  
```  
  
## <a name="arguments"></a>引數  
 *diagnostics_name*  
 診斷工作階段的名稱。 診斷工作階段名稱可以包含字元 a-z、 A-Z、 和 0-9 只。 此外，診斷工作階段名稱必須以字元開頭。 *diagnostics_name*限制為 127 個字元。  
  
 *max_item_count_num*  
 要保存在檢視中的事件數目。 比方說，如果指定 100，則比對的篩選準則的最近 100 個事件將會保存至診斷工作階段。 如果找不到少於 100 比對事件，診斷工作階段就會包含不超過 100 個事件。 *max_item_count_num*必須至少為 100 且小於或等於 100,000。  
  
 *event_name*  
 定義要收集診斷工作階段中的實際事件。  *event_name*是其中一個事件中所列[sys.pdw_diag_events](http://msdn.microsoft.com/en-us/d813aac0-cea1-4f53-b8e8-d26824bc2587)其中`sys.pdw_diag_events.is_enabled='True'`。  
  
 *filter_property_name*  
 要限制結果屬性的名稱。 例如，如果您想要限制根據工作階段識別碼*filter_property_name*應該*SessionId*。 請參閱*property_name*下方的可能值清單*filter_property_name*。  
  
 *value*  
 要評估的值*filter_property_name*。 實值型別必須符合屬性類型。 例如，如果屬性類型就是 decimal，類型*值*必須是十進位。  
  
 *comp_type*  
 比較類型。 可能的值是： 等於、 EqualsOrGreaterThan、 EqualsOrLessThan、 GreaterThan、 LessThan、 NotEquals、 Contains、 RegEx  
  
 *property_name*  
 與事件相關的屬性。  屬性名稱可以是一部分擷取標記，或做為篩選準則的一部分。  
  
|屬性名稱|Description|  
|-------------------|-----------------|  
|UserName|使用者 （登入） 名稱。|  
|SessionId|工作階段識別碼。|  
|QueryId|查詢識別碼。|  
|CommandType|命令類型。|  
|CommandText|內處理的命令文字。|  
|OperationType|事件的作業類型。|  
|有效期間|事件持續時間。|  
|SPID|服務處理序識別碼。|  
  
## <a name="remarks"></a>備註  
 每個使用者允許最多 10 個並行的診斷工作階段。 請參閱[sys.pdw_diag_sessions](http://msdn.microsoft.com/en-us/ca111ddc-2787-4205-baf0-1a242c0257a9)一份目前的工作階段的卸除任何不需要使用工作階段的`DROP DIAGNOSTICS SESSION`。  
  
 診斷工作階段將會繼續收集直到卸除的中繼資料。  
  
## <a name="permissions"></a>Permissions  
 需要**ALTER SERVER STATE**權限。  
  
## <a name="locking"></a>鎖定  
 在診斷工作階段的資料表上採用共用的鎖定。  
  
## <a name="examples"></a>範例  
  
### <a name="a-creating-a-diagnostics-session"></a>A. 建立診斷工作階段  
 這個範例會建立記錄的資料庫引擎的效能度量的診斷工作階段。 此範例會建立接聽引擎查詢執行/結束事件和封鎖的 DMS 事件在診斷工作階段。 傳回的內容是命令文字、 電腦名稱、 要求識別碼 (查詢 id) 和建立事件工作階段。  
  
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
  
 建立診斷工作階段之後執行查詢。  
  
```  
SELECT COUNT(EmployeeKey) FROM AdventureWorksPDW2012..FactSalesQuota;  
```  
  
 選取從 sysdiag 結構描述，然後檢視診斷工作階段結果。  
  
```  
SELECT * FROM master.sysdiag.MYDIAGSESSION;  
```  
  
 請注意 sysdiag 結構描述包含名為您的診斷工作階段名稱的檢視。  
  
 若要檢視連線的活動，`Session.SPID`屬性並新增`WHERE [Session.SPID] = @@spid;`至查詢。  
  
 當您在診斷工作階段完成時，使用卸除該**卸除診斷**命令。  
  
```  
DROP DIAGNOSTICS SESSION MYDIAGSESSION;  
```  
  
### <a name="b-alternative-diagnostic-session"></a>B. 替代的診斷工作階段  
 含有屬性些許不同的第二個範例。  
  
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
  
 執行查詢時，例如：  
  
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
  
 當您在診斷工作階段完成時，使用卸除該**卸除診斷**命令。  
  
```  
DROP DIAGNOSTICS SESSION PdwOptimizationDiagnostics;  
```  
  
  
