---
title: sys.dm_exec_query_plan (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/02/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_exec_query_plan_TSQL
- sys.dm_exec_query_plan
- dm_exec_query_plan
- sys.dm_exec_query_plan_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_query_plan dynamic management function
ms.assetid: e26f0867-9be3-4b2e-969e-7f2840230770
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: cb77a386ac0c7aa4fe6246b04723227b68ffa455
ms.sourcegitcommit: d92ad400799d8b74d5c601170167b86221f68afb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/16/2019
ms.locfileid: "58080250"
---
# <a name="sysdmexecqueryplan-transact-sql"></a>sys.dm_exec_query_plan (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

針對計畫控制代碼指定的批次，以 XML 格式傳回顯示計畫。 計畫控制代碼指定的計畫可以是快取或目前正在執行的計畫。  
  
執行程序表 XML 結構描述是發行及提供[颾 Microsoft 寍鯚](https://go.microsoft.com/fwlink/?linkid=43100&clcid=0x409)。 安裝有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的目錄也會提供這個項目。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
sys.dm_exec_query_plan(plan_handle)  
```  
  
## <a name="arguments"></a>引數  
*plan_handle*  
可唯一識別查詢執行計畫，該批次已經執行的語彙基元且其計畫位於計畫快取，或正在執行。 *plan_handle*已**varbinary(64)**。   

*Plan_handle*可以從下列動態管理物件取得：
  
-   [sys.dm_exec_cached_plans &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md)  
  
-   [sys.dm_exec_query_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)  
  
-   [sys.dm_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)  

-   [sys.dm_exec_procedure_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-procedure-stats-transact-sql.md)  

-   [sys.dm_exec_trigger_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-trigger-stats-transact-sql.md)  
  
## <a name="table-returned"></a>傳回的資料表  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**dbid**|**smallint**|當編譯對應於這個計畫的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式時，作用中內容資料庫的識別碼。 對於隨選和準備的 SQL 陳述式而言，則為編譯陳述式的資料庫識別碼。<br /><br /> 資料行可為 Null。|  
|**objectid**|**int**|這個查詢計畫的物件識別碼 (如預存程序或使用者自訂函數)。 針對隨選和備妥的批次，這個資料行是**null**。<br /><br /> 資料行可為 Null。|  
|**number**|**smallint**|編號預存程序整數。 例如，群組的程序**訂單**可能名為應用程式**orderproc; 1**， **orderproc; 2**，依此類推。 針對隨選和備妥的批次，這個資料行是**null**。<br /><br /> 資料行可為 Null。|  
|**encrypted**|**bit**|指出對應的預存程序是否加密。<br /><br /> 0 = 未加密<br /><br /> 1 = 加密<br /><br /> 資料行不可為 Null。|  
|**query_plan**|**xml**|包含指定的查詢執行計畫的編譯時間執行程序表表示法*plan_handle*。 顯示計畫是 XML 格式。 每個包含諸如特定 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式、預存程序呼叫和使用者自訂函數呼叫的批次，都會產生一份計畫。<br /><br /> 資料行可為 Null。|  
  
## <a name="remarks"></a>備註  
 在下列情況中，任何顯示計畫輸出都會傳入**query_plan**傳回之資料表的資料行**sys.dm_exec_query_plan**:  
  
-   使用指定的查詢計畫，如果*plan_handle*已從計畫快取中收回**query_plan**傳回之資料表的資料行是 null。 比方說，如果沒有時擷取計畫控制代碼，以及當它搭配之間的時間延遲可能會發生這種情況**sys.dm_exec_query_plan**。  
  
-   某些[!INCLUDE[tsql](../../includes/tsql-md.md)]陳述式不會快取，例如大量作業陳述式或陳述式包含字串常值大於 8 KB 的大小。 無法使用擷取這些陳述式的 XML 執行程序表**sys.dm_exec_query_plan**除非批次目前正在執行，因為它們不存在於快取。  
  
-   如果[!INCLUDE[tsql](../../includes/tsql-md.md)]批次或預存程序包含呼叫使用者定義函式呼叫或動態 sql，例如使用 EXEC (*字串*)、 已編譯使用者定義函式不包含資料表中的 XML 執行程序所傳回**sys.dm_exec_query_plan**批次或預存程序。 相反地，您必須進行個別呼叫**sys.dm_exec_query_plan**計畫控制代碼對應到使用者定義函式。  
  
 當隨選查詢使用簡單或強制參數化**query_plan**資料行會包含陳述式文字並不實際查詢計劃。 若要傳回的查詢計劃，請呼叫**sys.dm_exec_query_plan**準備參數化查詢的計畫控制代碼。 您可以判斷查詢是否已藉由參考參數化**sql**資料行[sys.syscacheobjects](../../relational-databases/system-compatibility-views/sys-syscacheobjects-transact-sql.md)檢視或文字資料行[sys.dm_exec_sql_text](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md)動態管理檢視。  
  
 基於中允許的巢狀層級數目的限制**xml**資料類型**sys.dm_exec_query_plan**無法傳回達到或超過 128 個層級的巢狀項目查詢計劃。 在舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，這會讓查詢計畫無法傳回並產生錯誤 6335。 在  [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Service Pack 2 和更新版本中， **query_plan**資料行會傳回 NULL。 您可以使用[sys.dm_exec_text_query_plan &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-exec-text-query-plan-transact-sql.md)動態管理函數，以文字格式傳回查詢計畫的輸出。  
  
## <a name="permissions"></a>Permissions  
 若要執行**sys.dm_exec_query_plan**，使用者必須是成員**sysadmin**固定伺服器角色，或有`VIEW SERVER STATE`伺服器的權限。  
  
## <a name="examples"></a>範例  
 下列範例示範如何使用**sys.dm_exec_query_plan**動態管理檢視。  
  
 若要檢視 XML 顯示計畫，執行下列查詢，查詢編輯器中的[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]，然後按一下**ShowPlanXML**中**query_plan**所傳回的資料表資料行**sys.dm_exec_query_plan**。 此時 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 摘要窗格會顯示 XML 顯示計畫。 將 XML 顯示計畫儲存至檔案，以滑鼠右鍵按一下**ShowPlanXML**中**query_plan**資料行中，按一下 **將結果存檔**，格式檔案命名為\< *file_name*>.sqlplan，例如 MyXMLShowplan.sqlplan。  
  
### <a name="a-retrieve-the-cached-query-plan-for-a-slow-running-transact-sql-query-or-batch"></a>A. 擷取執行緩慢的 Transact-SQL 查詢或批次之快取查詢計畫  
 各類型 [!INCLUDE[tsql](../../includes/tsql-md.md)] 批次的查詢計畫，如特定批次、預存程序和使用者自訂函數，都會快取在稱為計畫快取的記憶體區域中。 每個快取的查詢計畫都用一個稱為計畫控制代碼的唯一識別碼來識別。 您可以指定與這個計畫控制代碼**sys.dm_exec_query_plan**動態管理檢視來擷取特定的執行計畫[!INCLUDE[tsql](../../includes/tsql-md.md)]查詢或批次。  
  
 如果 [!INCLUDE[tsql](../../includes/tsql-md.md)] 查詢或批次在特定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 連接上執行了很長一段時間，請擷取這項查詢或批次的執行計畫來找出延遲的原因。 下列範例會顯示如何擷取執行緩慢的查詢或批次的 XML 顯示計畫。  
  
> [!NOTE]  
>  若要執行此範例中，取代的值*session_id*並*plan_handle*到您的伺服器特有的值。  
  
 首先，請利用 `sp_who` 預存程序來擷取正在執行查詢或批次之處理序的伺服器處理序識別碼 (SPID)：  
  
```sql  
USE master;  
GO  
exec sp_who;  
GO  
```  
  
 `sp_who` 傳回的結果集指出 SPID 是 `54`。 您可以搭配 `sys.dm_exec_requests` 動態管理檢視來使用 SPID，以利用下列查詢來擷取計畫控制代碼：  
  
```sql  
USE master;  
GO  
SELECT * FROM sys.dm_exec_requests  
WHERE session_id = 54;  
GO  
```  
  
 所傳回的資料表**sys.dm_exec_requests**指出執行緩慢查詢或批次的計畫控制代碼`0x06000100A27E7C1FA821B10600`，您可以指定為*plan_handle* 引數`sys.dm_exec_query_plan`擷取執行計畫以 XML 格式，如下所示。 中包含以 XML 格式執行緩慢查詢或批次的執行計畫**query_plan**所傳回的資料表資料行`sys.dm_exec_query_plan`。  
  
```sql  
USE master;  
GO  
SELECT * 
FROM sys.dm_exec_query_plan (0x06000100A27E7C1FA821B10600);  
GO  
```  
  
### <a name="b-retrieve-every-query-plan-from-the-plan-cache"></a>B. 從計畫快取中擷取每份查詢計畫  
 若要擷取計畫快取中所有查詢計畫的快照集，請查詢 `sys.dm_exec_cached_plans` 動態管理檢視，來擷取快取中所有查詢計畫的計畫控制代碼。 計畫控制代碼會儲存在 `plan_handle` 的 `sys.dm_exec_cached_plans` 資料行中。 之後，請依照下列方式，利用 CROSS APPLY 運算子，將計畫控制代碼傳給 `sys.dm_exec_query_plan`。 目前在計畫快取中的每項計畫之 XML 顯示計畫輸出，都是在傳回的資料表之 `query_plan` 資料行中。  
  
```sql  
USE master;  
GO  
SELECT * 
FROM sys.dm_exec_cached_plans AS cp 
CROSS APPLY sys.dm_exec_query_plan(cp.plan_handle);  
GO  
```  
  
### <a name="c-retrieve-every-query-plan-for-which-the-server-has-gathered-query-statistics-from-the-plan-cache"></a>C. 擷取伺服器已從計畫快取中收集了查詢統計資料的每項查詢計畫  
 若要擷取伺服器已收集了目前在計畫快取中的統計資料之所有查詢計畫的快照集，請查詢 `sys.dm_exec_query_stats` 動態管理檢視，以擷取快取中這些計畫的計畫控制代碼。 計畫控制代碼會儲存在 `plan_handle` 的 `sys.dm_exec_query_stats` 資料行中。 之後，請依照下列方式，利用 CROSS APPLY 運算子，將計畫控制代碼傳給 `sys.dm_exec_query_plan`。 伺服器已收集了目前在計畫快取中的統計資料之各項計畫之 XML 顯示計畫輸出，都是在傳回的資料表之 `query_plan` 資料行中。  
  
```sql  
USE master;  
GO  
SELECT * 
FROM sys.dm_exec_query_stats AS qs 
CROSS APPLY sys.dm_exec_query_plan(qs.plan_handle);  
GO  
```  
  
### <a name="d-retrieve-information-about-the-top-five-queries-by-average-cpu-time"></a>D. 擷取按平均 CPU 時間排列之前五項查詢的相關資訊  
 下列範例會傳回前五項查詢的計畫和平均 CPU 時間。  
  
```sql  
SELECT TOP 5 total_worker_time/execution_count AS [Avg CPU Time],  
   plan_handle, query_plan   
FROM sys.dm_exec_query_stats AS qs  
CROSS APPLY sys.dm_exec_query_plan(qs.plan_handle)  
ORDER BY total_worker_time/execution_count DESC;  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [動態管理檢視與函數 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [sys.dm_exec_cached_plans &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md)   
 [sys.dm_exec_query_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)   
 [sys.dm_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)   
 [sp_who &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-who-transact-sql.md)   
 [執行程序邏輯和實體運算子參考](../../relational-databases/showplan-logical-and-physical-operators-reference.md)   
 [sys.dm_exec_text_query_plan &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-text-query-plan-transact-sql.md)  
  
  
